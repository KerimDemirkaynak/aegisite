---
title: Satır içi efektler Eğitimi
menu:
  docs:
    parent: tutorials
weight: 2720
aliases:
  - /docs/latest/Karaoke_inline-fx/
---

Karaoke satır içi efektler (inline-fx), bir satırın farklı bölümlerine farklı efektler atamak için [zamanlanmış karaoke]({{< relref "Timing#karaoke-timing" >}}) işaretleme yöntemidir.

Satır içi efekt işaretlemesi kendi başına bir şey yapmaz, yalnızca bunu anlayan bir [karaoke efekti betiği]({{< relref "Automation" >}}) zamanlanmış karaoke satırına uygulandığında bir etkisi olur.

## İşaretleme (Markup)

Satır içi efekt etiketleri, `\-efektadı` biçimindeki (normalde geçersiz olan) ASS geçersiz kılma etiketleridir; burada _efektadı_ tanımlanan satır içi efektin adıdır.

Normal geçersiz kılma etiketlerinde olduğu gibi, bir satır içi efekt etiketi, içinde bulunduğu heceyi ve içinde satır içi efekt etiketi olan bir sonraki heceye kadar olan tüm heceleri etkiler.

Her satırın başlangıcında satır içi efekt sıfırlanarak boş hale gelir.

{{<example-box>}}
İşte satır içi efekt işaretlemesine sahip zamanlanmış bir karaoke satırı:

```ass
{\k40}zu{\k20}t{\k42}to {\k32\-paint}e{\k17}ga{\k45}i{\k32}te{\k26}ta {\k24\-cloud}yu{\k55}me
```

Bu hecelere satır içi efektler şu şekilde atanır:

| Hece               | Satır içi efekt |
| ------------------ | --------------- |
| zu                 | (boş)           |
| t                  | (boş)           |
| to                 | (boş)           |
| e                  | `paint`         |
| ga                 | `paint`         |
| i                  | `paint`         |
| te                 | `paint`         |
| ta                 | `paint`         |
| yu                 | `cloud`         |
| me                 | `cloud`         |

{{</example-box>}}

## Karaoke Templater'da Kullanım

Efekt oluşturmak için [Karaoke Templater]({{< relref "Automation/Karaoke_Templater" >}}) kullanıyorsanız, şablonların yalnızca belirli bir satır içi efekte sahip heceleri etkilemesini sağlamak için şablonlarda _fx_ değiştiricisini kullanabilirsiniz. (Doğrudan) yalnızca boş satır içi efekte sahip hecelerle eşleşmek mümkün değildir.

{{<example-box>}}
Yukarıdaki örnek zamanlanmış karaoke ile şu şablonlara sahip olabilirsiniz:

```plaintext
template syl: {tüm heceler için uygulanan temel efekt}
template syl fx paint: {yalnızca 'paint' hecelerine uygulanan katman efekti}
template syl fx cloud: {yalnızca 'cloud' hecelerine uygulanan katman efekti}
```

Buradaki fikir, temel bir efekte sahip olmak ve ardından bazı hecelerin bunun üzerine ek efektler almasını sağlamaktır.

{{</example-box>}}

{{<example-box>}}
Kara-templater içinde, satır içi efekte dayalı olarak etkinleşen veya devre dışı kalan bir _fxgroup_ kullanarak yalnızca boş satır içi efekte sahip hecelerle eşleşmek mümkündür. Ayrıca birden fazla satır içi efekt için çalışan şablonlara sahip olmak için \_fxgroup_s kullanabilirsiniz.

```plaintext
code syl: fxgroup.blankfx = (syl.inline_fx == "")
template syl fxgroup blankfx: {efekt yalnızca boş satır içi efektli hecelere uygulanır}
```

Önemli olan, kod satırının her hece için çalışması ve onu kullanması gereken hece bazlı şablonlardan önce çalıştırılmasıdır.

{{</example-box>}}

## Lua betiklerinde kullanım

Satır içi efekt etiketleri [`karaskel.preproc_line_text`]({{< relref "Automation/Lua/Modules/karaskel.lua.md#karaskelpreproc_line_text" >}}) tarafından ayrıştırılır, bu nedenle yalnızca altyazı satırlarınızda bu düzeyde bir karaskel ön işlemesi uyguladıysanız çalışacaklardır.

Bir hece için satır içi efekt daha sonra `syl.inline_fx` olarak kullanılabilir ve efektleri koşullu olarak uygulamak için bunu bir dizeyle karşılaştırabilirsiniz.

{{<example-box>}}
Betiğinizde hece başına çalışan bazı kodlarda:

```lua
if syl.inline_fx == "" then
    apply_base_effect(subs, meta, line, syl)
elseif syl.inline_fx == "paint" then
    apply_paint_effect(subs, meta, line, syl)
elseif syl.inline_fx == "cloud" then
    apply_cloud_effect(subs, meta, line, syl)
end
```

Basitçe satır içi efekt adını çeşitli olasılıklarla karşılaştırın ve doğru efekt kodunu çalıştırın.

{{</example-box>}}
{{<example-box>}}
Betiğinizde hece başına çalışan bazı kodlarda:
Betiğinizin en üst düzeyinde:

```lua
effects = {}
effects[""] = function(subs, meta, line, syl)
    -- temel efekt kodu buraya
end
effects.paint = function(subs, meta, line, syl)
    -- paint efekt kodu buraya
end
effects.cloud = function(subs, meta, line, syl)
    -- cloud efekt kodu buraya
end
```

Daha sonra, hece bazlı işleme kodunda:

```lua
effects[syl.inline_fx](subs, meta, line, syl)
```

Öncelikle, farklı efektleri uygulamak için fonksiyonlarla doldurulmuş bir tablo oluşturulur. Tablo için kullanılan anahtarlar, olası satır içi efektlerin adlarıdır. Efektin uygulanması gerektiğinde, efekt tablosunda doğru fonksiyon bulunur ve çağrılır.
{{</example-box>}}