# TM4C123G-Icin-Ornek-Projeler
Proje 1(LCD_karakter_yazma)
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
