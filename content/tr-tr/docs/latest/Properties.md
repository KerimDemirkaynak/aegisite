---
title: Betik Özellikleri
menu:
  docs:
    parent: miscellaneous
weight: 7300
aliases:
  - /docs/latest/Properties/
---

**Betik özellikleri**, tüm betiği çeşitli şekillerde etkileyen bazı üstbilgiler ve diğer seçeneklerdir. Bunlara _Dosya menüsü_ -> _Özellikler_ kısmından erişilebilir.

![Özellikler](/img/3.2/Properties.png#center)

Özellikler şunlardır:

- **Başlık**, **Orijinal betik**, **Çeviri**, **Düzenleme**, **Zamanlama**, **Senkronizasyon noktası**, **Güncelleyen** ve **Güncelleme detayları** - Bunlar yalnızca bilgilendirme amaçlıdır ve oluşturmayı (render) hiçbir şekilde etkilemezler. Yararlı bulursanız bunları uygun değerlere ayarlayın.

- **Çözünürlük**, **YCbCr Matrisi**, **Kenarlık ve gölge ölçeklendirme** - Bu alanların anlamı için [Betik Çözünürlüğü]({{< relref "Script_Resolution" >}}) sayfasına bakın.

- **Satır kaydırma stili** - Altyazı oluşturucunun, tek bir satıra sığmayacak kadar uzun olan satırları nasıl böleceğini kontrol eder. Modlar şunlardır:

  - 0 - Varsayılan mod. "Akıllı" kaydırma; eğer bir satır kendi başına sığmayacak kadar uzunsa, onu yaklaşık olarak eşit uzunlukta iki satıra böler, ancak üst satırın daha geniş olmasını tercih eder. Manuel satır sonu eklemek için `\N` (büyük N harfine dikkat) kullanılabilir.
  - 1 - Satır çerçevenin kenarlarına ulaştığında (kenar boşlukları hariç) bir satır sonu ekler; yani eğer satıra tek bir kelime fazla geliyorsa, alt satırda sadece o son kelime kalır. Neredeyse hiçbir zaman kullanışlı değildir. 0 modunda olduğu gibi, manuel satır sonları için `\N` kullanılabilir.
  - 2 - Otomatik satır kaydırma yapılmaz; eğer bir satır video çerçevesine sığmayacak kadar uzunsa, çerçeveden dışarı taşmaya devam eder. Manuel satır sonları eklemek için `\n` ve `\N` kullanılabilir.
  - 3 - 0 modu ile aynıdır, ancak alt satırın daha geniş olmasını tercih eder. Uzun süre boyunca VSFilter'ın bu moddaki uygulamasının hatalı olduğunu ve bazen fazladan boş satırlar eklediğini veya tek kelimelik satırlar oluşturduğunu unutmayın.

Kaydırma modu neredeyse her zaman sıfır olmalıdır.
İki numaralı mod, bazen kaydırılan veya manuel olarak satır sonları eklenen uzun satırlar için kullanışlıdır, ancak bu satır bazında [\\q]({{< relref "ASS_Tags#\\q" >}}) etiketi ile ayarlanmalıdır.