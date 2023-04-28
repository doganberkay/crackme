# CH1

### Önbakış

![](https://github.com/doganberkay/crackme/blob/main/image_2023-04-28_155159319.png?raw=true)

Kullanıcıdan girdi bekleyip aldığı girdi yanlışsa çıkış yapan bir program.


![](https://github.com/doganberkay/crackme/blob/main/image_2023-04-28_170217410.png?raw=true)

TLS Callback kullandığı görülmektedir. Böylece entrypoint öncesi kod çalıştırabilmektedir.


### Write Up


![](https://raw.githubusercontent.com/doganberkay/crackme/main/image_2023-04-25_170523320.png)

Kullanıcıdan input aldığı bu yerde aldığı her input aldığında ekrana * koyan kod bloğudur. 

Bu kod bloğu 13 ile karşılaştırma yapmaktadır. Burdan islenilen şifrenin 13 olabileceği düşünülmektedir.


Girilen inputa aynı zamanda XOR işlemi uygulanmakdatır. Bu işlemde kullandığı XOR keyi bulabiliyoruz.

Verdiğim input;
>bbbbbbbbbbbbb

Yukarda girdiğim inputu XORlayıp aşağıdaki hale getirmiştir.

>{,+*)('&%$#"! } //parantezsiz hali

XOR Key;
>"NIHKJEDGFA@CB"


![resim22112](https://raw.githubusercontent.com/doganberkay/crackme/main/image_2023-04-25_164526942.png)

```
add edx, FFFFF 
add ecs, eax
cmp edx, CFFF3
```

Kodun farklı yerlerinde CFFF3 ile karşılaştırma işlemi yapılıyor. Öncesinde yaptığı edx'e FFFF eklemesiyle bu döngüye sadece 13 kere girdiğini görebiliyoruz. Daha önce ön gördüğümüz gibi istenilen şifre 13 basamaklıdır.

![](https://github.com/doganberkay/crackme/blob/main/image_2023-04-25_170950755.png?raw=true)

En üstte gözüken döngüye baktığımız zaman yine CFFF3 olana kadar FFFF toplama işlemi yapıyor. 13 kere girdiği döngüde sırayla eax üzerinden karakterler göstermektedir.

![](https://github.com/doganberkay/crackme/blob/main/image_2023-04-28_174251227.png?raw=true)

>1E 16 0A 02 1E 1A 0C 06 14 05 05 11 7D


Bu çıkan karakterleri daha önce bulduğumuz XOR keyi ile XORlama işlemi yaptığımız zaman ise şifreyi bulmuş oluyoruz.

>P_BIT_HARDER?


![](https://github.com/doganberkay/crackme/blob/main/image_2023-04-28_175708779.png?raw=true)

Bulduğumuz şifrenin doğru olduğunuda deneyerek görebiliyoruz.