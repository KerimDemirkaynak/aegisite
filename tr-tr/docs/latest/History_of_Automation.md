---
title: Otomasyonun Tarihçesi
menu:
  docs:
    parent: automation
weight: 6600
aliases:
  - /docs/latest/Sidebar/History_of_Automation/
---

Aegisub'daki Otomasyon sistemi, temel karaoke efektleri oluşturmaya yarayan çok basit ve neredeyse kullanışsız bağımsız bir sistemden, oldukça güçlü bir genişletme mekanizmasına dönüşmüştür. İşte sistemlerin ana yazarı tarafından kaleme alınan, geçmişine dair kısa bir özet.

## Otomasyon 1, aslında sadece Karaoke Efektörü

![Efektör_ekran_görüntüsü](/img/3.2/Effector_screenshot.png)

_Karaoke Efektörü_ programı, başlangıçta daha sonra rafa kaldırılan küçük bir çeviri projesi için karaoke efektleri yapmak amacıyla oluşturulmuştu. Borland Delphi ile yazılmıştı ve betik oluşturmak için Lua 5.0 kullanıyordu. Lua'nın bu kullanımı, bugün ona "Otomasyon 1" dememin temel nedenidir. Temelde, Otomasyon 3'teki _simple-k-replacer_ betiğinin yaptığına benzer ancak daha karmaşık ve kullanımı o kadar da kolay olmayan efektlerin oluşturulmasına izin veriyordu.

Eğer müzeden kalma bu kalıntıyı denemek isterseniz, buradan indirebilirsiniz: <https://www.animereactor.dk/aegisub/effector.rar>

## Otomasyon 2, gerçekleşmeyen Python motoru

Otomasyon 2, Aegisub'daki betik sistemi olması amaçlanmıştı; teknik özelliklerini Aegisub henüz sadece dahili ön-alfa geliştirme aşamasındayken taslak haline getirmiştim. Betik dili olarak Python'ı kullanması ve oldukça esnek olması planlanmıştı. Ancak genel olarak kötü bir tasarım olduğu ortaya çıktı (ki geriye dönüp bakıldığında bu iyi bir şey olabilir) ve hiçbir zaman uygulanmadı. Bunun yerine tekrar Lua'yı incelemeye başladım ve Otomasyon 3 olacak sistemin taslağını hazırladım.

Şu anda Otomasyon 2 üzerindeki çalışmalara dair pek bir kanıt kaldığını sanmıyorum. Hakkında söylenebilecek en önemli şey, mevcut Otomasyon 4'ün, Otomasyon 2'nin amaçladığı her şeyi ve hatta daha fazlasını başarmış olmasıdır.

## Otomasyon 3, Lua'ya dönüş ve kullanılabilir bir şeyler

Otomasyon 2 ve Python fiyaskosundan sonra tekrar "diller arasında gezintiye" çıktım ve sonunda yine Lua'ya döndüm, ayrıca çok daha az iddialı bir tasarıma yöneldim. Bunun işe yaradığı kanıtlandı ve sistem, Otomasyon 3 olarak sonuçlandı. Başlangıçta Otomasyon 3'ün de bir şekilde genişletilebilir olması ve ileride sadece altyazı satırlarının temel olarak değiştirilmesinden daha fazlasını desteklemesi amaçlanmıştı; bu durum, tüm Otomasyon 3 betiklerinde gerekli olan _kind="basic_ass"_ ifadesinden açıkça anlaşılmaktadır. Ne yazık ki, Otomasyon 3'ün genel mimarisi sonunda hiçbir şekilde genişletilmesine izin vermedi ve Otomasyon 4 için ilk kaba fikirler oluşmaya başladı.

Sonuç olarak Otomasyon 3 çok başarılı olduğunu kanıtladı ve harika bir iş çıkardı.

## Otomasyon 4, sınırsız özellik çalışmaları?

![Merhaba-auto4](/img/3.2/Hello-auto4.png)

Otomasyon 3'ün kusurları ortaya çıkmaya başladığında Otomasyon 4'ün tasarımı başladı. Birçok insan diğer diller için, özellikle Perl ve Python için talepte bulunuyordu, bu yüzden birden fazla betik dili desteği temel tasarıma dahil edildi. Otomasyon 4'ün geliştirilmesi oldukça kesintili ilerledi, bazen aylarca durakladı. Başlangıçta Aegisub 1.09 için planlanmıştı, sonra 1.10'a, ardından nihayet 1.11'e ertelendi; bu sürümdeki yeni özellikler ve köklü tasarımlar nedeniyle Aegisub 2'ye dönüştü ve Otomasyon 4 bunlardan biriydi.

Mayıs 2006'nın ortalarında, _hello-auto4.png_ dosyasının zaman damgasına güvenecek olursam, Otomasyon 4/Lua nihayet "çalışır" durumdaydı ancak bir yıldan fazla zaman geçtikten sonra gerçekten kullanışlı hale geldi. Bu da benim tembelliğimin bir kanıtı.

> _- Niels Martin Hansen, 2 Temmuz 2007_