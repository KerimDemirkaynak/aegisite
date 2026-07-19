---
title: unicode.lua
menu:
  docs:
    parent: lua-modules
weight: 6263
aliases:
  - /docs/latest/Automation/Lua/Modules/unicode/
---

Automation 4 Lua için `unicode` modülü, UTF-8 kodlamalı metinlerle çalışmak için çeşitli yardımcı fonksiyonlar içerir.

## Kullanım

Bu modülü {{< lua `unicode = require 'aegisub.unicode'` >}} ile içe aktarın.

## unicode.charwidth

Özet: {{< lua `width = unicode.charwidth(instring, index=1)` >}}

`instring` içerisinde `index` konumundan başlayan UTF-8 kodlamalı karakterlerin kapladığı bayt sayısını döndürür.
İşaret edilen karakterin bir önek baytı (yani karakter dizisinin ilk baytı) olduğu varsayılır.

`index` parametresi isteğe bağlıdır ve belirtilmediğinde varsayılan olarak 1 (bir) kabul edilir; bu da `instring` içerisindeki ilk karakterin genişliğinin döndürüleceği anlamına gelir.

## unicode.chars

Özet: {{< lua `for char in unicode.chars(instring) do ... end` >}}

Verilen UTF-8 kodlamalı dizgedeki tüm karakterler (code point) üzerinde döngü kurmak için bir yineleyici (iterator) fonksiyonu döndürür.
Döngünün her yinelemesinde, `char` dizgedeki bir sonraki karakteri temsil eden bir dizge içerir. Bu dizge bir bayttan daha uzun olabilir.

## unicode.len

Özet: {{< lua `length = unicode.len(instring)` >}}

Verilen UTF-8 kodlamalı dizgenin karakter (code point) cinsinden uzunluğunu belirler.

Bu fonksiyonun sabit zamanda değil, `instring` içerisindeki Unicode karakter sayısıyla orantılı olarak doğrusal zamanda (O(N)) çalıştığına dikkat edin.

## unicode.codepoint

Özet: {{< lua `val = unicode.codepoint(instring)` >}}

`instring` içerisindeki ilk unicode karakterini okur.

## unicode.to_upper_case

Özet: {{< lua `upper = unicode.to_upper_case(instring)` >}}

Bir dizgeyi büyük harfe dönüştürür.
Bu fonksiyon aksanları, latin olmayan alfabeleri ve benzerlerini işleyebilir.

## unicode.to_lower_case

Özet: {{< lua `lower = unicode.to_lower_case(instring)` >}}

Bir dizgeyi küçük harfe dönüştürür.
Bu fonksiyon aksanları, latin olmayan alfabeleri ve benzerlerini işleyebilir.

## unicode.to_fold_case

Özet: {{< lua `folded = unicode.to_fold_case(instring)` >}}

Bir dizgeyi "fold case" (küçük harf benzeri bir dönüştürme) biçimine dönüştürür.
Bu işlem küçük harfe dönüştürmeye benzer ancak yerel ayarlardan bağımsızdır ve büyük/küçük harfe duyarsız karşılaştırmalar için daha iyi sonuçlar verir.