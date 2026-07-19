---
title: Otomasyon Yöneticisi
menu:
  docs:
    parent: automation
weight: 6300
aliases:
  - /docs/latest/Automation/Manager/
---

Otomasyon Yöneticisi penceresi, [Otomasyon]({{< relref "Automation" >}}) betiklerini görüntülemek, yüklemek ve kaldırmak için kullanılır.

Otomasyon Yöneticisi penceresi, _Otomasyon_ menüsünden veya ![Otomasyon-araç-çubuğu-simgesi](/img/3.2/Automation-toolbar-icon.png) araç çubuğu düğmesi ile açılır.

![otomasyon_yöneticisi](/img/3.2/automation_manager.png)

## Betik listesi

Pencerenin ana alanı, yüklenmiş tüm _betik dosyalarının_ bir listesidir. Bir betik dosyasının birkaç [özellik]({{< relref "../Glossary/Automation_script_feature" >}}) içerebileceğini unutmamak önemlidir; örneğin bir betik dosyası iki [makro]({{< relref "../Glossary/Macro" >}}) ve bir dışa aktarma filtresi tanımlayabilir.

Betikler iki yoldan biriyle yüklenebilir. Yukarıdaki ekran görüntüsünde, betiklerin çoğu en soldaki sütunda "G" harfi ile belirtildiği gibi _geneldir_ (otomatik yüklenen). Genel betikler, Aegisub ile birlikte otomatik olarak yüklenir. Bunlar [Otomasyon_otomatik_yükleme_klasörlerine](#) konulur. Genel betikleri kaldıramazsınız; bunları otomatik yükleme dizininden silmeniz ve ardından otomatik yükleme dizinini yeniden taratmanız gerekir.

Yukarıdaki ekran görüntüsündeki son betik, diğer betik türüne bir örnektir: "L" ile belirtilen _yerel_ betikler. Ekle düğmesi aracılığıyla manuel olarak eklenen betikler, üzerinde çalışılan altyazı dosyasına özeldir ve mevcut altyazı dosyası kapatıldığında otomatik olarak kaldırılır, ardından dosyayı yeniden açtığınızda altyazı dosyasıyla birlikte tekrar yüklenir.

Bazen bir betik listede kırmızı renkte görünür. Bu durum yalnızca betik herhangi bir nedenle yüklenemezse gerçekleşir. Nedeni genellikle Açıklama sütununda gösterilir. Hata açıklaması okunamayacak kadar uzunsa, betiği seçip hepsini görmek için Bilgiyi Göster düğmesine tıklayabilirsiniz. Yüklenemeyen betikler, yalnızca kendi betiklerinizi yazıyorsanız ve bir programlama hatası yapmayı başarırsanız gerçekleşmelidir.

## Düğmeler

Otomasyon Yöneticisi penceresinin altında 6 düğme bulunur:

- **Ekle** düğmesi, yerel bir betik yüklemek için kullanılır.
- **Kaldır** düğmesi, yerel bir betiği kaldırmak için kullanılır. Yalnızca yerel bir betik seçildiğinde kullanılabilir.
- **Yeniden Yükle** düğmesi, seçili betik dosyasını diskten kaldırıp tekrar yükler. Bunu geliştirdiğiniz betikleri yeniden yüklemek için kullanabilirsiniz, ancak bunu yapmanın diğer yolları için aşağıya bakın.
- **Bilgiyi Göster** düğmesi, seçili betik hakkında ve tüm Otomasyon sistemi hakkında ayrıntılı bilgi gösterir.
- **Otomatik Yükleme Dizinini Yeniden Tara** düğmesi, Aegisub başlatıldığından beri herhangi bir betiğin eklenip eklenmediğini veya kaldırılıp kaldırılmadığını görmek için otomatik yükleme klasörlerini tarar. Otomatik yükleme dizinlerindeki tüm yeni betikler daha sonra yüklenir, kaldırılmış olan betikler kaldırılır ve diğer tüm genel betikler yeniden yüklenir.
- **Kapat** düğmesi, Otomasyon Yöneticisi penceresini kapatır.

## Betikleri yeniden yüklemenin diğer yolları

Betik geliştiriyorsanız, betiğinizi yeniden yüklemek için sık sık Otomasyon Yöneticisi'ne döndüğünüzü fark edebilirsiniz. Ancak betikleri yeniden yüklemenin daha hızlı yolları da vardır:

- [Dışa Aktar]({{< relref "Exporting" >}}) iletişim kutusu açıldığında tüm yerel betikler yeniden yüklenir. Bunu [Seçenekler]({{< relref "Options#automation" >}}) iletişim kutusundan değiştirebilirsiniz.
- Otomatik yükleme klasörlerini yeniden taramak için Ctrl tuşunu basılı tutarak Otomasyon araç çubuğu düğmesine tıklayın.
- Tüm betikleri yeniden yüklemek ve ayrıca otomatik yükleme klasörlerini yeniden taramak için hem Ctrl hem de Shift tuşlarını basılı tutarak Otomasyon araç çubuğu düğmesine tıklayın.
- Tüm betikleri yeniden yüklemek için varsayılan bir kısayol tuşu olmasa da, [tercihler iletişim kutusundan]({{< relref "Options#hotkeys" >}}) bir tane ekleyebilirsiniz.

Bu yöntemlerden herhangi biri kullanıldığında Otomasyon Yöneticisi açılmaz, ancak bir betik yüklenemezse bir hata mesajı penceresi alırsınız. Daha fazla bilgi için hata iletişim kutusundaki satırlara çift tıklayabileceğinizi unutmayın.