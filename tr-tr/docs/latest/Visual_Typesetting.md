---
title: Görsel Dizgi
menu:
  docs:
    parent: typesetting
weight: 4300
aliases:
  - /docs/latest/Visual_Typesetting/
---

{{<todo>}}Ekran görüntüleri güncellenmelidir {{</todo>}}

## Genel Bakış

![video_display](/img/3.2/video_display.png#center)

### Oynat (Play)

Videoyu, şu an görüntülenen kareden başlayarak oynatır. Videoyu Aegisub'da oynatma ile ilgili notlar için [Video]({{< relref "Video#playing-video" >}}) bölümüne bakınız.

### Satırı oynat (Play line)

Videoyu, şu an aktif olan satırın ilk karesinden başlayarak oynatır ve satırın sonunda durdurur.

### Video otomatik arama (Video autoseek)

Yeni bir satır seçildiğinde videonun otomatik olarak o satırın ilk karesine gitmesini açar/kapatır.

### Kare zamanı ve numarası

Mevcut kare numarasını ve karenin başlangıç zamanını görüntüler. Eğer o an görüntülenen kare bir ana kare (keyframe) ise, bu kutucuğun arka planı yeşil renkte olur.

"Seçili altyazıların başlangıcını mevcut video karesine ayarla" (Ctrl-3) ve "Seçili altyazıların sonunu mevcut video karesine ayarla" (Ctrl-4) komutlarının, zamanı burada görüntülenenden farklı bir değere ayarlamasının normal olduğunu unutmayın; çünkü zamanları tam olarak karenin zamanına eşitlemek genellikle yuvarlama hatalarına yol açar.

{{<todo>}}Ana araç çubuğu aslında herhangi bir yerde belgelenmiş mi? {{</todo>}}

### Altyazı göreceli zamanı

Aktif altyazı satırının başlangıç ve bitiş zamanına kalan süreyi görüntüler. Bu özellik çoğunlukla [\\t]({{< relref "ASS_Tags#animatedtransform" >}}) ve [\\fad]({{< relref "ASS_Tags#fade" >}}) gibi göreceli zaman alan geçersiz kılma etiketleri (override tags) için kullanışlıdır.

### Yakınlaştırma (Zoom)

Mevcut video yakınlaştırma oranını görüntüler ve değiştirilmesine izin verir.

### Video konum kaydırıcısı

Videoda gezinmek için kullanılır. Sürgüyü sürüklerken Shift tuşuna basılı tutmak ana karelere yapışmasını sağlar. Varsayılan olarak, sol/sağ ok tuşları bir kare ileri/geri gider; Alt-sol/sağ 10 kare ileri/geri gider; Shift-sol/sağ bir ana kare ileri/geri gider. Kaydırıcıya yanlışlıkla arama yapmadan odaklanmak için sağ tıklayabilir veya Ctrl-Space tuşlarına basabilirsiniz. Kaydırıcı zaten odaktaysa, Ctrl-Space tuşları klavye odağını son odaklanılan kontrole geri döndürür.

## Video bağlam menüsü

Diğer seçenekleri içeren bir bağlam menüsü açmak için sağ tıklayabilirsiniz:

![Visual_menu](/img/3.2/Visual_menu.png#center)

PNG anlık görüntüsünü kaydet
: Mevcut karenin bir PNG görüntüsünü [seçeneklerde]({{< relref "options#video" >}}) belirtilen yola kaydeder. Bu görüntü gerçek video boyutunda olacak ve yakınlaştırma veya en-boy oranı geçersiz kılmalarından etkilenmeyecektir.

Görüntüyü panoya kopyala
: Yukarıdaki ile aynıdır, ancak görüntüyü PNG olarak kaydetmek yerine panoya kopyalar. Daha sonra herhangi bir resim düzenleme yazılımına yapıştırabilirsiniz.

PNG anlık görüntüsünü kaydet (altyazısız)
: Bir önceki seçenekle aynıdır, ancak altyazılar görüntüde görünmez.

Görüntüyü panoya kopyala (altyazısız)
: Yukarıdaki ile aynıdır, ancak panoya kopyalar.

Koordinatları panoya kopyala
: Mevcut fare koordinatlarını panoya kopyalar, örn: "230,152"

## Araç Açıklamaları

Şu anda yedi farklı görsel dizgi aracı bulunmaktadır: artı imleci (crosshair), sürükle (drag), Z ekseninde döndür, XY eksenlerinde döndür, ölçekle (scale), dikdörtgen kırpma (rectangular clip) ve vektörel kırpma (vector clip).

### Artı imleci (Crosshair)

Bu standart moddur. Fareyi videonun üzerinde gezdirmek, imlecin altındaki betik koordinatlarını ve baktığınız tam noktayı gösteren bir artı imlecini gösterir. Shift tuşunu basılı tutmak, bunun yerine sağ alt köşeden olan uzaklığı gösterir. Bir noktaya çift tıklamak, mevcut satırı ([\pos etiketi]({{< relref "ASS_Tags#setposition" >}}) kullanarak) o konuma yerleştirir. Çift tıklama sırasında Alt tuşu basılı tutulursa, mevcut karede görünmeyen satırlar dahil olmak üzere seçili diğer tüm satırlar aktif satırla aynı mesafede kaydırılır.

![Visual_crosshair](/img/3.2/Visual_crosshair.png#center)

### Sürükle (Drag)

Sürükleme aracının iki modu vardır. Yardımcı görsel dizgi çubuğundaki düğmeye tıklayarak bunlar arasında geçiş yapabilirsiniz.

![Visual_drag](/img/3.2/Visual_drag.png#center)

Konumlandırma modunda, altyazıları çapaları (kareler) aracılığıyla video yüzeyinde sürükleyerek kolayca taşıyabilirsiniz. Bıraktığınız yere [\\pos]({{< relref "ASS_Tags#setposition" >}}) komutu ile yerleştirilirler.

Hareket modunda, bir daire ile temsil edilen "hareket sonu" çapası bulunur. Hareket başlangıcından hareket sonuna işaret eden bir ok olacaktır. Hareketin başlayacağı veya biteceği zamanları ayarlamak için, ilgili çapayı altyazının o çapada olmasını istediğiniz zamana taşıyın. Örneğin, hareketin satır başlangıcından 5000 milisaniye sonra başlamasını istiyorsanız, videoyu satır başlangıcından 5000 milisaniye sonrasına getirin ve başlangıç çapayı oraya sürükleyin. Aynı durum hareket sonu çapası için de geçerlidir.

Eğer satırınızın bir köken noktası (origin point) belirlenmişse, noktalı bir çizgiyle kare çapaya bağlı, üçgenle temsil edilen üçüncü bir çapa göreceksiniz. Köken konumunu etkilemek için bunu da sürükleyebilirsiniz. Bu aynı çapa iki döndürme aracında da görünür olacaktır.

Bir çapayı sürüklerken Shift tuşuna basılı tutulursa, sürükleme işlemi sadece X veya Y koordinatını (hangisi daha fazla değişecekse) değiştirmekle sınırlanacaktır.

Ctrl tuşuna basılı tutup seçime eklemek veya çıkarmak istediğiniz çapalara tıklayarak aynı anda birden fazla çapa seçilebilir. Bir çapa sürüklendiğinde tüm seçili çapalar hareket eder.

Çapa olmayan bir noktaya çift tıklamak, aktif çapayı o konuma taşır (artı imleci aracındaki çift tıklama işlemine benzer). Alt tuşu basılı tutulursa, seçili diğer tüm çapalar aktif çapaya göre kaydırılır.

### Z ekseninde döndür (Rotate on Z axis)

Bu modda, altyazının pivot noktası (belirlenmişse pozisyonu veya köken noktası) etrafında ortalanmış bir daire göreceksiniz. Daire, açıları işaretlemeye ve ölçmeye yardımcı olan 6 yay ile çevrilidir.

![Visual_rotate_1](/img/3.2/Visual_rotate_1.png#center)

Bu modda iki işlevsellik vardır. Ya (mevcut değilse [\\org]({{< relref "ASS_Tags#rotationorigin" >}}) etiketi ekleyerek) hareket ettirmek için köken noktasını (dairenin merkezindeki üçgen) sürükleyebilir ya da satırı döndürmek için başka herhangi bir yere tıklayıp sürükleyebilirsiniz.

Dairenin merkezini fare imlecine bağlayan bir çizgi olduğunu fark edeceksiniz. Tıklayıp sürüklediğinizde, altyazı satırı o çizgiyi takip ederek döner; yani satırı döndürmek için imleci merkezin etrafında döndürmeniz gerekir. Konumlandırmayı bitirmek için fareyi bırakmanız yeterlidir. Ayrıca rotasyonu 30 derecelik artışlarla sınırlamak için Ctrl tuşunu kullanabilirsiniz.

Eğer köken merkezden uzaksa, döndürürken altyazıların merkezinin nereye konumlanacağını gösteren küçük bir yardımcı çizgi göreceksiniz.

Birden fazla satır seçilirse, tüm seçili satırlar yeni rotasyona ayarlanır (sürükle ve artı imleci araçlarında olduğu gibi birbirlerine göre döndürülmezler).

![Visual_rotate_2](/img/3.2/Visual_rotate_2.png#center)

### XY eksenlerinde döndür (Rotate on XY axes)

Bu mod önceki moda biraz benzerdir, ancak birkaç önemli fark vardır. Bu, iki ekran ekseninde döndüğü için, rotasyon üç boyutludur ve görselleştirilmesi daha zordur.

Bunu kolaylaştırmak için, altyazıların üzerinde bulunduğu düzlemi temsil eden bir ızgara vardır ve siz bu ızgarayı döndürürsünüz. Ayrıca merkezden dışarıya doğru, üç eksenin yönünü ve oryantasyonunu gösteren üç ok bulunur.

![Visual_rotate_xy](/img/3.2/Visual_rotate_xy.png#center)

Bu aracı kullanmak için, fare düğmesini ekranın herhangi bir yerinde basılı tutun ve hareket ettirin. Sağa ve sola hareket ettirdiğinizde satır Y ekseninde, yukarı ve aşağı hareket ettirdiğinizde ise X ekseninde dönecektir.

Döndürürken Shift tuşuna basılı tutarsanız, rotasyon iki eksenden sadece biriyle (en fazla hareketin olduğu yönde) sınırlanır. Ctrl tuşuna basılı tutarsanız, rotasyon 30 derecelik adımlarla gerçekleşir.

Birden fazla satır seçilirse, tüm seçili satırlar yeni rotasyona ayarlanır.

Z döndürme aracında olduğu gibi, burada da köken çapayı sürükleyebilirsiniz.

### Ölçekle (Scale)

Bu en basit araçtır ve altyazıları X ve Y eksenlerinde ölçeklendirmenize olanak tanır. Her eksen için bir çubuk gösterir; bu çubuklar sadece %100 boyutunu değil, aynı zamanda mevcut ölçeği de gösterir.

![Visual_scale](/img/3.2/Visual_scale.png#center)

Bu aracı kullanmak için, fare düğmesini basılı tutun ve fareyi yukarı-aşağı (Y ekseninde ölçekleme için) veya sağa-sola (X ekseninde ölçekleme için) sürükleyin. En büyük değişimin olduğu eksenle sınırlamak için Shift tuşunu, %25'lik artışlarla sınırlamak için ise Ctrl tuşunu basılı tutabilirsiniz.

### Dikdörtgen kırpma (Rectangular clip)

Dikdörtgen kırpma aracı, eksene hizalı bir dikdörtgenin DIŞINDA hiçbir şeyin görüntülenmemesi için altyazıları kırpmanıza olanak tanır (özünde `\clip(x1,y1,x2,y2)` etiketi).

![Visual_clip](/img/3.2/Visual_clip.png#center)

Bu aracı kullanmanın iki yolu vardır. Ya dikdörtgenin dört köşesinden birini tıklayıp tutarak mevcut bir kırpmayı yeniden boyutlandırabilir ya da sıfırdan yeni bir dikdörtgen oluşturmak için boş bir alanda tıklayıp sürükleyebilirsiniz. Görünmez olacak alanlar karartılacaktır.

### Vektörel kırpma (Vectorial clip)

Son araca benzer şekilde, vektörel kırpma aracı, dışındaki hiçbir şeyin işlenmemesi için bir alan çizmenize olanak tanır. Ancak fark, bu alanın çizgiler ve bézier eğrilerinden oluşan bir yol ile tanımlanan herhangi bir keyfi şekle sahip olabilmesidir.

![Visual_vector_clip](/img/3.2/Visual_vector_clip.png#center)

Bu modun 8 alt aracı vardır:

![Visual_vector_toolbar](/img/3.2/Visual_vector_toolbar.png#center)

1. Sürükle - Bir kontrol noktasını sürüklemenizi sağlar.
1. Çizgi ekle - Noktaya tıklayarak son noktadan mevcut fare konumuna düz bir çizgi eklemenizi sağlar.
1. Bézier bicubic eğrisi ekle - Yukarıdakinin aynısıdır ancak bicubic bir eğri ekler. Daha sonra eğrinin şeklini ayarlamak için iki kontrol noktasını kullanabilirsiniz.
1. Çizgi ve eğri arasında dönüştür - Diğer türe dönüştürmek için bir çizgi segmentine veya bicubic eğriye tıklayın.
1. Eğriyi böl - İşaretli noktada ikiye bölmek için bir çizgi segmentine veya bicubic eğriye tıklayın.
1. Noktayı sil - Silmek için bir noktaya tıklayın.
1. Serbest çizim şekli - Video üzerinde fare ile tıklayıp sürükleyerek, çizgi segmentlerinden oluşan serbest bir şekil çizin. Bu şekil, ilk nokta ile son noktanın birleşmesiyle otomatik olarak kapatılacaktır.
1. Serbest pürüzsüz şekil - Yukarıdakinin aynısıdır ancak şekil bicubic eğrilerle pürüzsüzleştirilir.

Sürükleme aracında olduğu gibi, seçime eklenecek veya çıkarılacak çapalara Ctrl-tıklama yapılarak aynı anda birden fazla kontrol noktası seçilebilir. Varsayılan olarak tüm kontrol noktaları seçilidir; hepsinin seçimini kaldırmak için Sürükle modundayken boş bir noktaya tıklayın. Taşıma modunda tıklayıp sürükleyerek kutu seçimi yapmak suretiyle aynı anda birden fazla kontrol noktası seçilebilir.