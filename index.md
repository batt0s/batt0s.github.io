## Hakkımda

Matematik ve Bilgisayar Bilimleri 1. sınıf öğrencisiyim. Yıllardır hobi olarak yazılımla uğraşıyorum ve günlük olarak Linux kullanıp sürekli bir şeyler deniyorum.

Bu sitede ilgimi çeken konular hakkında yazılar yazıp tecrübelerimi paylaşıyorum ve gelecekteki kendime notlar bırakıyorum.

[Github Profilim](https://github.com/batt0s)

İletişim: [kerem.ullen@pm.me](mailto:kerem.ullen@pm.me)

## Posts
{% for post in site.posts %}
 <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
 <p><small><strong>{{ post.date | date: "%B %e, %Y" }} - {{ post.category }}</strong></small></p>            
{% endfor %}
