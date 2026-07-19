---
title: Yol Belirleyiciler
menu:
  docs:
    parent: miscellaneous
weight: 7200
aliases:
  - /docs/latest/Aegisub_path_specifiers/
---

Aegisub, dosya konumlarını belirtmek için basit bir sistem kullanır. Aegisub'daki çoğu yol adı, her biri belirli konumları ifade eden özel değişkenlerle başlatılarak yazılabilir. Yol belirleyicilerin, yolun tamamı olmadıkları sürece her zaman sonunda bir eğik çizgi (/) içermesi gerektiğini unutmayın (yani ?scripta çalışmaz).

?data
: Uygulama verilerinin depolandığı konum. Windows'ta bu, kurulum dizinidir (.exe dosyasının konumu). Mac OS X'te bu, uygulama paketinin içindedir. Diğer POSIX benzeri sistemlerde bu `$prefix/share/aegisub/` dizinidir.

?user
: Yapılandırma dosyaları, otomatik yedeklemeler ve bazı ek öğeler gibi kullanıcı veri dosyalarının konumu. Windows'ta bu `%APPDATA%\Aegisub\` dizinidir, Mac OS X'te `$HOME/Library/Application Support/Aegisub/` dizinidir ve diğer POSIX benzeri sistemlerde `$HOME/.aegisub/` dizinidir. Taşınabilir (portable) modda bu, ?data olarak değişir.

?temp
: Sistem geçici dizini. Ses önbelleği ve gerekli tüm geçici altyazı dosyaları burada saklanır.

?local
: Yerel kullanıcı ayarları dizini. FFMS2 dizinleri ve fontconfig önbelleği gibi çalıştırmalar arasında kalıcı olması gereken önbellek dosyaları burada saklanır. Windows'un güncel sürümlerinde `%LOCALAPPDATA%\Aegisub` dizinidir, diğer her yerde ise ?user ile aynıdır.

?script
: Yalnızca bir altyazı dosyası açık ve bir yere kaydedilmişse tanımlanır; bu durumda betiğin bulunduğu dizini işaret eder.

?video
: Yalnızca bir video dosyası yüklendiğinde tanımlanır. Video dosyasının bulunduğu dizini işaret eder. Sahte (dummy) video yüklüyken buranın bir şeyleri kaydetmek için iyi bir yer olmadığını unutmayın.

?audio
: Yalnızca bir ses dosyası yüklendiğinde tanımlanır. Ses dosyasının bulunduğu dizini işaret eder. Sahte (dummy) ses yüklüyken buranın bir şeyleri kaydetmek için iyi bir yer olmadığını unutmayın.