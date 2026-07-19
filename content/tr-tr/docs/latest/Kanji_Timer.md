---
title: Kanji Zamanlayıcı
menu:
  docs:
    parent: timing
weight: 5400
aliases:
  - /docs/latest/Kanji_Timer/
---

Kanji zamanlayıcı, zamanlanmış karaoke satırlarından oluşan bir setten, henüz zamanlanmamış başka bir satır setine karaoke zamanlamalarını kopyalamayı kolaylaştırır. Esas olarak Japonca şarkılara karaoke eklemek için tasarlanmıştır.

## Başlamadan önce

Kanji zamanlayıcı, belirli bir stile sahip (zamanlanmış) bir girdi satırındaki heceleri, başka bir stile sahip (zamanlanmamış) karşılık gelen satırdaki hecelerle eşleştirmeye çalışır. Başka bir deyişle, zamanlanmış girdi satırlarının tümü aynı stile ("romaji" gibi) ve zamanlanmamış olanların ise başka bir stile ("kanji" gibi) sahip olmalıdır. Zamanlanmış kaynak satırlarının zamanlanmamış hedef satırlarından daha fazla olması veya tam tersi durumu aracı karıştırabilir, ancak genellikle bu durumu düzeltmek mümkündür (aşağıya bakınız). Kaynak satırları hedef satırlarla doğru bir şekilde eşleştirmek için, her iki setin de ızgara (grid) içinde aynı sırada olması gerekir. Örneğin, bu çalışır:

```plaintext
Zamanlanmış satır 1
Zamanlanmamış satır 1
Zamanlanmış satır 2
Zamanlanmamış satır 2
```

Bu da çalışır:

```plaintext
Zamanlanmış satır 1
Zamanlanmış satır 2
Zamanlanmamış satır 1
Zamanlanmamış satır 2
```

Ancak bu **çalışmaz** (satırları yanlış eşleştirir):

```plaintext
Zamanlanmış satır 1
Zamanlanmış satır 2
Zamanlanmamış satır 2
Zamanlanmamış satır 1
```

## Kanji zamanlayıcıyı kullanma

Kanji zamanlayıcı iletişim kutusu şöyledir:

![Kanji zamanlayıcı](/img/3.2/Kanji_timer.png#center)

Yapmanız gereken ilk şey, zamanlanmış girdi satırları ve zamanlanmamış çıktı satırları için hangi stillerin kullanıldığını seçmektir. Bu işlem iletişim kutusunun sağ üst köşesinde yapılır; üstteki açılır menü kaynak stili, alttaki ise hedef stildir. Bunu yaptıktan sonra başlat düğmesine tıklayın.

Şimdi, ilk kaynak satırının ilk hecesinin kaynak metin alanında vurgulandığını ve hedef alanında önerilen hedef hecenin vurgulandığını göreceksiniz. Şimdi yapmanız gereken, her bir kaynak heceyi hedefteki bir veya daha fazla kanji (veya diğer hecelerle) "gruplandırmaktır". Bu işlem aşağıdaki klavye kısayolları kullanılarak yapılır:

Enter
: Vurgulanan gruplandırmayı kabul et (ve tüm heceler gruplandırılmışsa bir sonraki satıra geç).

Sağ ok
: Hedef vurgu uzunluğunu artır.

Sol ok
: Hedef vurgu uzunluğunu azalt.

Yukarı ok
: Kaynak vurgu uzunluğunu artır.

Aşağı ok
: Kaynak vurgu uzunluğunu azalt.

Backspace (Geri al)
: Kabul edilen son hecenin gruplandırmasını kaldırır (veya bağlantısını keser) ve tekrar gruplandırmayı denemenize izin verir (hata yaparsanız kullanışlıdır).

## Dikkat edilmesi gerekenler

- Vurguları değiştirmek için fareyi kullanmayın; bu, aracı oldukça karıştırır. Bunun yerine klavye kısayollarını kullanın, çok daha hızlıdırlar.
- Hedef satır zaten karaoke zamanlamalı olabilir, ancak eğer öyleyse, kanji zamanlayıcı bu zamanlamaların üzerine yazacaktır.
- Boş heceler tek başlarına kopyalanacak veya çevrelerindeki hecelerle birleştirilecekse onlarla birleştirilecektir.
- Her \\k etiketinden önce gelen tüm ASS geçersiz kılma etiketleri (override tags) doğrudan, değiştirilmeden kopyalanacaktır, ancak \\k etiketinden sonraki etiketler şu an için hiç kopyalanmamaktadır.
- Kaynak satırlarınız hedef satırlarınızdan fazlaysa veya tam tersi bir durum varsa, kaynak ve hedef satır eşleşmesinin doğru yapıldığından emin olmak için "Kaynağı atla" veya "Hedefi atla" seçeneklerini kullanabilirsiniz.