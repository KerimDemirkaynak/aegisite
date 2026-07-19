---
title: Satırları Seç
menu:
  docs:
    parent: working-with-subtitles
weight: 3600
aliases:
  - /docs/latest/Select_Lines/
---

**Satırları seç** aracı, betikte belirli kriterlerle eşleşen tüm satırları bulmak ve seçmek için kullanışlıdır. Bu araç, tüm yorum satırlarını silmekten belirli bir oyuncu tarafından söylenen tüm satırları bulmaya kadar pek çok işlem için yararlı olabilir. Araca _Altyazılar_ menüsü -> _Satırları seç_ yolundan ulaşılabilir.

![Satırları_seç](/img/3.2/Select_lines.png#center)

### Eşleşme

Bu kontroller, satırları seçmek için hangi kriterlerin kullanılacağını belirler.

Eşleşir
: Kriterlerle eşleşen tüm satırları seçer.

Eşleşmez
: Kriterlerle eşleşmeyen tüm satırları seçer.

Büyük/küçük harf duyarlı
: Büyük/küçük harf duyarlılığını kontrol eder; yani aracın büyük ve küçük harf arasındaki farkı dikkate alıp almayacağını belirler.

Tam eşleşme
: Verilen metinle _tam olarak_ eşleşen satırları bulur.

İçerir
: Verilen metni _içeren_ satırları bulur.

Düzenli ifade (Regex) eşleşmesi
: Metni bir [düzenli ifade](https://en.wikipedia.org/wiki/Regular_expression) veya "regex" olarak ele alır ve ifade eşleşirse satırı seçer. Düzenli ifadeler hakkında bir eğitim için [perlretut kılavuz sayfasını](https://perldoc.perl.org/perlretut.html) okumayı veya Google'da aramayı deneyebilirsiniz. Aegisub tarafından desteklenen tam sözdizimi referansı için [wxWidgets düzenli ifadeler referans sayfasına](https://docs.wxwidgets.org/stable/overview_resyntax.html) bakın.

### Alan içinde

Bu seçenek, yukarıda belirtilen eşleştirme için her satırın hangi alanının kullanılacağını kontrol eder. Olası alternatifler şunlardır:

Metin
: Satırın gövde metni

Stil
: Satırın stil adı

Oyuncu
: Oyuncu alanı

Efekt
: Efekt alanı

### Diyalog/yorum eşleştirme

Burada, yorum satırlarından mı, diyalog satırlarından mı yoksa her ikisinden birden mi seçim yapmak istediğinizi seçebilirsiniz.

### Eylem

Aracın, verilen kriterlerle eşleşen satırlara ne yapacağına karar verir. Aşağıdakiler arasından seçim yapabilirsiniz:

Seçimi ayarla
: Mevcut seçiminiz kaldırılır ve bunun yerine betikteki kriterlerle eşleşen tüm satırlar seçilir.

Seçime ekle
: Betikteki kriterlerle eşleşen tüm satırları mevcut seçiminize ekler.

Seçimden çıkar
: Şu anda seçili olan ve kriterlerle eşleşen tüm satırların seçimini kaldırır.

Seçimle kesiştir
: Seçimden çıkar işleminin tersini yapar. Yani, mevcut seçimde bulunan ve kriterlerle eşleşen tüm satırlar seçili kalır, ancak diğer her şeyin seçimi kaldırılır.