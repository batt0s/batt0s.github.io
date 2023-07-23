---
layout: default
category: software
tags: [python]
title: Python Method Çeşitleri - @staticmethod ve @classmethod nedir?
---
# Python Method Çeşitleri - @staticmethod ve @classmethod nedir?

Geçen gün githubda bazı Django projelerinin kodlarını okurken `@classmethod` diye bir şey gördüm ve araştırdım. 

`@staticmethod` ve `@classmethod` dekoratörleri sınıflar içinde özel metodlar oluşturmak için kullanılır. 

## `@staticmethod`
`@staticmethod` dekoratörü metod tanımlarken metodun sınıftan bir bilgiye ihtiyaç duymadığı durumlarda kullanılır. 

```python
class MyClass:
	@staticmethod
	def add(x, y):
		return x + y

result = MyClass.add(1, 2) # 3
```

Böylece bir instance tanımlamanıza gerek kalmaz. Kullanışlı olduğu durumlar olsa da genelde ihtiyaç olmaz. Mesela bu örnekte `add()` metodunu class dışında bir fonksiyon olarak da yazabilirdik.

## `@classmethod`
`@classmethod` dekoratörü metod tanımlanırken genelde constructor metodu tanımlarken kullanılır. İçerisine self verilmez, cls verilir. Açıkçası tam olarak nasıl tanımlayacağımı bilmiyorum o yüzden örnek vereyim.

```python
class MyClass:
	@classmethod
	def __init__(self, name):
		self.name = name
	def new(cls, name):
		return cls(name)

myclass = MyClass.new("deneme")
```

Burada kullanılan `cls` o sınıfın adı yerine geçer, yani bu durumda `cls(name)` = `MyClass(name)`. Eğer bu class'ı inherit ederseniz alt classın adı çağırılır.

 `new()` metodunun içerisi bu kadar basit olmayabilir daha uzun olabilir.

Diyebilirsiniz ki neden `__init__` varken ayrıca yapıcı metod tanımlayayım. Aynı soruyu ChatGPT ye sordum bana bazı senaryolar söyledi.

Örneğin farklı yapıcılar oluşturabiliriz:
```python
class Rectangle: # Dikdörtgen
	def __init__(self, width, height): # Genişlik ve Yükseklik alıyor
		self.width = width
		self.height height
	
	@classmethod
	def create_square(cls, side_length): # Kare oluştur, sadece bir uzunluk alıyor çünkü karenin genişliği ve yüksekliği aynıdır
		return cls(side_length, side_length)

square = Rectangle.create_square(2)
print(square.width, square.length) # 2 2
```

Ya da farbrika metodları:
```python
class Vehicle: # Araç
    def __init__(self, brand, model): # Marka ve Model alıyor
        self.brand = brand
        self.model = model

    @classmethod
    def create_car(cls, model): # Araba oluştur, sadece model alıyor, marka otomatik olarak toyota
        return cls("Toyota", model)

    @classmethod
    def create_bike(cls, model): # Motor oluştur, sadece model alıyor, marka otomatik olarak honda
        return cls("Honda", model)

car = Vehicle.create_car("Corolla")
bike = Vehicle.create_bike("CBR250R")

print(car.brand, car.model)  #  Toyota Corolla
print(bike.brand, bike.model)  #  Honda CBR250R
```

Birkaç örnek daha verdi ama bana bunlar olabilirmiş gibi geldi. 

Umarım anlatabilmişimdir. 

---

Kerem Üllenoğlu <br>
kerem.ullen@proton.me
