---
title: SSS
menu:
  docs:
    parent: introduction
weight: 2600
aliases:
  - /docs/latest/FAQ/
---

Aegisub hakkında Sıkça Sorulan Soruların küçük bir derlemesi - çoğunlukla başka hiçbir yere uymayan konular.

### Karaoke efektleri?

[Karaoke Şablonlayıcı eğitimlerine]({{< relref "Automation/Karaoke_Templater/Tutorial_1" >}}) bakın.

### Aegisub ile DVD altyazıları oluşturabilir miyim?

Doğrudan değil, ancak SSA dosyalarını VOBSub'a dönüştürebilen [MaestroSBT](https://sourceforge.net/projects/maestrosbt/) adında şık bir program var. Hangi etiketlerin ve diğer şeylerin kullanılabileceği konusunda oldukça fazla kısıtlaması vardır, bu nedenle önce kılavuzunu okumanız önerilir. Ayrıca ASS kabul etmediğini, sadece SSA kabul ettiğini unutmayın. Gerçek SSA dosyalarını kaydetmek için Aegisub'ın Dosya -> Dışa Aktar... iletişim kutusunu kullanabilirsiniz.

### Aegisub SRT formatında kaydetmeye izin veriyor mu?

Evet, ancak sadece hiçbir bilginin kaybolmayacağı durumlarda. Başka bir deyişle, `\1c`, `\b` veya `\i` dışındaki geçersiz kılma (override) etiketleriniz varsa, Aegisub doğrudan SRT olarak kaydetmeye izin vermeyecektir. Ancak, Dosya -> Dışa Aktar... iletişim kutusunu kullanarak yine de SRT olarak dışa aktarabilirsiniz. Sadece tüm onay kutularının işaretini kaldırın (betik bilgisini temizle, VFR dönüştürme vb.).

### Bir hata buldum!?

[Hata takip sisteminde](https://github.com/TypesettingTools/Aegisub/issues) bildirin. Lütfen raporunuza mümkün olduğunca çok ayrıntı ekleyin! Unutmayın ki bir hata hata takip sisteminde yer almıyorsa, bizim açımızdan *yok sayılır*.

### Aegisub'da neden \<X özelliği> yok? \<Y programında> var!

Büyük olasılıkla istediğinizi bilmediğimiz içindir. [Hata takip sisteminde](https://github.com/TypesettingTools/Aegisub/issues) talep edin ve ne olacağını görün.

### Daha fazla bilgiyi nerede bulabilirim ve/veya nasıl yardım alabilirim?

Aegisub ile ilgili konular için [Discord sunucusu](https://discord.gg/AZaVyPr) ve [IRC kanalı](irc://irc.rizon.net/aegisub) soru sormak için iyi yerlerdir.

Genel video ile ilgili sorular için, [Doom9.org](https://www.doom9.org) ve [forumları](https://forum.doom9.org) genellikle başvurulacak yerdir.

### Bilmem gereken herhangi bir VSFilter hatası var mı?

Tek kelimeyle: [evet](https://web.archive.org/web/20110811220802/http://asa.diac24.net/VSFilter#BUGS).