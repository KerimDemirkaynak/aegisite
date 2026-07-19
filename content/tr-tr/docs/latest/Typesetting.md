---
title: Dizgiye Giriş
menu:
  docs:
    parent: typesetting
    name: Dizgiye Giriş
weight: 4000
aliases:
  - /docs/latest/Typesetting/
---

Wikipedia'nın [dizgi](https://en.wikipedia.org/wiki/Typesetting) tanımı şöyledir: "**Dizgi**, metin materyalinin kağıt veya başka bir ortamda grafik formunda sunulmasını içerir." Altyazı bağlamında bu üç anlama gelir:

- Konuşulan diyalogların (çevirisinin) izleyiciye kolay okunabilir ve görsel olarak hoş bir biçimde sunulması.
- Yabancı dildeki arka plan metinlerinin (bölüm başlıkları, zaman/mekan gibi sahne bilgileri ve arka plandaki nesnelerin üzerindeki olay örgüsü için önemli diğer yazılar) çevrilmesi ve bu çevirinin, tercihen orijinali oradaymış gibi görünecek şekilde (ancak okunabilirliği koruyarak) izleyiciye sunulması.
- Videoda gösterilmesi gereken diğer metinlerin (logolar, karaoke vb.) tasarlanması.

Özellikle fansub topluluğunda "dizgi" (typesetting) kelimesi genellikle bu üç maddeden ikincisini veya üçüncüsünü ifade eder.

Bu sayfa, altyazı dizgisine bir giriş yapmaya çalışacaktır. Ne yazık ki iyi zevk öğretilmesi zor bir şeydir, ancak elimizden gelenin en iyisini yapacağız.

## Diyalog dizgisi

Diyalog dizgisinin ana hedefi **okunabilirliktir**; geri kalan her şey işin süsüdür. İzleyici okuyamıyorsa altyazıların olmasının bir anlamı yoktur. Altyazıların genellikle çok hızlı okunması gerektiğini unutmayın, bu nedenle kolay algılanabilirlik hayati önem taşır. İyi bir okunabilirlik için bazı kılavuzlar:

- Sade, karmaşık olmayan, ciddi bir yazı tipi kullanın. Sans-serif fontlar (eğer serif konusunda ısrarcıysanız "slab serif" fontlar) genellikle tercih edilir, özellikle düşük video çözünürlüklerinde, çünkü serifler bulanıklaşma eğilimindedir ve bu da doğal olarak kötü görünür. Çok ince yazı tiplerinden de kaçınılmalıdır. Küçük büyük harf (small caps) fontları kötüdür çünkü harflerin üst ve alt uzantıları kelimelerin tanınmasına yardımcı olur. Helvetica, Arial veya Verdana gibi denenmiş ve güvenilir yazı tiplerini kullanmak kötü bir fikir değildir; daha az "sıkıcı" ama yine de okunabilir bir şey istiyorsanız, Calibri gibi "hümanist" tarzda bir sans-serif yazı tipi deneyin.
- İyi tanımlanmış ancak çok kalın olmayan bir kenarlık kullanın. Renk önemlidir; ana renkle kontrast ne kadar yüksek olursa o kadar iyidir. Beyaz ana renk/siyah kenarlık kombinasyonu denenmiş ve güvenilirdir. Gölge isteğe bağlıdır; kullanacaksanız yarı saydam siyah olarak ayarlamayı düşünün; tam siyah, okunabilirliği azaltma eğilimindedir.
- Rahat kenar boşluklarına sahip büyük, dostane harfler kullanın; genellikle altyazıların, özellikle TV ekranında (TV'de izleme mesafesi genellikle bilgisayar ekranı için 0.3-0.6m iken 2-3 metredir) kolayca okunabilmesi için düşündüğünüzden daha büyük olmaları gerekir. Altyazılarınızı TV'de göstermeyi planlıyorsanız, [overscan](https://en.wikipedia.org/wiki/Overscan) (ekran taşma payı) konusunu da hesaba katmalısınız; Aegisub'ın bu konuda size yardımcı olabilecek bir overscan maskesi özelliği (bkz. [video ile çalışma]({{< relref "Video" >}})) vardır. Nihai sonuç bir TV'de izlenmeyecek olsa bile, overscan alanındaki altyazılar genellikle pek okunabilir değildir. Ayrıca videonun en-boy oranını da göz önünde bulundurun; 16:9 veya daha geniş en-boy oranları, dikey alandan ödün vererek daha uzun satırlara sahip olma fırsatı sunar.
- Aynı anda ikiden fazla metin satırının görünür olmadığından emin olun (aynı anda çok fazla kişinin konuştuğu durumlarda istisnalar yapılabilir). Bazen metni içine sığdırmak için yatay olarak biraz sıkıştırabilirsiniz; bazen de metin bloğunu iki farklı satıra bölüp birini diğerinden sonra göstermeniz gerekir.

{{<todo>}}örnekler {{</todo>}}

## "Tabela" dizgisi

Tabela dizgisi (çeşitli arka plan metinlerini çevirme) genellikle ASS ile gerçekleştirilebilir, ancak daha karmaşık efektler için bazen Adobe AfterEffects gibi ticari programlar kullanılır; çünkü tabela dizgisinin kutsal kasesi, altyazıyı sanki görüntüde her zaman varmış gibi göstermektir. Buraya nasıl ulaşılacağı bu sayfada detaylı olarak tartışılmayacaktır ancak işte bazı ipuçları:

- Tabela olay örgüsü için gerçekten önemli mi? Ekranda görünen her metni çevirmeye çalışmak sizi hızla çıldırtacaktır ve sonuç genellikle zaten okunamaz olacaktır.
- Çoğu zaman, olay örgüsü için önemli bir tabelanın (örneğin bir mektup) metni aslında diyalogda sesli olarak okunur; eğer durum böyleyse, tabela dizgisini atlamayı düşünmelisiniz çünkü hem metin hem de diyalog olması izleyiciyi bilgi bombardımanına tutabilir. Sırf yapabildiğinizi göstermek için bir tabelayı dizgilememelisiniz.
- Çeviriyi kolayca okunabilir hale getirebilecek misiniz? Örneğin, içine sığdırmak için çok az alanınız varsa, çeviri notunu normal bir "üst başlık" (toptitle) olarak koymayı düşünün.

{{<todo>}}görseller {{</todo>}}

## Daha fazla okuma

[Tipografi](https://en.wikipedia.org/wiki/Typography) hakkındaki Wikipedia sayfası, birçok yararlı bağlantıya ve çeşitli dizgi ile ilgili terimlerin açıklamasına sahiptir.