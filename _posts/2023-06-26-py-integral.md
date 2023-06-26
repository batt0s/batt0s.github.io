---
layout: default
category: math
tags: [math,python]
title: Python ile Belirli İntegral
---

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>


Bir keresinde C++ ile integral hesabı yapmam gerekmişti, başta çok kolay olacağını düşünmüştüm. O zamanlar daha üniversiteye başlamamıştım. Lisede integral hesaplamak için bir yöntem öğreniriz. $\int x^a dx = \frac{x^{(a+1)}}{a} + c$  Bu yöntemi kağıt üzerinde kullanabilsem de bilgisayarda yapamadım. Daha sonra araştırmalarım *Simpson Kuralı* diye bir şey gördüm ve çok üstüne araştırmadan sadece gördüğüm formülü kodlayıp geçmiştim. Şimdi Matematik ve Bilgisayar Bilimleri okuyorum ve bazı şeyler hakkında daha fazla bilgim, fikrim var. Gördüm ki Nümerik Analiz çok ilgi çekici bir konuymuş. Bu konu hakkında bildiklerim ile bir şeyler yazmaya çalıştım. Konu hakkında uzman değilim eğer yanlış gördüğünüz bir yer varsa bana eposta göndermekten çekinmeyin lütfen.


## Nümerik Analiz

### Nümerik (Sayısal) Analiz ve Amacı Nedir?

Nümerik analizin amacı çözümünü analitik yöntemlerle yapamadığımız herhangi bir matematik problemini çözmek için yöntemler/algoritmalar bulmak ve yaklaşık sonuç bulmaktır. Genelde mühendisler tarafından sürekli kullanılır. Daha fazla bilgi için [vikipedi:Sayısal Analiz](https://tr.wikipedia.org/wiki/Say%C4%B1sal_analiz) sayfasına bakabilirsiniz.

### Sayısal İntegral Hesabı

Nümerik analizin farklı hesaplamalar için farklı alt türleri var. Bu yazıda göz atacağımız tür iste *Sayısal İntegral*. Bu noktada kullanabileceğimiz birçok yöntem var; Yamuklar Yöntemi, Simpson Yöntemi, Ramberg Algoritması, Gaussion Kuadroture Yöntemi... Bu yazıda ben Simpson Yöntemine değineceğim. 

#### Simpson Yöntemi

İsmini Thomas Simpson'dan alır. Basitçe fonksiyona benzer bir veya birden fazla polinomun alanını bularak yaklaşık integral bulmayı hedefler. Örneğin $\int_{a}^{b} f(x)dx$ için $a$ ve $b$ den geçen, tepe noktası $m = (a+b)/2$ olan bir $P(x)$ polinomu bulup $\int_{a}^{b} P(x)dx$ alırsak yaklaşık olarak bir sonuç bulabiliriz. 

![Örnek Görsel (Kaynak:wiki:Simpson's rule)](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Simpsons_method_illustration.svg/220px-Simpsons_method_illustration.svg.png)

Bu eğri uydurma işlemine interpolsayon denir. Polinomlar için *Lagrange İnterpolsayon Polinomu* kullanılabilir. 

##### Lagrange İnterpolasyonu

$(x_0, f_0), (x_1, f_1), (x_2, f_2)$ gibi üç noktadan $f(x) = a_0 + a_1 x + a_2 x^2$ polinomunun geçtiğini düşünelim. 
$$L_0 = \frac{(x-x_1)(x-x_2)}{(x_0-x_1)(x_0-x_2)}, L_1 = \frac{(x-x_0)(x-x_2)}{(x_1-x_0)(x_1-x_2)}, L_2 = \frac{(x-x_0)(x-x_1)}{(x_2-x_0)(x_2-x_1)}$$
olmak üzere $f(x) = L_0f_0 + L_1f_1 + L_2f_2$ dir. Daha genel bir tanım ve interpolasyonlar hakkında daha detaylı bilgiler için kaynaklara göz atabilirsiniz. 

##### Simpson's 1/3 rule

Simpson yönteminde $n$ farklı parçaya ayırabilirsiniz, benim kullanacağım yöntem 2'ye ayırmak ve bir 2. dereceden polinom oluşturmak olacak. Bunun özel adı Simpson'un 1/3 kuralı veya Simpson'un 1. kuralıdır. 

Lagrange interpolasyonu ile bir polinom oluşturalım. Yukarıdaki görseli hatırlayın. $a,b$ ve $m$. 

$$P(x)dx = f(a)\frac{(x-m)(x-b)}{(a-m)(a-b)} + f(m)\frac{(x-a)(x-b)}{(m-a)(m-b)} + f(b)\frac{(x-a)(x-m)}{(b-a)(b-m)}$$
olur. İki tarafında integralini alıp düzenlersek şu ifadenin doğruluğunu gösterebiliriz:
$$\int_a^b P(x)dx = \frac{b-a}{6}[f(a)+4f(\frac{a+b}{2})+f(b)]$$
Artık elimizde bir formül olduğuna göre bunu kodlayabiliriz.

```python
# main.py
def simpson(f, x_0, x_2):
    h = (x_2 - x_0)/2
    x_1 = (x_2 + x_0)/2
    area = (h/3)*(f(x_0) + 4*f(x_1) + f(x_2))
    return area
```

Şimdi python da bu fonksiyon aracılığıyla integral hesaplayabiliriz. Örnek olarak $\int_0^2 x^2 dx$ i çözelim. 

```python
>>> from main import simpson
>>> def f(x):
...     return x*x
... 
>>> simpson(f, 0, 2)
2.6666666666666665
```

Gerçekten de sonuç olarak $\frac{8}{3}$ yani $2.6666$ verdiğini görebiliriz.

Merak edenler için formülü elde etmenin başka bir yöntemi daha var. *Taylor Teoremi* kullanabiliriz. 

<details>
<summary>Görüntülemek için tıklayın</summary>


##### Simpson Yöntemi 

Merak edenler için formülü elde etmenin başka bir yöntemini daha yazmak istiyorum. Bu sefer *Taylor Teoremi* kullanacağım. 

$f \in c^{n+1}[a,b]$ olsun. Yani $f$ fonksiyonu $[a,b]$ aralığı üzerinde $1., 2., ..., (n+1).$ mertebeden sürekli türeve sahip olsun. Ayrıca $x_0 \in [a,b]$ olsun. Bu durumda $\forall x \in [a,b]$ için 
$$f(x) = f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+...+\frac{f^n(x_0)}{n!}(x-x_0)^n+\frac{f^{n+1}(x_0)}{(n+1)!}c(x)(x-x_0)^{n+1}$$

Şimdi tekrardan $\int_a^b f(x)dx$ integralini düşünelim. $f$ fonksiyonunun dördüncü mertebeden sürekli türeve sahip olduğunu var sayalım. $[a,b]$ aralığını eşit uzunluklu iki alt aralığa bölelim. Bu durumda $x_0=a, x_1=x_0+h,x_2=b$ olur. $f$ fonksiyonunu $x_1$ civarında Taylor Serisine açarsak:

$$\int_{x_0}^{x_2} f(x)dx =\int_{x_0}^{x_2} f(x_1)dx + \int_{x_0}^{x_2}  f'(x_1)(x-x_1)dx  + \int_{x_0}^{x_2}  \frac{f''(x_1)(x-x_1)^2}{2}dx  
	+ \int_{x_0}^{x_2}  \frac{f'''(x_1)(x-x_1)^3}{3!}dx 	+ \int_{x_0}^{x_2}  \frac{f^{4}(c)(x-x_1)^4}{4!}dx $$

$$\int_{x_0}^{x_2} f(x)dx = f(x_1)x |_{x_0}^{x_2} + \frac{f'(x_1)}{2}(x-x_1)^2  |_{x_0}^{x_2} + \frac{f''(x_1)}{6}(x-x_1)^3 |_{x_0}^{x_2} + \frac{f'''(x_1)}{24}(x-x_1)^4  |_{x_0}^{x_2}
	 + \frac{f^{(4)}(c)}{120}(x-x_1)^5  |_{x_0}^{x_2}$$

$$= f(x_1)2h + 0 +\frac{f''(x_1)(h^3)}{3} + 0 + \frac{f^{(4)}h^5}{60}$$
$$f(x_1)2h + \frac{h^3}{3} (\frac{f(x_0) - 2f(x_1) + f(x_2)}{h^2} - \frac{f^{(4)}(c(x))h^2}{12}) + \frac{f^{(4)}h^5}{60}$$
$$\frac{h}{3}(f(x_0) - 4f(x_1) + f(x_2)) - \frac{h^5}{90}f^{(4)}(c)$$
Hata terimini ihmal edersek
$$\int_{x_0}^{x_2} f(x)dx = \frac{h}{3}(f(x_0) + 4f(x_1) + f(x_2))$$

Yine aynı formülü elde edebiliriz. 

İnterpolasyon ile yaptığımı mantıksal olarak kavramak daha kolay ama matematik olarak formülü elde etmek daha zor, Taylor Teoreminde ise formülü elde etmek daha kolay ama mantık olarak kavramak zor geldi bana. Sonuç olarak ikisini de yazmak istedim.

</details>

---

**Kaynakça**

[Vikipedi:Sayısal Analiz](https://tr.wikipedia.org/wiki/Say%C4%B1sal_analiz) \
[Wikipedia:Simpson's rule](https://en.wikipedia.org/wiki/Simpson's_rule) \
[Wikipedia:Lagrange polynomial](https://en.wikipedia.org/wiki/Lagrange_polynomial) \
[numerikanaliz.com:Nümerik Analiz Nedir?](https://numerikanaliz.com/numerik-analiz-nedir/) \
[itu.edu.tr:Eğri uydurma ve İnterpolasyon](https://web.itu.edu.tr/yukselen/HM504/02-%20E%F0ri%20uydurma%20ve%20interpolasyon.pdf) \
[KBUZEM:Sayısal Analiz 11. Hafta İnterpolasyon](https://web.karabuk.edu.tr/yasinortakci/dokumanlar/say%C4%B1sal_analiz/turkce/11.pdf) \
[KBUZEM:Sayısal Analiz 14. Hafta Sayısal Türev ve İntegral](https://web.karabuk.edu.tr/yasinortakci/dokumanlar/say%C4%B1sal_analiz/turkce/14.pdf)

---

Kerem Ü. \
kerem.ullen@proton.me
