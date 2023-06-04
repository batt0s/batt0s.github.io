---
layout: default
category: security
tags: [security]
title: Dosyaları buluta göndermeden önce bunu yapın - Dosya Şifreleme
---
# Cloud Storage

Çoğumuz Cloud Storage yani Bulut Depolama'yı kullanıyoruz. Dosyalarınızı  paylaşmak ya da verilerinizi yedeklemek için kolay ve kullanışlı bir yöntem. Peki bu bulut sistemlerine nasıl verilerinizi kendiniz yükleyecek kadar güveniyorsunuz? Günün sonunda Cloud dediğimiz şey başka birinin bilgisayarı. Ne kadar sistem size verilerinizin şifrelendiğini söylese de milyon dolarlık şirketlerin sözüne güvenmek bu kadar kolay mı? İstedikleri zaman dosyaları görebilirler. Eğer bir şifreleme yoksa bu sadece dosyaları yüklediğiniz sistemin sahiplerinin değil ayrıca hackerların da dosyaları ele geçirdiği zaman rahatça okuyabilmesi demek. Dosyaları şifreliyorlarsa bile yine sonuç olarak sistem sahipleri şifreliyor, günün sonunda bir şekilde dosyalarınıza erişebiliyorlar. 

Ben şahsen bu sistemlere güvenmiyorum ve güvensem de işimi güvene bırakmak istemiyorum. 

Verileri korumak için yapabileceğiniz şeyler var, bunlardan biri de dosyaları sunucuya göndermeden önce kendiniz şifrelemeniz. 


# Dosya şifreleme

Bu işlem için ben açık kaynaklı OpenGPG yazılımını kullanıyorum.

Şifreleme dediğiniz zaman temel olarak iki şifreleme türü var. Simetrik ve Asimetrik. Basitçe simetrik şifrelemede bir parola seçersiniz ve şifrelemeyi o parola ile yapar daha sonra da aynı parola ile şifrelemeyi çözersiniz. Asimetrikte iki tür anahtarınız olur, bunlardan biri Public Key diğeri Private Key. Public Key ile şifreleme yapar, Private Key ile şifreyi çözersiniz. Asimetrik şifreleme genelde iki kişi arasında kullanılır. Bizim durumumuzda simetrik şifreleme daha mantıklı. 

Şimdi uygulamaya geçelim. 

```bash
$ pwd
/home/battos/gpg
$ ls
secret.txt
$ cat secret.txt
batt0s.github.io
```

Göründüğü gibi, bulunduğum dizinin içerisinde bir `secret.txt` dosyası var ve bu dosyanın içeriği "batt0s.github.io". Bu dosyayı buluta göndermeden önce şifrelemek istiyorum.

```bash
$ gpg -c --no-symkey-cache --cipher-algo AES256 secret.txt
```

Bu satırı açarsak: `-c` simetrik şifreleme olduğunu belirtir, `--no-symkey-cache` belirlenen parolanın cache de saklanmasını istemediğimizi belirtir, `--cipher-algo AES256` şifrelemenin AES256 algoritması ile yapılmasını istediğimizi belirtir. Daha sonrasında en sonda dosyamız. Bu komutu girip entera bastığınızda sizden parola ister, parolanızı girin. 

```bash
$ ls
secret.txt    secret.txt.gpg
```

Oluşan `secret.txt.gpg` bizim şifrelenmiş dosyamız. Yazdırmaya çalışırsak okuyamacağımız bir çıktı verir.

```bash
$ cat secret.txt.gpg
�       �l��4��PF��HG~�!<`�z~�X
                               �>z4���ʥ�YвI$CG2� ���w�ط�$i���i,�>��+��:�q��0�4�b�⏎      
```

Şimdi orijinal dosyamızı silelim. 

```bash
$ rm secret.txt
$ ls
secret.txt.gpg
```

Şifrelenmiş dosyayı açmak için yapmamız gereken

```bash
$ gpg secret.txt.gpg
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
$ ls 
secret.txt    secret.txt.gpg
$ cat secret.txt
batt0s.github.io
```

Bu komuta ekstra bir şey vermeye gerek yok, GPG otomatik olarak şifreli bir dosya olduğunu ve onu açmaya çalıştığınızı anlayacak, ardından parola soracak ve parolayı doğru girdiğiniz takdirde yukarıdaki gibi `secret.txt` dosyası oluşması lazım. Dosyayı yazdırmaya çalıştığınızda orijinal içeriğe ulaştığınızı görürsünüz.

# Klasörler

Klasörleri şifrelemek için yapmanız gereken şey klasörü tar arşivine çevirmek. 

---

[Kerem Ü](mailto:kerem.ullen@pm.me)