---
title: Ek Yöneticisi
menu:
  docs:
    parent: miscellaneous
weight: 7500
aliases:
  - /docs/latest/Attachment_Manager/
---

Ek yöneticisi, yazı tiplerini ve/veya resimleri betiğinize (metin olarak kodlayarak) eklemenizi sağlar. Bu, yazı tiplerini ayrı dosyalar olarak göndermek zorunda kalmadan bir betik üzerinde çalışan herkesle paylaşmak için bazen yararlıdır. Ancak oldukça sınırlıdır ve sorunlara yol açmaya meyillidir.

## Genel Bakış

![Ek_listesi](/img/3.2/Attachment_list.png#center)

Tüm diyalog oldukça açıklayıcıdır. "Ekle..." (Attach ...) butonları ek ekler, "Çıkart" (Extract) mevcut ekleri ayrı dosyalara çıkartır ve "Sil" (Delete) ekleri altyazı dosyasından siler.

## Sınırlamalar ve dezavantajlar

### Desteklenen formatlar

SSA formatı özellikleri, yalnızca belirli dosya türlerinin eklenmesine izin verir. Yazı tipleri için sadece .ttf formatına izin verilir. Resimler için .bmp, .gif, .ico, .jpg ve .wmf formatlarına izin verilir (.png eksikliğine dikkat edin). Resimleri *kullanan* hiçbir SSA komutu, SubStation Alpha dışında hiçbir programda uygulanmamıştır, bu nedenle resim eklemenin aslında yararlı bir şey olması pek olası değildir.

### Uyumluluk sorunları

Pek çok SSA/ASS düzenleyicisi ekleri görmezden gelir veya kaldırır. Orijinal SubStation Alpha (v4.08) düzgün çalışacaktır, ancak sadece gerçek SSA dosyaları için. Sabbu, tanınmayan alanlar hakkında şikayet edecek ve dosyayı kaydederseniz ekleri kaldıracaktır. Diğer düzenleyicilerin çoğu ya ekleri görmezden gelir ya da onlarla karşılaştığında çöker.

Dikkate değer bir istisna, birleştirme (muxing) sırasında ekli dosyaları Matroska eklerine dönüştürecek olan mkvmerge'dir. Betiği tekrar ayırırsanız (demux), ekler betikten kaldırılır ancak bunlar MKV ekleri olarak orada kalmaya devam eder.

### Boyut

Ne yazık ki, ikili verileri metin olarak depolamak (bu durumda, UUEncoding'in bir varyantı) çok verimli değildir. Ekli dosyalar, betik eki olarak ayrı dosya hallerinden önemli ölçüde daha fazla yer kaplayacaktır.

### Hız

Aegisub'ın geri alma sistemi, her değişiklikte yüklenen dosyanın tam bir kopyasını oluşturur. Normalde bu çok hızlıdır ancak ekler, büyük boyutları nedeniyle bu işlemi önemli ölçüde yavaşlatabilir.