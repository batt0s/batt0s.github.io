## Hakkımda

Merhaba, ben Kerem.
Yazılım Geliştirici, Matematik ve Bilgisayar Bilimleri Lisans Öğrencisi, Linux Tutkunu. <br>
Yıllardır hobi olarak teknoloj ile uğraşıyorum. Sürekli yeni bir şeyler deniyorum. Bu sitede ilgimi çeken konular hakkında yazılar yazıp tecrübelerimi paylaşıyor ve kendime notlar bırakıyorum. <br>
Özellikle Go ve Python kullanıyorum. Server-side yazılımlar geliştirmeye odaklanıyorum ama yazılımın ve matematiğin her türlü dalına ilgim var. <br>

## [Yazılar](https://pages.battos.dev/#yaz%C4%B1lar)

## Ders Notları
Eskişehir Osmangazi Üniversitesi, Fen Fakültesi, Matematik ve Bilgisayar Bilimleri. <br>
Bölümün bir öğrencisi olarak olabildiğince ders notu biriktiriyorum ve dijital ortamlara aktarmaya çalışıyorum. Ayrıca linklerde sadece ders notları değil ders ile ilgili bulabildiğim ve faydalandığım çeşitli kaynaklar da var. <br>
Burada olmayan bir dersin notunu arıyorsanız bana [kerem.ullen@pm.me](mailto:kerem.ullen@pm.me) üzerinden ulaşın, elimden geldiğince yardımcı olmaya çalışırım. <br>
- [Temel Bilgi Teknolojileri / Temel Bilgisayar Bilimleri](https://drive.google.com/drive/folders/114AqSWQ5SjU67F1DaJ189YMiXWbIMYY2?usp=sharing)
- [Bilgisayar Programlama](https://drive.google.com/drive/folders/15DkWwOhSx6x9sYirSPxWKKUXGroWL_HG?usp=sharing)
- [Analiz](https://drive.google.com/drive/folders/157ylXhVWRLjuQbD8tviMB0vMi676valJ?usp=sharing)
- [Analitik Geometri](https://drive.google.com/drive/folders/13BmVgDLoyFYbyQkSwvFn-8Clo7inGo0O?usp=drive_link)
- [Lineer Cebir](https://drive.google.com/drive/folders/1-96MpiRPlqRg1gC72VZGqPStRiGnNS4G?usp=drive_link)

## Bağlantılar
- Email: [kerem.ullen@pm.me](mailto:kerem.ullen@pm.me) <br>
- Website: [battos.dev](https://battos.dev) <br>
- Github: [@batt0s](https://github.com/batt0s) <br>
- LinkedIn: [linkedin.com/in/kerem-ullen](https://linkedin.com/in/kerem-ullen) <br>
- YouTube: [@packagebattos](https://www.youtube.com/@packagebattos)


## Projeler
### [Riemann-py](https://riemann.battos.dev/)
- Riemann Toplamı (İntegrali) Hesaplamak ve Görselleştirmek için basit bir web sayfası
- Python kullanıldı. Hesaplar için Sympy, görselleştirme için matplotlib, web için Flask.
- Kodları GitHub üzerinden görüntüleyebilirsiniz: [github.com/batt0s/riemann-py](https://github.com/batt0s/riemann-py)

### [GoShort](https://goshort.battos.dev)
- Go öğrenirken yaptığım bir URL kısaltıcı
- Kodları GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/goshort](https://github.com/batt0s/goshort)

### [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Resmi olmayan [Evrim Ağacı Sözler](https://evrimagaci.org/sozler) API.
- [Render](https://render.com) üzerinde yayınlandı: [ea-quotes-api](https://ea-quotes-api.onrender.com/)
- Kodlarını GitHub üzerinde görüntüleyebilirsiniz: [github.com/batt0s/ea-quotes-api](https://github.com/batt0s/ea-quotes-api)

### [MyAnimeList Dataminer](https://github.com/batt0s/mal-dataminer/)


## Yazılar
{% for post in site.posts %}
 <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
 <p><small><strong>{{ post.date | date: "%B %e, %Y" }} - {{ post.category }}</strong></small></p>            
{% endfor %}
