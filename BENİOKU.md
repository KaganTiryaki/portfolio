# Kağan Tiryaki — Portföy Sitesi

Three.js (WebGL) + GSAP ScrollTrigger + Lenis ile yapılmış, scroll'a dayalı
sinematik kişisel site. Merkezde **krom (sıvı metal) damla**; scroll boyunca
serpantin bir yörüngede dolaşır, en üstte ve en altta **tam ortada** durur.
Higgsfield ile üretilen aurora arka planı + parçacık bulutu + bloom.

**Tek dosya: `index.html`.** Build adımı yok.

## Çalıştırma (yerel)

Çift tıklayarak açılmaz (ES modülleri + `assets/env.png` yüklemesi yüzünden
tarayıcı engeller). Bu klasörün içinde yerel bir sunucu gerekir:

```powershell
py -m http.server 8000
```

Sonra tarayıcıda: **http://localhost:8000**

## Merkez nesneyi değiştirme (opsiyonel)

URL'den 4 farklı merkez nesne seçilebilir — tek kod tabanı:

| URL | Nesne |
|-----|-------|
| `localhost:8000/`            | Krom / aynalı sıvı metal (varsayılan) |
| `localhost:8000/?p=crystal`  | İridesan kristal |
| `localhost:8000/?p=neural`   | Nöral ağ |
| `localhost:8000/?p=gem`      | Fasetalı iridesan elmas |

Varsayılanı kalıcı değiştirmek için `index.html`'de şu satırı düzenle:
```js
const PIECE = (new URLSearchParams(location.search).get('p')||'chrome')...
```
`'chrome'` yerine `'crystal'` / `'neural'` / `'gem'` yaz.

## İçerik / etkileşim

- **Sinematik scroll:** krom merkez nesne scroll boyunca serpantin yörünge çizer
  (üstte ve altta tam ortada durur), ölçek/deformasyonu bölümlere göre değişir.
- **İşler:** dev hayalet sıra numaraları, reveal'de çizilen iridesan accent çizgisi,
  Borsa Botu'nda animasyonlu kanıt sayacı (%0,0 → %98,7) + dolan güven çubuğu.
- **Scroll-hız "juice":** hızlı kaydırınca krom ekstra döner, parçacıklar yatar,
  marquee hafif eğilir; yavaş/sakin kaydırmada efekt yok.
- Mikro-etkileşimler: manyetik butonlar, text-scramble, imleç-reaktif parçacıklar,
  harf-harf hero reveal, özel imleç.
- **İki dilli:** sağ üstte **bayrak düğmesi** (🇹🇷 / 🇺🇸); seçim hatırlanır (localStorage).
- **İletişim bağlı:** WhatsApp · E-posta · Instagram · GitHub.

## Yayına alma (Vercel — ücretsiz)

1. [vercel.com/new](https://vercel.com/new)
2. **`portfolio` klasörünün tamamını** sürükle-bırak. Gerekli dosyalar:
   `index.html` + `assets/env.png` + `assets/bg.png`.
3. Deploy → `adresin.vercel.app` hazır. Açılan adres doğrudan siteyi gösterir
   (artık tek `index.html` var, ayrı yönlendirme gerekmez).

## Teknik

- **Three.js** — krom MeshStandardMaterial (metalness 1, env yansıması) + snoise
  "soft-spiky" displacement shader; parçacık bulutu; UnrealBloom post-processing.
- **Lenis** — eylemsizlikli akıcı scroll.
- **GSAP ScrollTrigger** — scroll'a bağlı krom koreografisi + metin reveal'leri.
- `assets/env.png` — kromun yansıma/ortam haritası (Higgsfield).
- `assets/bg.png` — aurora arka planı (Higgsfield); radyal maskeyle ortası koyu.
- `prefers-reduced-motion` ve WebGL-yok yedeği var.

Not: Yoğun WebGL içerir; çok eski/zayıf telefonlarda kasabilir. Gerekirse mobilde
bloom/transmission'ı kısmak için söyle.
