Demo benzeri, animasyonlu bir web sitesi (laboratuvar/demo amaçlı)

Dosyalar:
- index.html
- styles.css
- script.js
- assets/ (slayt ve diğer görselleri buraya koyun)

Çalıştırma:
1. Klasörde `index.html` dosyasını çift tıklayın veya bir HTTP sunucusunda açın.

Notlar:
- `assets/slide1.jpg`, `assets/slide2.jpg`, `assets/slide3.jpg` adlı görselleri ekleyin; yoksa CSS arka planları boş kalır.
- Galeri örnek görüntüleri uzak placeholder URL kullanır; yerel görsellerle değiştirmek isterseniz `index.html` içindeki `url(...)` yollarını değiştirin.
- İleri geliştirme: animasyonları zenginleştirmek isterseniz `script.js` içinde slider zamanlamasını veya `styles.css` içinde anahtar kare animasyonlarını güncelleyin.

Ek notlar:
- Slayt arka planları artık `.slide-bg` elemanı içinde yer alır ve Ken Burns (yavaş zoom) efekti uygulanır. `assets/slideN.jpg` dosyalarını `assets/` klasörüne koyun.
- Sayfa açılışında görünen renkli tema overlay'i (`.page-overlay`) yüklendikten sonra yavaşça kaybolur. Overlay'i değiştirmek için `styles.css` içindeki `.page-overlay` kurallarını düzenleyin.
