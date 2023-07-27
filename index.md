## Hakkımda

Matematik ve Bilgisayar Bilimleri okuyorum. Yıllardır hobi olarak teknoloji uğraşıyorum. Günlük olarak Linux kullanıp sürekli bir şeyler deniyorum. Python ile başladığım serüvende birçok programlama dili denedim. Linux ve yazılım en büyük iki hobim ve bu hobilerimin aynı zamanda hayatım boyu yapacağım işim olması için uğraşıyorum.

Bu sitede ilgimi çeken konular hakkında yazılar yazıp tecrübelerimi paylaşıyorum ve kendime notlar bırakıyorum.

İletişim: [kerem.ullen@pm.me](mailto:kerem.ullen@pm.me) <br>
[Github Profilim](https://github.com/batt0s) <br>
[Linkedin](https://www.linkedin.com/in/kerem-ullen)

## Projects
### [GoShort](https://goshort.onrender.com/)
- Go öğrenirken yaptığım bir URL kısaltıcı
- Render üzerinde yayınlandı: [GoShort](https://goshort.onrender.com/)
- Kodları GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/goshort](https://github.com/batt0s/goshort)
- Bu projeyi yaparken Go da net/http ve [chi](https://github.com/go-chi/chi) paketini kullanarak API yapmayı; [GORM](https://gorm.io/) ve PostgreSQL kullanmayı; JavaScript ile bir API kullanmayı; Go da API için testler yazmayı; GitHub Actions kullanmayı; [Render](https://render.com) da microservice yayınlamayı öğrendim.

### [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Python da web scrapping öğrenirken [Evrim Ağacı Sözler](https://evrimagaci.org/sozler) i kullanmıştım. Daha sonra FastAPI öğrenirken böyle bir API yazdım. Büyük bir proje değil ama buraya koymak istedim.
- [Render](https://render.com) üzerinde yayınlandı: [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Kodlarını GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/ea-quotes-api](https://github.com/batt0s/ea-quotes-api)

## Posts
{% for post in site.posts %}
 <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
 <p><small><strong>{{ post.date | date: "%B %e, %Y" }} - {{ post.category }}</strong></small></p>            
{% endfor %}
