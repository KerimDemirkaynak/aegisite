---
title: Karaoke Şablonlayıcı
menu:
  docs:
    parent: automation
    identifier: karaoke-templater
weight: 6100
aliases:
  - /docs/latest/Automation/Karaoke_Templater/
---

**Karaoke Şablonlayıcı (Karaoke Templater)**, Aegisub ile birlikte gelen bir [Otomasyon]({{< relref "Automation" >}}) betiğidir. Temel amacı, özel olarak tasarlanmış bir şablon dili ile [karaoke efektleri]({{< relref "../Glossary/Karaoke_effect" >}}) oluşturmaya yardımcı olmaktır. Karaoke Şablonlayıcı halihazırda yüklüdür ve Aegisub ile birlikte kullanıma hazırdır.

## Öğreticiler: Karaoke Şablonlayıcıya Giriş

- [Basit bir örnek]({{< relref "./Karaoke_Templater/Tutorial_1" >}})
- [Matematiksel ifadeleri kullanma]({{< relref "./Karaoke_Templater/Tutorial_2" >}})
- [Birden fazla şablon satırı kullanma](#)
- [Konumlandırılmış hecelerle daha gelişmiş efektler](#)

{{<todo>}}Daha fazla öğretici planlayın. Ayrıca yukarıdakileri gerçekten yazın. {{</todo>}}

## Referans

- [Şablon ve kod satırlarını tanımlama]({{< relref "./Karaoke_Templater/Declaring_template_and_code_lines" >}})
- [Şablonların ne zaman ve hangi sırayla çalıştırılacağına dair kurallar]({{< relref "./Karaoke_Templater/Template_execution_rules_and_order" >}})
- [Şablon değiştiriciler]({{< relref "./Karaoke_Templater/Template_modifiers" >}})
- [Satır içi değişkenler (dolar-değişkenleri)]({{< relref "./Karaoke_Templater/Inline_variables" >}})
- [Kod blokları ve kod satırları için kurallar]({{< relref "./Karaoke_Templater/Code_lines_and_blocks" >}})
- [Kod bloğu/satırı yürütme ortamının içerikleri]({{< relref "./Karaoke_Templater/Code_execution_environment" >}})

`line` ve `syl` değişkenlerinde nelerin olduğu ve daha fazlası hakkında bilgi için ayrıca [`Automation/Lua/Modules/karaskel.lua`]({{< relref "Lua/Modules/karaskel.lua.md" >}}) bölümüne bakın.

## _Multi-template_ (Çoklu şablon) kullanıcıları için

Aegisub 1.10'daki _multi-template_ betiğini kullandıysanız, karaoke şablonlayıcıda benzer birçok kavramı tanıyacaksınız, ancak dikkat etmeniz gereken bazı tuzaklar da mevcut. Bunlardan bazıları şunlardır:

- Şablon satırlarını artık Aktör (Actor) alanında değil, Efekt (Effect) alanında tanımlıyorsunuz. Buraya sadece `template` değil, çok daha fazlasını da yazabilirsiniz. Giriş için yukarıdaki öğreticileri okuyun veya maceraperest hissediyorsanız aşağıdaki referansa göz atın.
- Lua kod bloklarını yazmak için yüzde işaretleri kullanmak yerine ünlem işaretleri kullanıyorsunuz. Yani `%$start+$i*30%` yerine `!$start+$i*30!` yazın.
- `A` global değişkeni kaldırıldı, ancak `line` ve `syl` doğrudan erişilebilir durumda. Kaçışlı (escaped) Lua kodu artık gerçek global ortamda değil, kendi ortamında çalıştırılıyor; bu sayede şablonlarınız ile Karaoke Şablonlayıcı arasında çakışma yaşanması çok daha düşük bir ihtimal.
- Bir şablonun yürütülmesini iptal etmek için kullanılan `return false` hilesi artık çalışmıyor. Genel olarak çok ifadeli Lua bloklarına sahip olmak ve bunlardan değer döndürmek de artık çalışmıyor. İlk amaç için `fxgroup` işlevselliği getirildi, çok ifadeli ihtiyaçlarınız için ise kod satırları tanıtıldı.
- `newline` ve `line` (oluşturulmakta olan ve orijinal satır için) ile çalışmak yerine, artık oluşturulmakta olan satırlar için `line` ve orijinal satırlar için `orgline` ile çalışıyorsunuz.
- Oluşturulan satırlarınızın başlangıç ve bitiş zamanlarını kontrol etmeyi çok daha kolaylaştırmak için `retime` fonksiyonu getirildi.
- Çok daha fazla süslü özellik eklendi. Tüm bunları öğrenmek için öğreticileri kontrol edin veya referansı okuyun.