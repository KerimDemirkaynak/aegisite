---
title: Şablonları tanımlama
menu:
  docs:
    parent: karaoke-templater
weight: 6110
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Declaring_template_and_code_lines/
---

Bu sayfa, bir şablon satırının veya kod satırının nasıl tanımlandığını açıklar.

- Şablon satırları ve kod satırları her zaman Yorum (Comment) olarak işaretlenir.

<div></div>

- Efekt alanındaki boşlukla ayrılmış ilk kelime, satırın bir şablon satırı mı, kod satırı mı, zamanlanmış karaoke satırı mı, stillendirilmiş karaoke satırı mı yoksa başka türlü belirlenmemiş bir şey mi olduğunu belirler.

<div></div>

- Efekt alanındaki ilk kelime `template` ise, satır bir şablon satırıdır.

<div></div>

- Efekt alanındaki ilk kelime `code` ise, satır bir kod satırıdır.

<div></div>

- Efekt alanı tam olarak `fx` ifadesine eşitse, satır stillendirilmiş bir karaoke satırıdır. Stillendirilmiş karaoke satırları, Karaoke Templater'ın çalıştırılması sırasında silinir.

<div></div>

- Efekt alanı `Karaoke`, `karaoke` ise veya boşsa, satır zamanlanmış bir karaoke satırıdır.

<div></div>

- Efekt alanı başka bir şey içeriyorsa, satır belirsiz bir tiptedir ve Karaoke Templater tarafından dokunulmaz.

<div></div>

Şablon satırları ve kod satırları, `template` veya `code` anahtar kelimelerinden sonra ek metin içerebilir. Bu metin, boşluklarla ayrılmış bir dizi kelime olarak ayrıştırılır ve değiştiriciler (modifiers) olarak adlandırılır. Bunun hakkında daha fazla bilgi için [Şablon değiştiricileri]({{< relref "./Template_modifiers" >}}) bölümüne bakın.