## Hakkımda

Merhaba, ben Kerem.
Yazılım Geliştirici, Matematik ve Bilgisayar Bilimleri Lisans Öğrencisi, Linux Tutkunu. <br>
Yıllardır hobi olarak teknoloj ile uğraşıyorum. Sürekli yeni bir şeyler deniyorum. Bu sitede ilgimi çeken konular hakkında yazılar yazıp tecrübelerimi paylaşıyor ve kendime notlar bırakıyorum. <br>
Özellikle Go ve Python kullanıyorum. Server-side yazılımlar geliştirmeye odaklanıyorum ama yazılımın ve matematiğin her türlü dalına ilgim var.


## Bağlantılar
- Email: [kerem.ullen@pm.me](mailto:kerem.ullen@pm.me) <br>
- Website: [battos.dev](https://battos.dev) <br>
- Github: [@batt0s](https://github.com/batt0s) <br>
- LinkedIn: [linkedin.com/in/kerem-ullen](https://linkedin.com/in/kerem-ullen) <br>
- YouTube: [@packagebattos](https://www.youtube.com/@packagebattos)


## Projeler
### [GoShort](https://goshort.battos.dev)
- Go öğrenirken yaptığım bir URL kısaltıcı
- Kodları GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/goshort](https://github.com/batt0s/goshort)

### [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Resmi olmayan [Evrim Ağacı Sözler](https://evrimagaci.org/sozler) API.
- [Render](https://render.com) üzerinde yayınlandı: [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Kodlarını GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/ea-quotes-api](https://github.com/batt0s/ea-quotes-api)

## Yazılar
{% for post in site.posts %}
 <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
 <p><small><strong>{{ post.date | date: "%B %e, %Y" }} - {{ post.category }}</strong></small></p>            
{% endfor %}
