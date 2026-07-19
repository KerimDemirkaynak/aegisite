---
title: Ses ile Çalışmak
menu:
  docs:
    parent: timing
weight: 5000
aliases:
  - /docs/latest/Audio/
---

Aegisub, hem geleneksel dalga formu (waveform) gösterimi hem de alternatif bir spektrum gösterimi sunan oldukça gelişmiş, özelleştirilebilir bir ses moduna sahiptir. Hem normal diyalog zamanlaması hem de karaoke zamanlaması için çeşitli farklı zamanlama modları mevcuttur.

## Ses açma

Aegisub'a bir ses dosyası yüklemek için _Ses_ (Audio) menüsüne gidin ve _Ses dosyası aç_ (Open audio file) seçeneğine basın. Eğer halihazırda yüklü bir video dosyanız (ses parçası dahil) varsa, bunun yerine _Videodan ses aç_ (Open audio from video) seçeneğini kullanabilirsiniz; bu seçenek, mevcut videonuzdaki ses parçasını yükleyecektir. [Ses sağlayıcınızın]({{< relref "Options#advancedaudio" >}}) kodunu çözebildiği her türlü ses dosyasını açabilirsiniz (aşağıda daha fazla bilgi bulabilirsiniz). Ayrıca, gerçek bir ses dosyası yüklemeden sadece ses ekranını kullanmak isterseniz, _2s30dk Boş Ses Aç_ (Open 2h30 Blank Audio) veya _2s30dk Gürültü Sesi Aç_ (Open 2h30 Noise Audio) seçeneklerini tercih edebilirsiniz.

Ses açma işlemi bir ses oynatıcı hatasıyla sonuçlanırsa veya ses çalındığında hiç ses gelmiyorsa, [farklı bir ses oynatıcıya]({{< relref "Options#advancedaudio" >}}) geçmek sorunu çözebilir.

### Desteklenen formatlar

Aegisub, ses dosyalarını açmak için normalde neredeyse aklınıza gelebilecek her formatı güvenilir bir şekilde açabilen [FFMS2](https://github.com/FFMS/ffms2) kullanır. Windows üzerinde Aegisub, dosyaları açmadan önce indekslemesi gerekmediğinden daha hızlı olabilen DirectShow'u (Avisynth aracılığıyla) da kullanabilir. Ancak DirectShow önemli ölçüde daha az güvenilirdir ve Avisynth aracılığıyla birden fazla ses parçası içeren bir dosyayı açarsanız son derece beklenmedik durumlar yaşanabilir.

Aegisub sadece mono sesi destekler. Çok kanallı sesler otomatik olarak mono haline getirilir (downmix), ancak iki kanaldan fazla kaynak için sonuçlar düşük kaliteli olabilir.

### Ses önbellekleme

Sıkıştırılmamış (PCM) bir Microsoft WAV dosyası olmayan herhangi bir ses formatı yüklüyorsanız, Aegisub'ın önce bunun kodunu çözmesi ve önbelleğe alması gerekir. Yüklendiğinde, ses mono kanalına indirgenir (sadece bir kanalı almak istiyorsanız [ses dönüştürücü seçeneğine]({{< relref "Options#avisynth-windows-only" >}}) bakın), PCM'ye (WAV olarak bilinir) açılır ve (varsayılan olarak) bir RAM önbelleğine yüklenir. Bu, uzun bir sıkıştırılmış ses dosyasını açmak için _yüklü miktarda_ RAM'e ihtiyacınız olacağı anlamına gelir. Eğer bilgisayarınızın RAM'i azsa veya tam uzunlukta bir film üzerinde çalışıyorsanız, Aegisub'ın (daha yavaş olan) sabit disk önbelleğini nasıl kullanacağına dair talimatlar için [ses önbelleği seçeneğine]({{< relref "Options#cache" >}}) bakın; veya dosyayı önce WAV formatına dönüştürün, çünkü Aegisub önbelleğe alma gereği duymadan WAV dosyalarını doğrudan okuyabilir.

Belirli bir ses dosyası için kullanılan tam bellek miktarı aşağıdaki formülle hesaplanabilir:
s = ( b * r * l ) / 8
burada _s_ bellek miktarı (byte cinsinden - kB elde etmek için 1024'e bölün), _b_ örnek başına bit sayısı (mevcut uygulamada her zaman 16), _r_ örnekleme hızı (Hz cinsinden, genellikle 48000, bazı durumlarda 44100) ve _l_ sesin uzunluğudur (saniye cinsinden).

Örneğin, 48 kHz'de 25 dakikalık bir ses klibi için (16 * 48000 * 25 * 60)/8 = 144000000 byte ~= 137 MB belleğe ihtiyacınız olacaktır.

Sesi yüklemek ve önbelleğe açmak biraz zaman alır. Ses yüklenirken ses ekranının kaydırma çubuğunda bir ilerleme çubuğu gösterilir.