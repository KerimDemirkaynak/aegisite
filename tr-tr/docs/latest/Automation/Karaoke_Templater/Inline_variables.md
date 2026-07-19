---
title: Satır içi değişkenler ($-değişkenleri)
menu:
  docs:
    parent: karaoke-templater
weight: 6140
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Inline_variables/
---

Bu sayfa, Karaoke Templater içinde kullanılabilen ve **dolar değişkenleri** olarak da bilinen **satır içi değişkenleri** (inline variables) açıklar.

## Satır içi değişkenler nasıl kullanılır?

Tüm satır içi değişkenler dolar işareti ($) ile başlar. Sadece şablon satırlarında çalışırlar, kod satırlarında çalışmazlar. Ancak şablon satırlarındaki kod bloklarının içinde kullanılabilirler.

İşte satır içi değişkenleri kullanan bir şablon metninin nasıl görünebileceğine dair bir örnek:

```ass
{\pos($x,$y)\t($start,$end,\bord0)}
```

`$x`, `$y`, `$start`, `$end` kısımları şablondaki satır içi değişkenlerdir.

Bir şablon uygulandığında gerçekleşen ilk şey, tüm satır içi değişkenlerin bulunması ve değerleriyle değiştirilmesidir. Örneğin, yukarıdaki örnekte `$x` ve `$y`, şablonun uygulandığı hecenin X ve Y koordinatlarıyla; `$start` ve `$end` ise hecenin başlangıç ve bitiş zamanlarıyla değiştirilir.

Satır içi değişkenler için büyük/küçük harf duyarlılığı yoktur. `$start`, `$START` ve `$StArT` ifadelerinin hepsi çalışır ve aynı sonucu verir.

### Sınırlamalar

Satır içi değişkenler "akıllı" değildir: nereye yerleştirirseniz yerleştirin aynı işlemi yaparlar ve hangi etiketle kullanıldıklarını "bilmezler". Her değişken her yerde başarıyla kullanılamaz ve bazılarının anlamı, örneğin [retime]({{< relref "./Code_execution_environment#retime" >}}) fonksiyonunun kullanımı gibi durumlardan etkilenir. Bu gibi durumlarda, satır içi değişkenler uygun olmayabilir ve kod bloklarını kullanmanız gerekir.

Satır içi değişkenlerin değerleri bir şablon uygulandığında ilk iş olarak belirlendiğinden, değerlerine herhangi bir şekilde müdahale edemezsiniz.

Satır içi değişkenleri kullanmak, bir efekte başlamak için kolay bir yoldur ancak birçok gelişmiş efekt için en iyi seçenek olmayabilirler.

Tüm konumlandırma ve boyutlandırma satır içi değişkenleri (örneğin `$y`, `$right` ve `$width`), kod bloklarında elde edebileceğiniz ve alt-piksel hassasiyetine sahip dahili veri yapılarındaki değerlerin aksine, en yakın tam piksel değerine yuvarlanır.

## Satır ve hece değişkenleri

Satır içi değişkenler hem "satır" hem de "hece" varyantlarına sahiptir. "Satır" varyantları işlenen satırın tamamı hakkındaki bilgileri içerirken, "hece" varyantları işlenen mevcut hece hakkındaki bilgileri içerir.

Ayrıca değişkenlerin çoğunun "otomatik" varyantları da vardır; bunlar kullanıldıkları şablon türüne bağlı olarak satır veya hece varyantı olurlar. "Pre-line" (satır öncesi) şablonlarda otomatik satır içi değişkenler satır varyantlarına, diğer tüm yerlerde ise hece varyantlarına referans verirler.

## Değişkenler

Otomatik varyantları da bulunan satır değişkenlerinin tümü küçük "L" harfi ile başlar. Hece varyantları ise "S" harfi ile başlar.

#### Satır varyantları

layer
: satır katmanı

lstart, lend, ldur, lmid
: satır başlangıç, bitiş, süre ve orta noktası, milisaniye cinsinden mutlak zamanlar

style
: satır stili adı

actor
: satır aktör adı

margin_l, margin_r
: etkin sol ve sağ kenar boşluğu (sıfır değilse satır, aksi takdirde stil)

margin_v, margin_t, margin_b
: etkin dikey, üst ve alt kenar boşluğu; dikey ve üst aynıdır

syln
: satırdaki hece sayısı

li
: satır dizini (dosyadaki ilk fiziksel satır 1'dir)

lleft, lcenter, lright
: kenar boşlukları ve hizalama hesaba katılarak satırın sol, yatay orta ve sağ kenarları, tam sayıya yuvarlanmıştır

ltop, lmiddle, lbottom
: kenar boşlukları ve hizalama hesaba katılarak satırın üst, dikey orta ve alt kenarları, yuvarlanmıştır

lx, ly
: hizalama geçersiz kılınmadığında \pos komutu için uygun satır x ve y konumu

lwidth, lheight
: piksel cinsinden satır genişliği ve yüksekliği, bu değer yuvarlanmıştır ve konumlandırma değişkenleriyle tam olarak eşleşmeyebilir

#### Hece varyantları

sstart, send, smid
: \t ve \move içine koymaya uygun, satır başlangıcına göre hece başlangıç, bitiş ve orta zamanları

sdur, skdur
: milisaniye ve santisaniye cinsinden hece süresi

si
: satır başlangıcından itibaren hece dizini

sleft, scenter, sright
: ekranın sol kenarından itibaren hece için mutlak sol, yatay orta ve sağ kenarlar, \pos ve \move için doğrudan uygundur

sbottom, smiddle, stop
: ekranın üst kenarından itibaren hece için mutlak alt, dikey orta ve üst kenarlar, gerekirse furigana konumlandırması için ayarlanmıştır, \pos ve \move için doğrudan uygundur

sx, sy
: varsayılan hizalamada hecenin mutlak x ve y konumu, \pos ve \move içinde doğrudan kullanıma uygundur

swidth, sheight
: piksel cinsinden hece genişliği ve yüksekliği, bu değer yuvarlanmıştır ve konumlandırma değişkenleriyle tam olarak eşleşmeyebilir

#### Otomatik varyantlar

start, end, mid
: satır/hece için başlangıç, bitiş ve orta zaman; satırlar için mutlak, heceler için göreceli

dur, kdur
: satır/hecenin milisaniye ve santisaniye cinsinden süresi

i
: satır veya hece dizini

left, center, right
: ekranın sol kenarından itibaren satırın/hecenin sol, orta ve sağ kenarları

top, middle, bottom
: ekranın üst kenarından itibaren satırın/hecenin üst, orta ve alt kenarları

x, y
: varsayılan hizalama kullanıldığında satırın/hecenin x ve y konumu

width, height
: piksel cinsinden satırın/hecenin genişliği ve yüksekliği, bu değer yuvarlanmıştır ve konumlandırma değişkenleriyle tam olarak eşleşmeyebilir