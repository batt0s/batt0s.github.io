## Hakkımda

Merhaba, ben Kerem Üllenoğlu.
Yazılım Geliştirici, Matematik ve Bilgisayar Bilimleri Lisans Öğrencisi, Linux Tutkunu. <br>
Yıllardır hobi olarak teknoloji ile uğraşıyorum. Sürekli yeni bir şeyler deniyorum. Şu sıralar özellikle Kodlama Teorisi (Coding Theory) ve Kuantum Sonrası Kriptografi (Post-Quantum Cryptography) ile ilgileniyorum. Bu sitede ilgimi çeken konular hakkında yazılar yazıp tecrübelerimi paylaşıyor ve kendime notlar bırakıyorum. <br>

## Bağlantılar
- Email: [me@battos.dev](mailto:me@battos.dev) <br>
- Website: [battos.dev](https://battos.dev) <br>
- Github: [@batt0s](https://github.com/batt0s) <br>
- LinkedIn: [linkedin.com/in/kerem-ullen](https://linkedin.com/in/kerem-ullen) <br>
- YouTube: [@packagebattos](https://www.youtube.com/@packagebattos) <br>
- Terminal: `ssh battos.dev`


## Projeler
### [mceliece_rs](https://github.com/batt0s/mceliece_rs)
- [Classic McEliece](https://classic.mceliece.org/) kuantum sonrası kriptosisteminin Rust ile yazılmış, sabit zamanlı (constant-time) implementasyonu.
- Bitirme projem; NIST PQC spesifikasyonuna ve Known Answer Test (KAT) vektörlerine uyumlu.
- Zamanlama yan kanalı saldırılarına (CCA) karşı sabit zamanlı decapsulation ve implicit rejection içeriyor.
- Rust çekirdek kütüphanesi ve PyO3 ile Python binding'leri olmak üzere iki crate'ten oluşuyor.
- İlgili yazı: [Implementing PQC - Building Classic McEliece in Rust]({{ "/cryptography/2026/07/28/mceliece.html" | relative_url }})

### [pqc-share](https://github.com/batt0s/pqc-share)
- Kuantum sonrası güvenli, uçtan uca şifreli peer-to-peer dosya paylaşım aracı.
- Anahtar kapsülleme (KEM) için Classic McEliece, veri şifreleme için AES-256-GCM kullanıyor.
- TCP üzerinden iki makine arasında dosya transferi sağlıyor.

### [rizzy](https://github.com/batt0s/rizzy)
- Go ile yazılmış basit, yorumlanan (interpreted) bir programlama dili.
- Interpreter'ların çalışma mantığını anlamak amacıyla *"Writing an Interpreter in Go"* kitabının üzerine konularak geliştirildi.

### [hausdorff-dist](https://github.com/batt0s/hausdorff-dist)
- Kompakt kümeler arasındaki Hausdorff uzaklığını interaktif olarak hesaplayıp görselleştiren Streamlit uygulaması.
- Kümeleri denklem/eşitsizlik olarak tanımlayıp farklı metrikler seçebiliyorsunuz; kritik tanık vektörleri çiziliyor.
- Python ile geliştirildi (Sympy, NumPy, Matplotlib, Streamlit).

### [anime-success-predictor-ml](https://github.com/batt0s/anime-success-predictor-ml)
- Makine öğrenmesi ile bir animenin "Hit" mi "Flop" mu olacağını tahmin eden Random Forest sınıflandırıcısı.
- Yüksek recall için threshold tuning ile optimize edildi.
- Veri seti MyAnimeList'ten toplandı ve [Kaggle](https://www.kaggle.com/datasets/battos/myanimelist-animes) üzerinde paylaşıldı.

### Daha Fazlası
Tüm projelerime ve güncel çalışmalarıma GitHub profilimden ulaşabilirsiniz: **[github.com/batt0s](https://github.com/batt0s?tab=repositories)**


## Yazılar
{% for post in site.posts %}
 <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
 <p><small><strong>{{ post.date | date: "%B %e, %Y" }} - {{ post.category }}</strong></small></p>            
{% endfor %}
