# Saat — Lokal Saat Uygulaması

Tarayıcıda sistem saatini **saniyede bir** güncelleyerek gösteren, tek dosyalık (pure HTML/CSS/JS) minimal bir saat uygulaması. Tipografi, cam efekti (glassmorphism), yumuşak parıltılar ve ince grid arkaplanıyla modern bir görünüm sunar. Yerel dil/biçem ayarlarını otomatik algılar.

---

## Özellikler

* ⏱️ **Anlık güncelleme:** `setInterval` ile saniyede bir yenilenen saat.
* 🌐 **Yerelleştirme:** `Intl.DateTimeFormat` ile kullanıcının `navigator.language` değerine göre tarih ve saat biçimi.
* 🧊 **Görsel tasarım:** cam arkaplan kartı, radial/conic/linear gradient’ler, yumuşak parıltı, ince grid overlay.
* 🔤 **Net tipografi:** tabular rakamlar ve responsive başlık boyutları.
* ♿ **Erişilebilirlik dokunuşu:** odak görünürlüğü için `sr-only` destek butonu.
* 📦 **Sıfır bağımlılık:** Tek bir `index.html`, ek araç ya da paket yok.

---

## Hızlı Başlangıç

1. Depoyu klonlayın veya `index.html` dosyasını indirin.
2. Dosyayı çift tıklayarak tarayıcıda açın.

Her şey bu kadar.

---

## Dosya Yapısı

```
.
└── index.html   # Uygulamanın tamamı tek dosyada
```

---

## Teknik Detaylar

* **Zaman/Tarih Biçimlendirme**

  * Zaman: `hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: false`
  * Tarih: `weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'`
  * Dil/yerel: `navigator.language` (desteklenmezse tarayıcı varsayılanı)

* **Güncelleme Döngüsü**

  ```js
  function tick() {
    const now = new Date();
    elClock.textContent = fmtTime.format(now);
    elClock.setAttribute('datetime', now.toISOString());
    elDate.textContent = fmtDate.format(now);
  }

  tick();            // ilk çizim
  setInterval(tick, 1000);  // saniyede bir güncelle
  ```

* **Stil ve Görsel Efektler**

  * CSS değişkenleri ile tema:

    ```css
    :root {
      --bg-grad: radial-gradient(...), conic-gradient(...), linear-gradient(...);
      --card-bg: rgba(255,255,255,0.05);
      --card-bd: rgba(255,255,255,0.10);
      --text-shadow: 0 8px 30px rgba(0,0,0,0.35);
    }
    ```
  * **Tabular rakamlar** (`font-variant-numeric: tabular-nums`) ile hane hizalaması.
  * **Responsive** yazı boyutları (`vw` ile) ve medyaya göre ölçekleme.

---

## Özelleştirme Rehberi

* **12 saat formatı (AM/PM):**

  ```js
  const fmtTime = new Intl.DateTimeFormat(locale, {
    hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: true
  });
  ```

* **Sabit yerel ayar (ör. Türkçe):**

  ```js
  const locale = 'tr-TR';
  ```

* **Renk paleti / parıltı ayarı:**

  ```css
  :root {
    --card-bg: rgba(255,255,255,0.06);
    --card-bd: rgba(255,255,255,0.12);
  }
  .glow {
    background: radial-gradient(circle at 50% 50%, #8b5cf6, #22d3ee, transparent 60%);
  }
  ```

* **Saat boyutu sınırları (desktop’ta daha küçük/büyük):**

  ```css
  @media (min-width: 1024px) { time#clock { font-size: 7vw; } }
  ```

---

## Erişilebilirlik

* `time#clock` elemanına ISO-8601 `datetime` özniteliği eklenir.
* Odak görünürlüğünü test eden `sr-only` butonu, klavye kullanıcıları için görünebilir hale gelir.
* Kontrast/görünürlük istenirse `--card-bg`, `--card-bd` ve yazı gölgesi ayarları artırılabilir.

---

## Tarayıcı Uyumluluğu

* `Intl.DateTimeFormat` geniş desteklidir; modern tarayıcılar hedeflenir.
* Çok eski tarayıcılar için polyfill gerektirebilir (projede dahil değildir).

---

## Dağıtım (GitHub Pages)

1. Bu depoda **Settings → Pages** bölümüne gidin.
2. **Source** olarak `main` branch ve `/root` klasörünü seçin.
3. Kaydedin; birkaç dakika içinde sayfanız yayında olacaktır.

Alternatif olarak herhangi bir statik hosting (Netlify, Vercel, Cloudflare Pages) tek tıkla çalışır.

---

## Geliştirme Notları

* Performans için **saniyede bir** güncelleme yeterli; daha sık güncelleme gereksiz CPU tüketir.
* Yazı tipi için sistem font yığını kullanılır; özel font eklemek isterseniz CSS’e dahil edebilirsiniz.
* Tek dosya mimarisi basit tutar; bileşenleştirme isterseniz `style` ve `script` bölümlerini ayrı dosyalara ayırabilirsiniz.

---

## Yol Haritası / Öneriler

* [ ] Tema anahtarlama (koyu/açık; otomatik sistem temasına uyum).
* [ ] Saat dilimi seçici (ör. UTC, belirli şehirler).
* [ ] Tam ekran mod / ekran koruyucu benzeri görünüm.
* [ ] PWA desteği (manifest + service worker).
* [ ] Haptik/ayar paneli (12/24 saat, yazı boyutu, renk paleti).

---

## Katkı

Hata/öneriler için **Issues** açabilirsiniz. Küçük düzeltmeler için doğrudan PR göndermek serbesttir. Kod stili basit ve yalındır; lütfen tek dosya yapısını koruyun ya da değişiklik yapıyorsanız kısa bir açıklama ekleyin.

---

## Teşekkür

Görsel ilham: modern UI trendleri (glassmorphism, yumuşak parıltı, grid overlay).
Teknik altyapı: yalnızca tarayıcı API’ları (`Intl`, `setInterval`) ve CSS.

---

### Hızlı Özet

* Tek dosya → `index.html`
* Aç ve çalıştır → derleme yok, bağımlılık yok
* Yerel dile göre otomatik tarih/saat
* Şık ve erişilebilir arayüz, kolayca özelleştirilebilir
