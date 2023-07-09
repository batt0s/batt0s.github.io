---
layout: default
category: linux
tags: [linux,python]
title: Django-Gunicorn-Nginx | Django Uygulamasını Yayınlamak
---
# Django Uygulamasını Server Üzerinde Yayınlamak

Django ile bir uygulama yaptınız ve şimdi de bu uygulamayı yayınlamak istiyorsunuz. Elinizde bir sunucu var.  Ben bu yazı için Ubuntu Server 22.04 kullanacağım. 

Boş bir Ubuntu Server kurulumundan sonra başlıyoruz. Root kullanıcısında değil sudo yetkileri olan normal bir kullanıcıdan yapacağız işlemleri. `sudo apt update` ve `sudo apt upgrade -y` ile sunucunuzu güncelleyin. Ev dizininize gelin.

Not: Bilmeyenler için bash kullanırken eğer normal bir kullanıcı olarak komut giriyorsanız `$` işareti görürsünüz ama eğer root kullanıcısıysanız `#` işareti görürsünüz. Promptların başında bu işaretleri koyuyorum ki ne olarak komut girdiğimi anlayın.

## venv ve gerekli paketlerin kurulumu

Öncelikle bir virtual env e ihtiyaç var. Bunun için:
```
~$ sudo apt install python3-venv
```  
ile "venv" paketini kurduk. Sonrasında venv oluşturmak için: 
```
~$ python3 -m venv env
```
 diyoruz. "env" adında bir venv oluşturduk. Aktif etmek için:
```
~$ source env/bin/activate
```
 Daha sonra gerekli paketleri kurun (projenizde kullandığınız paketler, requirements.txt vs). Gunicorn u kurmak için:
```
(env) ~$ pip install gunicorn
```

## Gerekli dizinlerin oluşturulması ve settings.py değişiklikleri

Benim elimde bir uygulama olmadığı için şimdilik boş bir django uygulaması oluşturacağım. Bunun için bir dizin oluşturuyorum, `mkdir myproject`, ve bu dizinin içine giriyorum, `cd myproject`, ardından projeyi oluşturuyorum, `django-admin startproject config .`. Ardından $HOME dizinine geri dönüyorum (not: `cd` komutuna parametre vermezseniz sizi $HOME dizinine alacaktır). 

Şu anda "env" ve "myproject" adında iki dizin olmalı. 
```
(env) ~$ mkdir logs static
```
ile logs ve static adında iki dizin daha oluşturuyoruz. Daha sonra `cd logs` ile dizinin içine girip `mkdir gunicorn nginx` komutu ile iki dizin daha oluşturup ev dizinine dönüyoruz.

Şimdi uygulamamızda bir değişiklik yapmamız lazım. `settings.py` ye gelip `STATIC_URL="/home/<kullanıcı>/static/"` yapmanız lazım ve `ALLOWED_HOSTS` a sunucunun IP adresini (ya da domain) eklemeniz lazım. 

## Gunicorn'un ayarlanması

myproject/config altında "gunicorn_config.py" adında bir dosya oluşturun. İçeriği şu şekilde olmalı:
```py
command="/home/<kullanıcı>/env/bin/gunicorn"
pythonpath="/home/<kullanıcı>/myproject"
bind="<ip>:8000"
workers=3
accesslog="/home/<kullanıcı>/logs/gunicorn/access.log"
errorlog="/home/<kullanıcı>/logs/gunicorn/error.log"
```

Satır satır açıklarsak: `command` gunicorn un yolu. `pythonpath` projenizin yolu. `bind` çalışacağı ip:port. `workers` kaç worker çalıştıracağınız. `accesslog` access loglarının tutulacağı dosyanın yolu ve `errorlog` error loglarının tutulacağı dosyanın yolu. 

Kaydedip çıkıyoruz.

Artık `(env) ~$ gunicorn -c myproject/config/gunicorn_config.py myproject.config.wsgi` ile gunicorn u başlatabilirsiniz ve ip:8000 adresine giderseniz uygulamayı görebilirsiniz. Ama biz her seferinde böyle çalıştırmayacağız. Otomatik çalışması için `supervisor` kullanacağım. Supervisor kullanırsak her sunucu başladığında arkaplanda otomatik olarak çalışacak ve hata sonucu kapandığında kendini yeniden başlatacak. 

Supervisor kurmak için 
```
$ sudo apt install supervisor -y
```
Daha sonrasında bir supervisor process i oluşturmalıyız. Supervisor process lerinin hepsi `/etc/supervisor/conf.d/` altında tutulur. Bu dizine `$ cd /etc/supervisor/conf.d` komutu ile gidiyoruz. Ardından `$ sudo touch myproject_gunicorn.conf` komutu ile bir dosya oluşturuyoruz ve düzenliyoruz. Düzenlerken hangi editörü kullanıyorsanız `sudo` ile açmayı unutmayın yoksa kaydedemezsiniz (örn:`$ sudo vi myproject_gunicorn.conf`). Dosya içeriği şu şekilde olmalı: 
```
[program:myproject_gunicorn]
user=<kullanıcı>
directory=/home/<kullnıcı>/myproject
command=/home/<kullanıcı>/env/bin/gunicorn -c /home/<kullanıcı>/myproject/config/gunicorn_config.py config.wsgi 
autostart=true
autorestart=true
```
Satır satır açarsak: `user` komutun çalıştırılacağı kullanıcı. `directory` çalışma dizini. `command` çalışacak komut. `autostart` sunucu açıldığında otomatik başlatma. `autorestart` process hata alıp çökerse tekrar başlatma. 

Bunu kaydedip çıkıyoruz.

Ardından 
```
$ sudo supervisorctl reread
$ sudo supervisorctl update
```
komutları ile supervisor un eklediğimiz dosyayı okumasını sağlıyoruz. `autostart` dediğimiz için direkt olarak başlatılacaktır. Artık ip:8000 adresinde gunicorn un çalıştığını görebilirsiniz. 

`$ sudo supervisorctl status myproject_gunicorn` ile process in durumunu kontrol edebilir, `start` `stop` ve `restart` ile başlatıp, durdurup, yeniden başlatabilirsiniz.

## Nginx ayarlanması
Şimdi sıra nginx in ayarlanmasında. 

```
$ cd /etc/nginx/sites-available
``` 
ile diznimizi değiştiriyoruz.
```
$ sudo touch myproject
```
ile dosya oluşturuyoruz. Dosyanın içeriği şu şekilde olmalı:
```
server {
	listen 80;
	server_name <ip veya domain>;
	
	access_log /home/<kullanıcı>/logs/nginx/access.log;
	error_log /home/<kullanıcı>/logs/nginx/error.log;

	location /static/ {
		root /home/<kullanıcı>/static;
	}

	location / {
		proxy_pass http://192.168.124.140:8000;
	}
}
```

Açarsak: `listen` port. `server_name` ip veya domain. `access_log` access loglarının tutulacağı dosyanın yolu. `error_log` error loglarının tutulacağı dosyanın yolu. `location /static/`de `root` bizim static dizinimizin yolu. `location /` ve `proxy_pass` ile gelen requestleri gunicorn a iletiyoruz. 

Kaydedip çıkıyoruz. Ardından aktif olması için önce `sites-enabled` a bir link oluşturuyoruz ve nginx i yeniden başlatıyoruz.
```
$ sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
$ sudo systemctl restart nginx
```

Artık ip adresinize bir tarayıcıdan girdiğinizde uygulamanızı görebilmeniz lazım.

---

Bir sıkıntı yaşarsanız bana ulaşabilirsiniz, elimden geldiğince yardımcı olmaya çalışırım.

Kerem Üllenoğlu \
kerem.ullen@proton.me