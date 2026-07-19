---
title: pano
menu:
  docs:
    parent: lua-modules
weight: 6265
aliases:
  - /docs/latest/Automation/Lua/Modules/clipboard/
---

`clipboard` (pano) modülü, panodan okuma ve panoya yazma işlemleri için işlevler sağlar.

## Kullanım

Bu modülü {{< lua `clipboard = require 'aegisub.clipboard'` >}} ile içe aktarın.

### clipboard.get()

Özet: {{< lua `text = clipboard.get()` >}}

Panonun mevcut içeriğini bir dizge (string) olarak alır.
Pano şu anda metin içermiyorsa veya bir hata oluşursa `nil` döndürür.

### clipboard.set()

Özet: {{< lua `clipboard.set(new_text)` >}}

Pano içeriğini bir dizgeye ayarlar.
Pano ayarlanabilirse true, bir hata oluşursa false döndürür.