---
title: Renk Seçici
menu:
  docs:
    parent: typesetting
weight: 4500
aliases:
  - /docs/latest/Colour_Picker/
---

Aegisub, varsayılan Windows renk seçicisinden daha gelişmiş bir renk seçici sunar. Renk değerlerini çeşitli renk uzaylarını kullanarak hem HTML hem de ASS onaltılık (hex) formatında girmenize, mini bir ekran görüntüsü üzerinden renk seçmenize ve renkleri grafiksel olarak seçmek için üç farklı renk spektrumu kullanmanıza olanak tanır.

## Genel Bakış

![Renk seçici](/img/3.2/Colour_picker.png#center)

Renk seçici aşağıdaki bileşenlere sahiptir:

- Renk spektrumu
- Dört renk uzayı için parametrik ayarlar
- ASS ve HTML formatları için HEX girişi
- Mini bir ekran görüntüsü alıp oradan renk seçmek için ekran-üzerinden-seç kontrolü
- En son seçilen 32 rengin listesi

Renk spektrumunun en son kullanılan modu hatırlanır.

## Ekran-üzerinden-seç fonksiyonunu kullanma

1. Ekran-üzerinden-seç kontrolü, pencerenin alt kısmında, en son kullanılan renklerin solunda bulunur.
1. Kullanmaya başlamak için "renk seç" simgesine tıklayın.
1. Ekran üzerinde sürükledikçe, renk seç butonunun yanındaki kare kutunun, imlecin üzerinde gezindiği alanın büyütülmüş haline dönüştüğünü fark edeceksiniz.
1. Rengi almak istediğiniz alanı bulduğunuzda, büyütmeyi sabitlemek için sol fare tuşuna tıklayın.
1. Şimdi büyütülmüş görüntüde rengini almak istediğiniz piksele tıklayın.

OS X'te, teknik kısıtlamalar nedeniyle, seçme kontrolüne tıklayıp ardından rengi almak istediğiniz noktaya tıklamak yerine, seçme kontrolünü istediğiniz noktaya kadar sürüklemeniz gerekmektedir.

## Renk uzaylarının tanımları

Mevcut üç renk uzayının kısa bir özeti şöyledir:

- _RGB_ - Kırmızı, Yeşil ve Mavi; bir bilgisayar monitörünün görüntüleri görüntülemek için kullandığı üç bileşen rengidir. RGB modunda, bu üç bileşenin her birinin yoğunluğunu belirlersiniz.
- _HSL_ - Ton, Doygunluk ve Parlaklık (Luminance). Ton, rengin gerçek "rengidir"; yani kırmızı, yeşil, mavi veya bunların bir karışımıdır. Doygunluk, rengin "griliği"dir; doygunluk azaldıkça renk gri tonuna yaklaşır. Parlaklık, rengin açıklığıdır; maksimum parlaklık saf beyaz, sıfır parlaklık ise saf siyah anlamına gelir.
- _HSV_ - Ton, Doygunluk ve Değer (Value). Ton ve Doygunluk, HSL'deki ile aynı anlama gelir. Ancak Değer, HSL'deki parlaklıktan farklıdır. Değer, rengin "siyah olmama" derecesidir; değer küçüldükçe renk saf siyaha yaklaşır.