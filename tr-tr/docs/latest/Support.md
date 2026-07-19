---
title: Aegisub'ı Destekleyin
menu:
  docs:
    parent: introduction
weight: 2500
aliases:
  - /docs/latest/Support/
---

Aegisub'ı desteklemek ister misiniz? Bu çok kolay!

### Geri Bildirim

Bize geri bildirimde bulunabilirsiniz - yorumlar, eleştiriler, öneriler vb. Hata raporları ve özellik talepleri her zaman memnuniyetle karşılanır. [Discord sunucumuza](https://discord.gg/AZaVyPr) ve [hata takip sistemimize](https://github.com/TypesettingTools/Aegisub/issues) göz atın veya [IRC kanalımızda](irc://irc.rizon.net/aegisub) sohbet etmek için uğrayın.

### Duyurma

Aegisub'ı beğendiniz mi? Arkadaşlarınıza ondan bahsedin! Aegisub'ın piyasadaki en iyi altyazı düzenleyicisi olmasına yardımcı olmanın iyi bir yolu da adını duyurmaktır.

### Bağış Yapma

Cömert mi hissediyorsunuz? Bize bağış yapmayı düşünün! Biliyorsunuz ki bu işi boş zamanlarımızda yapıyoruz.

### Programlama

> "Yeterli göz sayısı sağlandığında, tüm hatalar yüzeyseldir."

_-- Linus Torvalds_

Gerçekten yardım etmek mi istiyorsunuz, yoksa sadece bağışlamak istediğiniz bazı kodlarınız mı var? Kaynak ağacındaki readme.txt dosyasından bazı tavsiyeler:

İlk olarak, kodların bir kısmı oldukça okunabilir, bir kısmı idare eder ve bazıları ise yamalanmış çöplerden ibarettir. Bol şans. ;)

Yeni bir özellik kodlamaya başlamadan önce, bunun Aegisub'ın sahip olması gereken bir özellik olduğu konusunda hemfikir olduğumuzu doğrulamak için muhtemelen IRC'ye uğrayıp bir geliştiriciye danışmalısınız, aksi takdirde emeğinizi boşa harcama riskiyle karşı karşıya kalırsınız. Yine de talep edilmemiş hata düzeltmeleri genellikle memnuniyetle karşılanır.

İkinci olarak, Aegisub için herhangi bir kod yazmak istiyorsanız, şu koşulları kabul etmeniz gerekir:

1. Yamayı kamu malı (public domain) olarak yayınlayacak veya telif hakkını geliştiricilerden birine devredeceksiniz. Bu, bir kaynak dosyasının çok fazla kişiye ait olmasını önlemek içindir. (İstisna: BÜYÜK değişiklikler kendi adınız altında BSD lisansı ile kabul edilebilir. Geliştiricilere danışın)
1. Geliştiricilere göndermeden önce derlendiğinden ve düzgün çalıştığından EMİN olun.
1. Yamalar, master dalında olmayıp kararlı (stable) sürümde mevcut olan bir hata için olmadığı sürece, normalde git master dalına karşı olmalıdır.
1. Çekme istekleri (pull request) git master (veya uygunsa stable) üzerine rebase edilmelidir ve her çekme isteği için bir konu dalınız (topic branch) olmalıdır. Lütfen geçmişinizde herhangi bir birleştirme taahhüdü (merge commit) bulundurmayın.
1. Aegisub'ın tek bir birleşik kodlama stili yoktur, ancak programın herhangi bir yerinde zaten mevcut olan bir stili (ve tercihen dokunduğunuz kodun stilini) takip etmeye çalışın.

Üçüncü olarak, bunların tümü BSD lisansı altında mevcuttur. GNU'nun kendisine göre, BSD GPL uyumludur; yani GPL kodunu BSD koduna bağlayabilirsiniz. Ancak, bir kaynak dosyasının karışık BSD ve GPL içeriğine sahip olması durumunda, GPL kurallarına tabi olacağını unutmayın.