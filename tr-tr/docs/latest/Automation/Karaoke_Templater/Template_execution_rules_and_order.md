---
title: Yürütme sırası
menu:
  docs:
    parent: karaoke-templater
weight: 6120
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Template_execution_rules_and_order/
---

Bu sayfa, Karaoke Templater (_kara-templater_) aracının nasıl çalıştığına dair teknik detayları açıklar; bazı şeylerin neden bu şekilde çalıştığını, bazılarının ise neden çalışmadığını veya çalışmayacağını açıklamaya çalışır.

Bunların çoğu, kara-templater kullanmak için bilmeniz gerekmeyen teknik detaylardır, ancak anlamadığınız bir davranışla karşılaşırsanız bu sayfa açıklayıcı olabilir.

## Kavramlar

Bunlar, açıklama boyunca kullanılan bazı terimler ve kavramlardır. İsimler, betiğin kendisinde kullanılanlarla aynı veya benzerdir.

`tenv`
: **t**emplate **env**ironment (şablon ortamı) veya [kod yürütme ortamı]({{< relref "./Code_execution_environment" >}}).

`varctx`
: Satır içi **var**iable **c**on**t**e**x**t (değişken bağlamı), [satır içi değişkenlerin]({{< relref "./Inline_variables" >}}) gerçek değerlerinin depolandığı yerdir.

`template` (şablon)
: Kara-templater'ın temel "yürütme birimi"; bir şablon, esasen kara-templater tarafından derlenen ve yürütülen bir mini programdır.

`code template` (kod şablonu)
: Bir Lua kodu parçası çalıştıran ancak çıktı üretmeyen şablondur. (_code_ anahtar sözcüğü ile tanımlanır.)

`output template` (çıktı şablonu)
: Bazı karaoke veri girdilerinden çıktı satırları üreten şablondur. (_template_ anahtar sözcüğü ile tanımlanır.)

`code line` (kod satırı)
: Altyazı dosyasında bir kod şablonunu tanımlayan satırdır.

`template line` (şablon satırı)
: Altyazı dosyasında bir çıktı şablonunu veya bir parçasını tanımlayan satırdır. (Bir _line_ sınıfı çıktı şablonu, birden fazla şablon satırını kapsayabilir.)

`class` (sınıf)
: Bir sınıf, bir şablon türüdür. Dört temel sınıf vardır: _once_, _line_, _syl_ ve _furi_; ilki yalnızca kod şablonları için kullanılabilir.

`modifier` (değiştirici)
: Değiştiriciler, şablonların nasıl ve ne zaman yürütüleceğini etkiler.

`template text` veya kısaca `text` (şablon metni)
: Şablonun "metin" kısmı; kod şablonlarında Lua kodu, çıktı şablonlarında ise şablon kodudur. _line_ sınıfı çıktı şablonlarının ayrıca bir _pre-line text_ (satır öncesi metni) kısmı vardır.

## Başlangıç

Kara-templater'ın yaptığı ilk şey, altyazı dosyası hakkında bazı temel bilgileri toplamak için [karaskel]({{< relref "../Lua/Modules/karaskel.lua.md" >}}) kullanmaktır. `karaskel.collect_head` işlevindeki _generate_furigana_ parametresi için her zaman `true` değerini geçirir; bu, [furigana]({{< relref "Furigana_karaoke" >}}) stillerinin zaten mevcut değilse her zaman oluşturulacağı anlamına gelir.

Daha sonra dosyadaki tüm şablon satırlarını toplar.

### Şablonları toplama, ayrıştırma ve derleme

Dosyadaki her satır ziyaret edilir ve bir şablon satırı olup olmadığı kontrol edilir; yani bir yorum satırı olması ve Etki (Effect) alanındaki ilk kelimenin _code_ veya _template_ olması gerekir.

Detaylar burada önemli değildir, ancak Etki alanında bulunan her değiştirici adı, ya şablonda bir bayrak (flag) ayarlar ya da değiştiriciye verilen parametreye karşılık gelen bir değer atar.

İsimlendirilmiş bir _line_ sınıfı şablon satırı ile karşılaşıldığında, önce o isimde bir _line_ sınıfı şablon olup olmadığı kontrol edilir. Eğer yoksa, o isimle yeni bir şablon oluşturulur ve verilen değiştiricilerle başlatılır. Eğer zaten varsa, _şablon satırının metni, şablonun mevcut metnine eklenir_ ve yeni şablon satırında bulunan ancak mevcut şablonda olmayan değiştiriciler şablona eklenir. Değiştiriciler, şablonlardan bu şekilde veya başka bir yolla kaldırılamaz. _pre-line_ şablon satırlarının metni, normal metne değil, şablonun _pre-line text_ kısmına eklenir.

Farklı sınıflardaki şablonlar kendi "kovalarına" konur, bu yüzden örneğin _line_ ve _syl_ şablonları bir arada tutulmaz.

### Temizlik

Tüm şablonlar toplandıktan sonra, altyazı dosyasındaki tüm eski ve artık ihtiyaç duyulmayan satırlar silinir. Bu durum temel olarak Etki alanında _fx_ içeren satırları kapsar, çünkü bunların kara-templater'ın önceki bir çalışmasında oluşturulduğu varsayılır ve bu yeni çalışmada değiştirilmeleri gerekir.

### _tenv_'i başlatma

Şablonları gerçekten çalıştırmaya başlamadan önce yapılan son işlem, çalışma zamanı ortamını başlatmaktır. Temel olarak, herhangi bir şablon çalıştırılmadan önce mümkün olan her şey _tenv_ içerisine yerleştirilir. İçindekiler hakkında daha fazla ayrıntı için [Kod yürütme ortamı]({{< relref "./Code_execution_environment" >}}) bölümüne bakın. (Temel olarak `line`, `orgline`, `syl` ve `basesyl` dışındaki her şey.)

## _once_ şablonlarını çalıştırma

_once_ sınıfındaki tüm şablonlar önce yürütülür. Burada gerçekten heyecan verici bir şey olmaz; gerçekleşebilecek temel şey, _tenv_'e birkaç şeyin daha eklenmesidir.

## Dosyadaki karaoke satırları üzerinde yineleme

Dosyadaki şablon olmayan her satır üzerinden geçilir ve tüm şablonlar sırayla uygulanmaya çalışılır.

- Bir satır yorum ise ve Etki alanı `Karaoke` içermiyorsa, hemen atlanır.
- Bir satır yorum değilse ve Etki alanı `Karaoke` dışında başka bir şey içeriyorsa veya boşsa, hemen atlanır.
- Kara-templater, tüm şablonları diğer tüm satırlarla eşleştirmeye çalışır.

Yukarıdaki maddelerce reddedilmeyen her satır, üç adımda tüm şablonlardan geçirilir.

İlk olarak, tüm _line_ sınıfı şablonları satırla eşleştirilmeye çalışılır ve ardından satır üzerinde çalıştırılır. Bir şablonun bir satırla ne zaman eşleştiğinin tanımı için aşağıya bakın.

Daha sonra, satırdaki tüm heceler sırayla işlenir ve her biri için tüm _syl_ sınıfı şablonları satırla eşleştirilmeye çalışılır ve ardından hece üzerinde çalıştırılır.

Son olarak, satırdaki tüm furigana heceleri sırayla işlenir ve her biri için her _furi_ sınıfı şablonu satırla eşleştirilmeye çalışılır ve ardından furigana hecesi üzerinde çalıştırılır.

Döngüye alınan hecelerin ve furigana hecelerinin, ayrıştırılmış ve saklanmış heceler olduğunu; çoklu vurgulu sanal heceler, karakter bazlı sanal heceler veya bunların bir kombinasyonu olmadığını not etmek önemlidir.

{{<example-box>}}
Üç tane `syl` sınıfı şablonu olduğunu varsayalım: A, B ve C.

- A, _multi_ veya _char_ değiştiricisi olmayan normal bir şablondur.
- B, _multi_ değiştiricisine sahiptir ancak _char_ yoktur.
- C, hem _char_ hem de _multi_ değiştiricilerine sahiptir.

Şimdi bu şablonlar 2 heceli bir satıra uygulanır. Bu işlem sırayla gerçekleşir:

- 1. Hece seçilir.
  - Şablon A, satırla eşleştirilir. Eşleşir.
    - Şablon A, 1. heceye uygulanır.
  - Şablon B, satırla eşleştirilir. Eşleşir.
    - 1. hece, 1.1 ve 1.2 çoklu vurgulu sözde hecelerine bölünür.
    - Şablon B, 1.1 sözde hecesine uygulanır.
    - Şablon B, 1.2 sözde hecesine uygulanır.
  - Şablon C, satırla eşleştirilir. Eşleşir.
    - 1. hece, 1.a ve 1.b karakter bazlı sözde hecelerine bölünür.
    - 1.a ve 1.b heceleri, 1.a1, 1.a2, 1.b1 ve 1.b2 karakter bazlı sözde hecelerine bölünür.
    - Şablon C, 1.a1 sözde hecesine uygulanır.
    - Şablon C, 1.a2 sözde hecesine uygulanır.
    - Şablon C, 1.b1 sözde hecesine uygulanır.
    - Şablon C, 1.b2 sözde hecesine uygulanır.
  - 2. Hece seçilir.
    - İşlem 1. heceye benzer şekilde devam eder.

Çoklu vurgu ve karakter bazlı sözde heceler hakkında daha fazla ayrıntı için aşağıya bakın.
{{</example-box>}}

Yukarıdaki üç adım sırasında herhangi bir zamanda herhangi bir şablon eşleşirse, (orijinal) satır "zamanlanmış karaoke" olarak işaretlenir ve Etki alanında `karaoke` bulunan bir yorum satırı haline getirilir.

### Bir şablonu bir satırla eşleştirme

Şablonlar her zaman bir heceyle veya başka bir şeyle değil, her zaman bir satırla eşleştirilir.

- Eğer şablon _fxgroup_ değiştiricisine sahipse ve adlandırılan fxgroup devre dışıysa, şablon hiçbir şeyle eşleşmez.
- Eğer şablon _all_ değiştiricisine sahipse, her zaman her satırla eşleşir.
- Eğer şablon, satırla aynı Stile sahipse, satırla eşleşir.
- Aksi takdirde şablon satırla eşleşmez.

## _line_ sınıfı şablonlarını uygulama

{{<todo>}} bunu yaz {{</todo>}}

## _syl_ ve _furi_ sınıfı şablonlarını uygulama

{{<todo>}} bunu yaz {{</todo>}}

## Eski orta seviye açıklama

<pre>Ana kara-templater süreci:
1. Başlığı topla
   1. Tüm başlık bilgilerini bul, öncelikle PlayResX ve PlayResY
   2. Tüm stilleri bul
   3. Eksik stiller için furigana stilleri oluştur
2. Şablonları topla ve mevcut "fx" satırlarını sil
3. tenv'i başlat
   1. "string", "math" ve "_G" referanslarını ekle
   2. "tenv" öz referansını ekle
   3. "retime" işlevini ekle
   4. Boş "fxgroup" tablosu ekle
4. Her "code once" şablonunu çalıştır
5. Altyazı dosyasındaki her mevcut diyalog satırı için:
   a. Eğer Etki alanı "code" veya "template" ile başlıyorsa:
      1. Satırı atla
   b. Değilse:
      1. Eğer Etki alanı boş değilse ve "karaoke" değilse:
         a. Satırı atla
      2. Eğer Etki alanı boşsa ve satır bir Yorum ise:
         a. Satırı atla
      3. Satırı karaskel ile ön işlemden geçir
      4. varctx'i başlat
      5. tenv'i sıfırla
         1. "orgline"'ı girdi satırına ayarla
         2. "line", "syl" ve "basesyl"'i nil değerine ayarla
      6. Her "line" şablonu için:
         Eğer şablon satır stiliyle eşleşiyorsa veya şablon "all" ise:
         Bunu "template.loops" sayısı kadar tekrarla:
         1. "tenv.j"'yi döngü sayacına ayarla
         2. a. Eğer şablon bir kod satırıysa:
               1. "tenv.line"'ı girdi satırına ayarla
               2. Kodu çalıştır
            b. Değilse:
               1. Girdi satırının kopyası olarak çıktı satırı üret
               2. "tenv.line"'ı çıktı satırına ayarla
               3. Çıktı satırı Katmanını (Layer) şablon Katmanına ayarla
               4. Çıktı satırı Metnini boş olarak başlat
               5. Eğer şablonda satır öncesi (pre-line) varsa:
                  1. Satır öncesi şablonu çalıştır
                  2. Sonucu çıktı Metnine ekle
               6. a. Eğer şablonda normal satır varsa:
                     Girdi satırındaki her hece için:
                     1. "tenv.syl"'i heceye ayarla
                     2. Hece için varctx'i güncelle
                     3. Satır şablonunu çalıştır
                     4. Sonucu çıktı Metnine ekle
                     5. Eğer "notext" ayarlı değilse:
                        a. Eğer "keeptags" ayarlıysa:
                           1. "syl.text"'i çıktı Metnine ekle
                        b. Değilse:
                           1. "syl.text_stripped"'i çıktı Metnine ekle
                  b. Değilse:
                     a. Eğer "keeptags" ayarlıysa:
                        1. "syl.text"'i çıktı Metnine ekle
                     b. Değilse:
                        1. "syl.text_stripped"'i çıktı Metnine ekle
               7. Çıktı satırı Etki alanını "fx" olarak ayarla
               8. Çıktı satırını altyazı dosyasına ekle
      7. Satırdaki her ana hece için:
         Her "syl" şablonu için:
         Eğer şablon satır stiliyle eşleşiyorsa veya şablon "all" ise:
         Eğer şablon devre dışı bir fxgroup'da değilse:
         1. "tenv.syl"'i heceye ayarla
         2. Hece için varctx'i güncelle
         3. Eğer hece inlinefx'i şablon inlinefx'i ile eşleşmiyorsa:
            1. Heceyi atla
         4. Eğer şablonda "noblank" ayarlıysa ve hece boşsa:
            1. Heceyi atla
         5. Eğer şablon "char" ise:
            1. Hece kopyası olarak "charsyl" oluştur
            2. "tenv.basesyl"'i mevcut "tenv.syl"'e ayarla
            3. "tenv.syl"'i "charsyl"'e ayarla
            4. Hece içindeki her Unicode karakteri için:
               1. "charsyl" için sanal hece özelliklerini hesapla
               2. "charsyl" için varctx'i güncelle
               3. Sanal hece için hece işlemine devam et (5.b.7.6.'dan itibaren)
         6. Eğer şablon "multi" ise:
            1. Hece kopyası olarak "hlsyl" oluştur
            2. "tenv.basesyl" zaten yoksa, onu "hlsyl"'e ayarla
            3. "tenv.syl"'i "hlsyl"'e ayarla
            4. Hece üzerindeki her vurgu için:
               1. "hlsyl" için sanal hece özelliklerini hesapla
               2. "hlsyl" için varctx'i güncelle
               3. Sanal hece için hece işlemine devam et (5.b.7.7.'den itibaren)
         7. a. Eğer şablon bir kod satırıysa:
               1. "tenv.line"'ı girdi satırına ayarla
               2. Kodu çalıştır
            b. Değilse:
               Bunu "template.loops" sayısı kadar tekrarla:
               1. "tenv.j"'yi döngü sayacına ayarla
               2. Çıktı satırı oluştur
               3. Çıktı satırı Stilini sanal hece stiline ayarla
               4. Çıktı satırı Katmanını şablon katmanına ayarla
               5. "tenv.line"'ı çıktı satırına ayarla
               6. Şablonu çalıştır
               7. Çıktı satırı Metnini sonuca ayarla
               8. a. Eğer "keeptags" ayarlıysa:
                     1. "syl.text"'i çıktı satırı Metnine ekle
                  b. Eğer "notext" ayarlı değilse:
                     1. "syl.text_stripped"'i çıktı satırı Metnine ekle
                  c. Aksi takdirde hiçbir şey eklenmez
               9. Çıktı satırı Etkisini "fx" olarak ayarla
              10. Çıktı satırını altyazı dosyasına ekle
      8. Satırdaki her furigana parçası için:
         Ana hecelerle aynı işlem (5.b.7.)
      9. Eğer satıra kod olmayan şablonlar uygulandıysa:
         1. Girdi satırını Yorum yap
         2. Girdi satırı Etki alanını "karaoke" olarak ayarla
         3. Değiştirilmiş girdi satırını altyazı dosyasına kaydet

Kod satırını çalıştırma:
1. Satır metnini bir Lua işlevine derle
2. Derleme başarısız olursa, hata bildir
3. Derlenmiş işlevin ortamını tenv olarak ayarla
4. Bunu "template.loops" sayısı kadar tekrarla:
   1. "tenv.j"'yi döngü sayacına ayarla
   2. Derlenmiş işlevi çalıştır
   3. Bir hata oluşursa, bildir

Tek bir şablonu çalıştırma:
1. Sonuç metnini şablon olarak ayarla
2. Eğer bir varctx varsa:
   Sonuç metnindeki her "$([a-zA-Z_]+)" eşleşmesi için:
   1. Yakalanan ismin küçük harf karşılığını al
   2. a. Eğer yakalanan isim varctx'te bir alansa:
         1. Sonuç metnindeki eşleşmeyi varctx'teki değerle değiştir
      b. Değilse:
         1. Uyarı bildir
         2. Eşleşmeyi sonuç metninde olduğu gibi bırak
3. Sonuç metnindeki her "!(.-)!" eşleşmesi için:
   1. Yakalanan koda "result " ekle
   2. Yakalanan kodu bir Lua işlevine derle
   3. Derleme başarısız olursa, hata bildir
   4. Derlenmiş işlevin ortamını tenv olarak ayarla
   5. Derlenmiş işlevi çalıştır
      a. Eğer derlenmiş işlev bir hata üretirse:
         1. Hata bildir
         2. Eşleşmeyi sonuç metninde bırak
      b. Değilse:
         1. Eşleşmeyi işlevi çalıştırmanın sonucuyla değiştir</pre>

{{<todo>}}Bunu daha makul bir şeye dönüştür? {{</todo>}}