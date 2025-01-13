# TM4C123G-Icin-Ornek-Projeler
-Proje 1(LCD_karakter_yazma)-

Bu proje, TM4C123G mikrodenetleyicisini kullanarak GPIO portları aracılığıyla bir LCD ekranı kontrol etmek için geliştirilmiştir. Proje kodu, TivaWare kitaplığına dayalıdır ve temel GPIO çıkış işlemleriyle LCD'ye veri yazmayı ve ekran ayarlarını yapmayı içerir.

Proje Hakkında

Kodda aşağıdaki işlevler ve özellikler bulunmaktadır:
GPIO Portlarının Yapılandırılması:
Port C ve Port E, LCD ile iletişim için çıkış olarak yapılandırılmıştır.
Ekran Ayarları:
LCD'nin fonksiyon seçimi, ekran ayarları ve diğer yapılandırmalar yapılmaktadır.
Veri Yazma:
LCD'ye veri göndermek için gerekli işlemler gerçekleştirilmiştir.
Gecikmeler:
SysCtlDelay fonksiyonu, belirli işlemler arasında gecikme oluşturmak için kullanılmıştır.

Kullanılan Kütüphaneler

Projede aşağıdaki TivaWare kütüphaneleri kullanılmıştır:
sysctl.h ve sysctl.c: Sistem saatini yapılandırmak ve çevresel birimleri etkinleştirmek için.
gpio.h ve gpio.c: GPIO portlarının yapılandırılması ve veri yazımı için.

-Proje 2(LCD_Saat)-

Bu proje, Tiva C serisi mikrodenetleyici (TM4C123GH6PM) kullanılarak bir dijital saat uygulamasını gerçekleştirmeyi hedefler. Proje, dahili Timer modülü ve bir 16x2 LCD ekranı kullanarak saat, dakika ve saniye değerlerini görüntüler.

Özellikler
Saat, Dakika ve Saniye Gösterimi: LCD ekranda dijital saat formatında zaman gösterimi (hh:mm:ss).

Zaman Güncellemeleri: Timer modülü kullanılarak saniyede bir kesme oluşturulur ve zaman değerleri güncellenir.

Programlanabilir Sistem Saati: Mikrodenetleyicinin sistem saati, PLL ve osilatör ayarları ile 40 MHz olarak yapılandırılmıştır.

Kullanılan Kütüphaneler

TivaWare: Tiva mikrodenetleyicileri için yazılım geliştirme kütüphanesi.
driverlib/sysctl.h
driverlib/gpio.h
driverlib/timer.h
driverlib/interrupt.h
driverlib/adc.h

-Proje 3,4(ADC ve Seri Port Kısmı)-

Bu bölümde, projede kullanılan Seriport (UART) ve Analog-Dijital Çevirici (ADC) işlevleri detaylı bir şekilde açıklanmaktadır.

Seriport (UART)
Amaç
Mikrodenetleyici ile bir bilgisayar veya başka bir seri cihaz arasında veri iletişimi sağlamak.
Saat bilgilerini bilgisayara göndermek ve bilgisayardan gelen saat bilgilerini almak.
Seriport İşlemleri

1-UART Yapılandırması:

UART0, Tiva C'nin GPIOA portu üzerinden RX (PA0) ve TX (PA1) pinleri kullanılarak yapılandırılmıştır.
Baud hızı: 115200, veri formatı: 8-bit veri, 1 dur bit, parite yok.

2-Saat Verilerinin Gönderimi:

Saat bilgisi saatdizi dizisinden alınır ve formatlanarak seri porta gönderilir.
Gönderim, ASCII formatında yapılır:
Örneğin, [12:34:56] formatında saat bilgisi gönderilir.

3-Saat Verilerinin Alınması:

% karakteri geldiğinde, bilgisayardan saat bilgisi gönderileceği anlaşılır ve saatmi bayrağı set edilir.
Ardından gelen 8 karakterlik saat bilgisi saatdizi dizisine kaydedilir ve timer yeniden etkinleştirilir.

4-Mesaj Gönderimi:

Butona basıldığında, UARTCharPut fonksiyonu ile bir mesaj gönderilir.
Örnek mesaj: {emirh}\n

Analog-Dijital Çevirici (ADC)

Amaç
Harici sensörlerden alınan analog sinyalleri dijital değerlere dönüştürmek.
Ölçülen ADC değerini mV cinsinden hesaplamak ve LCD'ye yazdırmak.

1-ADC Modülü Yapılandırması:

ADC0 modülü, sekans 3 kullanılarak yapılandırılmıştır.
ADC işlemleri işlemci tarafından tetiklenir (ADC_TRIGGER_PROCESSOR).
ADC_CTL_CH0: Kanal 0 (AIN0) seçilmiştir.
Ortalama alınan değer kesme ile işlenir.

2-ADC Kesmesi:

ADC dönüşümü tamamlandığında kesme oluşur (ADCIntClear ile bayrak temizlenir).
Ortalama ADC değeri hesaplanır ve sıcaklık birimi olarak °C'ye dönüştürülür.

3-ADC Değerinin Gönderimi:

Ortalama ADC değeri, hane bazında parçalanarak seri porta gönderilir.
Format: (XXXX)\n

4-ADC Değerinin LCD'de Gösterimi:

LCDsayiYaz fonksiyonu, ADC'den alınan değeri LCD ekranında gösterir.

Notlar
ADC dönüşümünün doğruluğu, kullanılan sensöre ve referans voltajına bağlıdır.
Sıcaklık dönüşümü için, sensörün doğrusal karakteristiği göz önünde bulundurulmalıdır.

-Proje5(Hibernation)-

Projenin Amacı
Bu kod, Texas Instruments Tiva C serisi bir mikrodenetleyicide Hibernate (uyku) modunun kullanımını göstermektedir. Hibernate modu, enerji tasarrufu sağlamak için mikrodenetleyiciyi düşük güç tüketen bir moda geçirir. RTC (Gerçek Zamanlı Saat) alarmı sayesinde cihaz belirli bir süre sonra uyanabilir ve işlemlerine devam edebilir.

Fonksiyonlar ve Görevleri

1. main
Görevi: Hibernate modülünü başlatır, RTC alarmını ayarlar ve cihazı Hibernate moduna geçirir.

Detaylar:
Sistem saatini 16 MHz olarak yapılandırır.
Hibernate modülünü başlatır ve yapılandırır.
10 saniye sonra cihazı uyandıracak şekilde RTC alarmını ayarlar.
Hibernate moduna geçer ve cihaz uyandırıldığında döngüye devam eder.

2. Hibernate_Init

Görevi: Hibernate modülünü başlatır ve yapılandırır.
Detaylar:
Hibernate modülü için saat kaynağını etkinleştirir.
Hibernate osilatörünü düşük güç modunda yapılandırır.
RTC'yi etkinleştirir ve sıfırlar (opsiyonel).
RTC alarmı ile cihazın uyandırılmasını sağlar.

3. Hibernate_SetRTCAlarm

Görevi: RTC alarmını ayarlayarak belirli bir süre sonra cihazın uyanmasını sağlar.
Detaylar:
RTC'nin mevcut zamanını alır ve üzerine belirli bir süre ekleyerek alarm zamanını hesaplar.
RTC alarm zamanını ayarlar.

4. Hibernate_Enter

Görevi: Cihazı Hibernate moduna geçirir.
Detaylar:
Hibernate moduna geçiş talebinde bulunur.
Hibernate moduna geçiş tamamlanana kadar bekler.

Nasıl Çalışır?

Başlangıç: Mikrodenetleyici başlatıldığında sistem saati 16 MHz olarak yapılandırılır.
Hibernate Modülünün Etkinleştirilmesi: Hibernate modülü başlatılır, RTC ve osilatör etkinleştirilir.
RTC Alarmının Ayarlanması: RTC alarmı 10 saniye sonra cihazı uyandıracak şekilde ayarlanır.
Hibernate Moduna Geçiş: Cihaz Hibernate moduna geçer ve enerjiden tasarruf eder.
Uyandırma: 10 saniye sonra RTC alarmı devreye girer ve cihaz Hibernate modundan çıkarak işlemeye devam eder.
Son Döngü: Cihaz tekrar işlemeye devam eder ve gerekirse başka işlemler gerçekleştirebilir.

Donanım Gereksinimleri:

Tiva C serisi mikrodenetleyici (örneğin TM4C123G)
RTC alarmı için dahili osilatör kullanımı
Hibernate modülü uyandırma ayarları

Kullanım Notları:

Güç Yönetimi: Hibernate modu, düşük güç tüketimi gerektiren uygulamalarda kullanılır.
Uyandırma Kaynakları: Bu kod sadece RTC alarmını kullanarak cihazı uyandırır. Ancak, GPIO veya diğer kesme kaynakları ile uyandırma ayarları da yapılabilir.
Zamanlama: RTC alarm zamanı Hibernate_SetRTCAlarm fonksiyonu ile ayarlanır. Bu süreyi değiştirebilirsiniz.
