# PROGRESS — Begümnaz Program · Oturum Devamlılık Dosyası

> **Bu dosya yeni oturumun ilk okunan dosyasıdır.** Burada nerede kaldığımız, yarın ne yapacağımız, hangi kararların değişmediği yazılır. Önceki oturumda olan her kritik şey buraya yansır.

**Son güncelleme**: 13 Mayıs 2026 — Faz 4 İterasyon 30A (i18n EN Dashboard bilingual · renderHeroCard + nextActions + ZEN + compassion)

---

## 🚨 SONRAKİ OTURUMDA İLK YAPILACAK (Next session first action)

### 1. Manuel `git push` — Faz 4 Iter 20-29 (10 commit, push'lanmadıysa)

Bu oturumda 13 Mayıs 2026 Faz 4 büyük kısmı tamamlandı (Iter 19'dan sonra Iter 20-29, Iter 26 atlandı):

```bash
cd /Users/agent9/Desktop/bnsp-repo
git status                    # "ahead of origin/main by N commits" görmeli
git push origin main          # manuel push
```

Push sonrası GitHub Pages otomatik deploy. SW cache **v17-dinamik-tema-ai** — eski cache yenilenir.

### 2. Iter 30 — i18n EN tam çeviri (SONRAKİ OTURUM)

**Plan**: M1 (EN tam çeviri) öngörüsü 1.5-2 gün iş. Multi-phase:
- **30A**: I18N obje 27 → 100+ key + applyTranslations refactor
- **30B**: WEEKLY_FOCUS_TEXTS + ZEN + BODY_INTENTIONS bilingual
- **30C**: AI prompt'ları dinamik dil (getLang() bazlı) + glossary def bilingual

Bu oturumda atlandı — yorucu, push önceliği. Sonraki oturumda Iter 30A ile başla.

### 3. Iter 26 — Egzersiz video link upgrade (kullanıcı feedback bekleniyor)

PWA YT_MAP zaten direct watch URL kullanıyor (çalışıyor). md dosyalarında search URL'ler kullanıcı seçimine bağlı. Begümnaz hangi videoları beğendiğini söyleyince spesifik watch URL'lere geçilir.

### 4. (Opsiyonel) iOS Safari install + cache test

PWA install → "Ana ekrana ekle". SW v17 yeni cache → eski yenilenir, ilk açılışta hard reload gerekebilir.

### 5. (Opsiyonel) Begümnaz gerçek kullanım feedback'i

PWA artık Faz 4 ile çok daha kişisel + üretimde:
- Sabah açılışta AI merhamet mesajı (Iter 28)
- Settings'tan görsel yükle → tüm tema değişir (Iter 29)
- Beslenme + Supplement birleşik takip (Iter 22)
- Cilt ürün listesi Begümnaz'ın gerçek ürünleri (Iter 21)
- Regl onboarding placeholder (Iter 27)
- Mobile + popup UX iyileştirmeleri (Iter 23-25)

Begümnaz 1-2 hafta günlük kullansın → real-world feedback → Iter 30+ önceliklendirme.

---

## 📍 Şu Anki Sistem Durumu

### Repo

| | |
|---|---|
| **Local** | `/Users/agent9/Desktop/bnsp-repo/` |
| **Remote** | `https://github.com/bengisusengul/begumnaz-program.git` |
| **Deploy** | https://bengisusengul.github.io/begumnaz-program/ (GitHub Pages) |
| **Branch** | `main` (origin/main 1 commit gerisi) |
| **PWA file** | `index.html` (9912 satır, ~688 KB) |
| **SW cache** | `begumnaz-v7-no-hacettepe-2026-05-12` |
| **Manifest** | `manifest.json` — Begümnaz branding |
| **Bg image** | `bg.jpeg` |

> **DİKKAT**: macOS case-insensitive FS yüzünden `Begumnaz-program` (raw materyal Desktop'ta) ile `begumnaz-program` (repo adı) çakışıyordu. Çözüm: local repo klasör adı `bnsp-repo`, GitHub repo adı `begumnaz-program`.

### Faz Durumu

- ✅ **Faz 1**: Markdown dokümantasyon iskeleti (tamamlandı)
- ✅ **Faz 2**: PWA içerik adaptasyonu (Iter 18'de bitti — büyük temizlikler + cheetah hero)
- ✅ **Faz 3**: Deploy LIVE (GitHub Pages + Cloudflare Worker AI proxy — Iter 19'da tamamlandı)
- 🟢 **Faz 4**: PWA üretim olgunluğu (Iter 20-29 tamam, %90+ · sadece Iter 30 i18n EN çeviri sonraki oturuma)

---

## 📜 Bu Oturumda Yapılanlar (13 Mayıs 2026)

### Iter 30A — i18n EN Dashboard bilingual (M1 phase 1)

**Kullanıcı raporu**: Screenshot — EN seçildiğinde sadece nav çevriliyordu. Sayfa içeriği TR kalıyordu (Tünaydın, Sıradaki 3 Aksiyon, Öğle Yemeği, Hatırlatmalar vs.). Plan'da Iter 30 sonraki oturuma erteliydi, kullanıcı sorunu net gösterince **bu oturumda 30A** başlatıldı (görünür Dashboard).

**I18N obje genişletildi**: 27 key → 70+ key (TR + EN)

**Yeni key'ler (30+ ekleme)**:
- Dashboard ana: `next_3_actions`, `reminders`, `no_cycle_tracking`, `default_zen`, `compassion_today`, `compassion_loading`
- Greeting full: `greet_morning_full`, `greet_noon_full`, `greet_evening_full`, `greet_night_full` (Begümnaz adıyla)
- Cycle: `period_day` (Regl/Period), `cycle_day` (Gün/Day)
- Hero card actions: 16 key — `act_oil_pulling`, `act_sabah_ac`, `act_breakfast`, `act_lugol`, `act_lunch`, `act_snack`, `act_pre_wo`, `act_ikindi`, `act_dinner`, `act_footbath`, `act_tea`, `act_skin`, `act_probiotic`, `act_bed` + her birinin `_d` (detay) eşi
- Time labels: `time_acikma`, `time_pre_wo`
- Special: `pzt_extra` (Pazartesi Colewinde Vit D notu)

**Bilingual yapılan kod yerleri**:
- `renderHeroCard()` (3897+): greeting + 4 mode'un nextActions array'i tamamen t() ile bağlandı
- `cycleLine`: "Gün X · Regl" → "Day X · Period" (EN'de)
- `actionsHtml` boş durum: "Şu an aktif aksiyon yok..." → "No active action right now..."
- `nextLabel`: "⏰ Sıradaki N aksiyon" → "⏰ Next N action(s)"
- `phaseLine` (renderDashboard): "Döngü takibi yok" → "No cycle tracking"
- ZEN default fallback: "Bugün senin günün." → "Today is yours."
- `renderMorningCompassion`: "Bugün Begümnaz için" → "For Begümnaz today"
- HTML "Hatırlatmalar" span'a `data-i18n="reminders"` eklendi (applyTranslations() otomatik çevirir)

**SW cache bump**: `v17-dinamik-tema-ai` → **`v18-i18n-dashboard`**

**Kalan iş (Iter 30B + 30C sonraki oturum)**:
- 30B: WEEKLY_FOCUS_TEXTS (3432-3550, 6 cycle phase × 9 alt başlık = 50+ string) bilingual; ZEN obje (28 mesaj × 4 phase) bilingual; BODY_INTENTIONS bilingual; renderMorningCompassion fallback array'i EN versiyonu
- 30C: Diet sekmesi (Custom Food, makro grid, recipe modal), Cycle sekmesi (mood pills, body conv prompt), Exercise sekmesi (set log, RPE), Skin sekmesi (rotation labels), Medical sekmesi başlıkları; AI prompt'ları getLang() bazlı dinamik dil (Claude EN için yanıtlar)

**Bu Iter'ın etkisi**: Begümnaz EN seçtiğinde Dashboard (Today sekmesi — ana sayfa) tamamen EN gözükür. Diğer sekmeler hala karışık (Iter 30B/30C için). Ana kullanım akışı (Today + Settings + nav) artık tutarlı.

---

### Iter 29 — AI-assisted dinamik tema (M12) — Begümnaz görseli paleti belirler

**Kullanıcı isteği**: "Begümnaz beğendiği bir referans görseli yüklesin, tüm program o renklere bürünsün. Kendi isteğiyle, benim müdahalem olmasa bile programın rengini değiştirebilsin."

**Yeni Settings UI** (1753): `🎨 Tema` slbl + `<div id="theme-card"></div>` (Profiller'in üstünde)

**Yeni fonksiyonlar (Iter 29 bloğu)**:
- `THEME_VAR_KEYS` — 6 anahtar CSS variable adı (`bg-deep`, `bg-pink`, `cream`, `gold`, `coral`, `sage`)
- `THEME_DEFAULTS` — varsayılan hex'ler (Iter 9 cheetah pembe-bordo paleti)
- `getCustomTheme()` / `saveCustomTheme()` / `clearCustomTheme()` — localStorage `custom_theme`
- `applyThemeColors(colors)` — `document.documentElement.style.setProperty('--XXX', hex)` runtime injection
- `revertToDefaultTheme()` — variable'ları removeProperty + localStorage clear
- `loadSavedTheme()` — sayfa yüklenince custom_theme varsa otomatik uygula (DOMContentLoaded)
- `handleThemeImageUpload(input)` async — file → base64 + media_type → Claude vision API (Cloudflare proxy üzerinden)
- `applyPendingTheme()` / `cancelPendingTheme()` — preview onay/iptal

**Claude vision prompt**:
- Görsel + 6 renk istek (bg-deep, bg-pink, cream, gold, coral, sage)
- "Pembe-bordo-cream-gold ana paletinden çok uzaklaşma — sıcak, kadınsı, sağlık temalı kalsın"
- JSON dönüş: `{name: "Cheetah Sunset", colors: {...}}`
- claude-haiku-4-5-20251001 (vision destekli) · max 400 token

**UX akışı**:
1. Settings → 🎨 Tema → "📷 Görsel Yükle" (drag/drop-style label, dashed border)
2. JPG/PNG yükle (max 5 MB)
3. "✨ Claude renkleri analiz ediyor..." loading
4. 6 renk swatch + hex kod + tema adı preview
5. **✓ Uygula** → CSS variables runtime inject + localStorage save → toast "🎨 Tema uygulandı"
6. **İptal** → preview kapanır, mevcut tema kalır
7. Aktif tema kartında "🎨 [Tema adı] · varsayılana dön" linki

**Inline hex sınırı**: Iter 9-24 ana CSS variables (`--bg-deep`, `--bg-pink`, vb.) ile renklendirildi. Inline `style="color:#XXX"` (244 yer) variable kullanmıyor — tema değişiminde bazı yerler hardcoded kalır. Iter 24 ana modal/nav'ı standardize etti. Dinamik tema **CSS variable kullanan tüm yerleri** değiştirir; inline hex'ler statik kalır (gelecek Iter'da CSS var'a çevrilebilir).

**Cost**: Görsel yükleme 1x AI çağrı/değişim. Begümnaz tema değiştirdiğinde haiku-vision ~$0.005/çağrı. Aylık 5-10 değişiklik → ~$0.05/ay.

**SW cache bump**: `v16-sabah-merhamet-ai` → **`v17-dinamik-tema-ai`**

**Önem**: Begümnaz'ın programatik özerklik kazandığı kritik feature. Programın görsel kimliği artık SADECE ablanın kararı değil — Begümnaz istediği renge geçebilir. Kullanıcının özgün isteği (madde 12) tam karşılığa kavuştu.

---

### Iter 28 — AI-assisted sabah merhamet mesajı (M2)

**Hedef**: Her sabah PWA ilk açılışta Begümnaz'a **kişisel merhamet/güzellik mesajı**. Kullanıcı söyledi: "kendine merhameti artırmak en önemli". Dünyanın en güzel/akıllı/zeki/başarılı/merhametli kadını teması — klişe olmadan içtenliklі.

**Yeni HTML** (1399): `<div id="morning-compassion-card"></div>` (hero-card'ın üstüne)

**Yeni fonksiyonlar** (Iter 28 bloğu):
- `MORNING_FALLBACK_MESSAGES[]` — 20 sabit mesaj. Begümnaz profiline özgü (post-iso, endo, hassas cilt, hormonal akne); tema: beden olumlama + kendine merhamet + güzellik + akıllılık + samimi. Klişe yok. Örnek: "Cildin uzun yolda. Her hafta biraz daha onarılıyor — gözle görülmese de. Sen güçlüsün."
- `getMorningMessageCacheKey()` — `morning_message_YYYY-MM-DD`
- `getCachedMorningMessage()` — localStorage cache okuma
- `getRandomFallbackMessage()` — fallback array'den random
- `fetchAIMorningMessage()` async — Claude API (Cloudflare proxy üzerinden), context: cycle phase + endo flare durumu + saat. Prompt: 1-2 cümle, sıcak, kendine şefkat, "Merhaba/Günaydın" kalıbı YOK. claude-haiku-4-5-20251001 · max 200 token. Fallback'e düşme: API hata → random fallback.
- `renderMorningCompassion()` async — saat kontrolü (5-11 sabah) + Pazar özel kart çakışma kontrolü + cache → varsa direkt göster, yoksa fallback ile hemen render + AI çağrısı asenkron (proxy URL veya API key varsa). AI cevap gelince kart güncellenir.
- `renderMorningCompassionContent()` — pembe-bordo gradient kart, Playfair Display italic, ✨/💛 emoji badge ("Bugün Begümnaz için"), loading hint.

**renderDashboard çağrı** (3273 öncesi): `renderMorningCompassion();` eklendi (renderHeroCard'dan önce).

**localStorage**: `morning_message_${YYYY-MM-DD}` = `{text, source: 'ai'|'fallback', generated_at, error?}` — günde 1 AI çağrısı, sonraki açılışlarda cache.

**Cost tahmini**: 30 sabah × 1 çağrı × ~200 token (haiku ~$0.001/çağrı) = **~$0.03/ay**. Cloudflare proxy üzerinden, API key client'ta değil.

**SW cache bump**: `v15-regl-onboarding` → **`v16-sabah-merhamet-ai`**

**UX akışı**:
1. Begümnaz sabah 5-11 arası PWA'yı açar
2. Dashboard'da en üstte 💛 kart hemen görünür (random fallback)
3. AI çağrısı arkaplanda çalışır (proxy LIVE — Iter 19)
4. AI cevap gelince kart güncellenir (✨ etiketi)
5. Aynı gün tekrar açılırsa cache'ten gönderilir (yeni AI çağrısı yok)

**Önem**: Begümnaz'ın günü Claude'un kişisel selamlamasıyla başlar. Cycle phase + endo flare context'i AI'ya verildiği için mesaj her gün farklı + duruma uygun. Kullanıcının "kendine merhameti artırma" hedefi PWA'da somut karşılığa kavuştu.

---

### Iter 27 — Regl tahmin onboarding (M8)

**Mevcut**: `renderCyPredictions()` (9263) — kullanıcı regl eklemediyse `cy-pred-card` gizlendi. Boş gösterim.

**Yeni**: Boş durumda **onboarding placeholder** render edilir:
- 🌸 emoji + "Tahminler henüz hazır değil" Playfair Display başlık
- Açıklama: "İlk regl başlangıç tarihini ekle — sonraki regl, ovulasyon, fertil pencere, PMS dönemi otomatik tahmin edilir. 2+ kayıt sonrası median'a göre netleşir."
- **📅 Regl Ekle** butonu → mevcut `cy-start-input` formuna scroll + focus
- Alt not: "Tüm veriler yalnızca bu cihazda · Bengisu seed verisi yok (Iter 12)"

**Önem**: Begümnaz PWA'yı ilk açtığında tahmin kartı boş değil, cazip onboarding görür. Iter 12'de Bengisu period seed disabled edildi — onboarding yeni kullanıcıya kullanım kılavuzu sunuyor.

**SW cache bump**: `v14-mobile-overflow-fix` → **`v15-regl-onboarding`**

---

### Iter 26 — Egzersiz video linkleri (atlandı, ek not)

**Durum**: Plan'da search URL → direct watch URL upgrade öngörüldü.

**Bulgu**: PWA'da `YT_MAP` zaten direct watch URL kullanıyor (renderExDay içinde `gifImg.onclick = window.open('https://www.youtube.com/watch?v='+ytId)`). Yani PWA tarafı CALIŞIYOR — kullanıcı GIF tıkladığında direct video açılır.

**md dosyaları** (AGIRLIK-GUNLERI-DETAY.md, PELVIK-TABAN-VIDEOLARI.md): 19 search URL ve 7 kanal adı içeriyor. Search URL'ler çalışıyor (YouTube her zaman search yapar) ama "hangi video" kullanıcı seçimine bağlı.

**Karar**: Spesifik direct watch URL'leri için kullanıcı feedback gerekli (Begümnaz hangi videoları beğenir?). Iter 26 **atlandı**, gelecek Iter'da kullanıcı önerileriyle güncellenir. PWA tarafı zaten optimal.

---

### Iter 25 — Mobile responsive proaktif tasma koruması (M3)

Kullanıcı spesifik tasma raporu yoktu — Iter 25 **proaktif preventive** fix'leri ekledi (Begümnaz mobile'da kullanmaya başlayınca olası bug'ları önleme).

**Global koruma**:
- `*{...overflow-wrap:anywhere;}` — uzun string'ler (URL, kelimeler) otomatik sarılır, container'dan taşmaz
- `html,body{...overflow-x:hidden;}` — sayfa düzeyi yatay scroll engeli
- `body{...max-width:100vw;}` — viewport sınırı garanti

**Yeni media query** (≤360px küçük ekranlar — iPhone SE 1st gen, eski Android):
- `body{font-size:14px;}` — temel font küçültme
- `.card,.bx-card,.al-card,.micro-card{padding-left:14px;padding-right:14px;}` — kart iç padding daraltma
- `.topbar{padding-left:12px;padding-right:12px;}` — topbar kompakt

**Mevcut media query'ler korundu**:
- 360px (.nb nav button)
- 380px (.water-cup, .bulk-row)
- Touch target ≥44px (.btn, .meal-check, .flow-chip, .symp-chip, .scale-btn) — mevcut, dokunulmadı
- iOS safe-area-inset-bottom (`env()`) — mevcut, dokunulmadı

**SW cache bump**: `v13-renk-paleti-bordo` → **`v14-mobile-overflow-fix`**

**Test edilmemiş ama beklenen iyileşmeler**:
- Recipe modal'ında uzun food name'ler ellipsis yerine sarma
- Custom Food input'unda uzun yemek tarifleri taşma yok
- Settings modal alt scroll iOS Safari bottom bar ile çakışma korunur
- Bottom nav 360px'te daha az padding (mevcut), Now nav bar bordo (Iter 24)

**Kullanıcıya not**: Begümnaz mobile'da spesifik tasma yaşarsa screenshot paylaşsın → spot fix sonraki Iter'da.

---

### Iter 24 — Renk paleti tutarlılığı (M11)

PROGRESS Iter 9 (pembe/bordo Billie Eilish tema) sonrası bazı CSS class'ları **teal-blue** kalıntısı taşıyordu — eski Bengisu paletinden miras. Iter 24 ana modal + nav + uyarı kart paletini **bordo (rgba(110,26,40,...))** tonuna çekti.

**Değişen CSS class'ları**:

| Class | Eski | Yeni |
|---|---|---|
| `.bnav` (bottom nav, 200) | `rgba(15,65,71,0.78)` teal | `rgba(110,26,40,0.86)` bordo |
| `.modal` (407) | `rgba(15,65,71,0.92)` teal | `rgba(110,26,40,0.94)` bordo |
| `.pr-modal-content` (PR celebration modal, 913) | `linear-gradient(160deg,rgba(15,30,38,0.96),...)` teal-gold | `linear-gradient(160deg,rgba(110,26,40,0.96),...)` bordo-gold |
| `.mc-doctor` (1168) | `rgba(123,168,176,...)` blue-sage | `rgba(212,175,106,...)` gold |
| `.mc-doctor-title` (1169) | `rgba(123,168,176,0.95)` blue-sage | `rgba(232,178,63,0.95)` gold |

**Dokunulmayan teal kalıntılar** (küçük UI elementleri, görsel etki düşük):
- `.dash-stat`, `.set-log`, `.set-bottom-sheet`, `.rest-timer`, `.wd-ring-inner`, `.mh-silhouette` — `rgba(15,30,38,...)` (koyu teal-blue)
- Bu artıklar future Iter'da temizlenebilir; ana görsel kimlik artık bordo dominant.

**Önem**: Begümnaz PWA'sı şimdi tutarlı bordo-cream-gold paletinde. Iter 9 tema kararı (Billie Eilish + cheetah hero referansı) artık tüm modal/nav'da yansıyor.

**SW cache bump**: `v12-popup-x-btn` → **`v13-renk-paleti-bordo`**

---

### Iter 23 — Pop-up kapatma UX iyileştirme (M10)

**4 template modal'a sağ üst ✕ butonu eklendi**:
- `#glossary-modal` (2049)
- `#muscle-anatomy-modal` (2069)
- `#plate-modal` (2100)
- `#wedding-mirror-modal` (2120)

Her birinde mevcut "Kapat" butonu vardı, sağ üst X yoktu. Standart UX için 32×32 px circular X butonu eklendi (`position:absolute; top:10px; right:10px`). Başlıklara `padding-right:36px` eklenerek X butonunun başlık üzerine binmesi engellendi.

Diğer 10 modal'da Kapat butonu yeterli olduğu için dokunulmadı (over-engineering kaçınma).

**Toast auto-dismiss** (Explore raporundaki endişe):
- Mevcut `showToast()` (7954) zaten auto-dismiss yapıyor: success 3.5sn, normal/warn 2.2sn.
- Süre uygun — değişiklik yapılmadı.

**Kapatma yöntemleri (4 template modal için final)**:
- ✕ sağ üst butonu (YENİ)
- Alt "Kapat" butonu (mevcut)
- ESC tuşu (mevcut, global handler)
- Backdrop click (mevcut, global handler)

**SW cache bump**: `v11-supplement-birlesik` → **`v12-popup-x-btn`**

**Önem**: Kullanıcı dostluğu — özellikle mobile'da alt Kapat butonuna ulaşmak için scroll gerekebilir, sağ üst ✕ her zaman erişilebilir.

---

### Iter 22 — Beslenme + Supplement birleşik kart (M5)

Mikronutrient kartı (Diet sekmesi) ve doktor 16 ürün supplement protokolü ayrı yerlerde duruyordu (Dashboard'da timeline detay, Diet'te sadece 4 mikro). M5 hedefi: **TEK kart**ta birleştirmek.

**Yeni yapı (renderMicronutrientCard genişletildi)**:
- Kart adı değişti: "Mikronutrient Durumu" → **"Beslenme + Supplement Durumu"**
- **Üst yarı (mevcut)**: 4 mikro nutrient grid — C vit / K2 / Omega-3 / Lif
- **Orta yarı (YENİ)**: 💊 Bugünkü Supplement bölümü
  - **Progress bar** (taken/total) — gold→coral gradient, %ile görsel
  - **8 saat dilimi checkbox'ı** (her biri tıklanır):
    1. 🥥 08:00 Alkemist Oil Pulling
    2. ☀️ 08:30 Sabah AC (5 ürün: Akavital+Gül sirkesi+NADH+NAC+Bach)
    3. 💧 +2 saat Lugol iyot %5 (4 damla + Bach 2.)
    4. 💊 Kahvaltı tok (6 ürün + Pzt Colewinde D)
    5. 🍎 14:30 Ara + NAC (2.) + Bach (3.)
    6. 🕓 16:00 İkindi AC (Akavital + Gül sirkesi 2.)
    7. 🍲 17:30-19:00 Akşam (Anti turmeric + More than + Lifextra + Time Mg 2.)
    8. 🌙 22:00 Duobalance BV probiyotik
  - **"Sonraki" mesajı**: Şu an saatine göre upcoming slot vurgulanır (örn: "Sonraki: 14:30 · 🍎 Ara + NAC (2.) + Bach (3.)")
  - "Bugün tamam ✨" mesajı (hepsi alınınca)
- **Alt yarı (mevcut + güncel)**: ⚕️ Doktor sorusu paketi + bekleyen 3 soru hatırlatma

**Yeni fonksiyonlar**:
- `SUPPLEMENT_SLOTS` sabit array (8 dilim, key/emoji/saat/isim/içerik)
- `getSupplementLog()` — localStorage `supplement_log` parse (zaten BACKUP_KEYS'de)
- `setSupplementSlot(key, value)` — checkbox tıklanınca log güncelle + re-render
- `getTodaySupplementProgress()` — taken/total + upcoming slot hesabı (current time bazlı)

**localStorage**: `supplement_log` = `{YYYY-MM-DD: {oil_pulling: true, sabah_ac: false, ...}}`

**Hala Dashboard'da**: Detaylı timeline (saat saat, hangi ürün hangi zamanda, etkileşim notları, doktor onayı bekleyen flag'ler). Diet kart "Detaylı saat çizelgesi: Dashboard" yönlendirmesi yapar.

**SW cache bump**: `v10-cilt-mikronutrient-fix` → **`v11-supplement-birlesik`**

**Önem**: Begümnaz Diet sekmesini açtığında **tek bakışta** günün beslenme gap'i + supplement progress'i görür. Detay için Dashboard'a inebilir. Karar paralleli yokken takip kayboluyordu — şimdi her sekmede tutarlı view.

---

### Iter 21 — Cilt ürün listesi Begümnaz'a güncel + Mikronutrient Vit C Bengisu temizliği

**Cilt ürün listesi (M7) — KRİTİK BENGİSU KALINTISI TEMİZLENDİ**:
- `renderProds()` (~8800) tamamen yeniden yazıldı. **`skin-ultimate/URUN-LISTESI.md`** kaynak alındı.
- **Silinen Bengisu ürünleri**: Tea Tree Foaming Cleanser, Garnier BHA Cleanser, COSRX 6 Peptide, COSRX AHA/BHA Toner, Koreaco Brightening, Florence Bio Vit C, **The Ordinary Retinol 0.2%** (kritik yanlış — Begümnaz reçeteli tret kullanır), Medicube Collagen Jelly, Bioderma Atoderm, COSRX SPF, LRP Anthelios, COSRX Snail Eye
- **Silinen UK shop ref'leri**: Amazon UK, Boots/Superdrug, YesStyle/Stylevana — Begümnaz TR'de
- **Eklenen Begümnaz ürünleri** (URUN-LISTESI.md'den):
  - Temizleyici: Garnier Vit C Cleanser ✅ + Alınacak (CeraVe HC / Bioderma Sensibio / LRP Toleriane) 🛒
  - Serum sabah: ISANA Vit C 10% ✅ + ISANA Hyaluron+Panthenol ✅ + Niacinamide 10% 🛒
  - Aktif akşam: **Acnelyse 0.025% (tretinoin)** ✅ — Sal+Paz sandwich · ISANA AHA 6% ⚠️ · Azelaic acid 10% 🛒
  - Nemlendirici: Madescar (Centella) ✅ + Garnier Hyaluron Fresh ✅
  - SPF: Garnier BHA + Niacinamide SPF 50 ✅ (mecbur) + Purest Solutions BB ✅
  - Göz: ISANA Peptid Augencreme ✅ + ISANA Augencreme 0% ✅
  - Bırakıldı: ISANA Micellar Su ❌ (yakıyor)
- **Phase-aware emphasis güncellendi**: Regl→bariyer/hidrasyon, Ovulasyon→Vit C+niacinamide, Luteal→Madescar+SPF, Folliküler→tret+azelaic
- **TR shop fiyatları eklendi**: Eczane (CeraVe/Bioderma/LRP), Rossmann (ISANA), Trendyol (TO/COSRX), Watson's, Gratis
- **Status badge'leri**: ✅ kullan · ⚠️ dikkat · 🛒 alınacak · ❌ bırak
- **Alt info**: "🛒 Eklenecek 3 ürün ~700-1200 TL · 8 haftalık ekleme sırası" badge

**Mikronutrient (M5 ön-temizlik) — Bengisu kalıntısı tek cümle**:
- `renderMicronutrientCard()` (~5400) → Vit C action cümlesi:
  - Eski: "Demir emilimi 3-4× artırır (regl haftası kritik)" — Bengisu için yazılmış (demir emilimi Vit C ile). Begümnaz'da demir zaten yüksek (204), takviye yasak.
  - Yeni: "Antioksidan + kolajen sentezi (post-isotretinoin bariyer onarımı için kritik)" — Begümnaz protokolüne uygun (8 ay isotretinoin sonrası bariyer onarımı önceliği).

**SW cache bump**: `v9-cleanup-adaptive-bilim` → **`v10-cilt-mikronutrient-fix`**

**Önem**: Iter 17'de glossary tret tanımı düzeltildi (post-isotretinoin maddesi eklendi) ama PWA cilt sayfasındaki ürün listesi hala Bengisu'nun "The Ordinary Retinol" gösteriyordu. Iter 21 ile **tret protokol tutarlılığı sağlandı**: glossary, ürün listesi, PROGRESS.md, URUN-LISTESI.md hepsi Acnelyse 0.025% gösteriyor.

---

### Iter 20 — Faz 4 Cleanup: Adaptive Yük + Bilim Modu kaldırıldı

Faz 4 başlangıcı. Kullanıcı 13 maddelik iyileştirme listesi verdi (plan: `/Users/agent9/.claude/plans/hey-frolicking-journal.md`). Iter 20 ilk adım — kaldırılacak iki büyük modülü temizledi.

**Adaptive Yük (M4) — Apple Health entegrasyonu yok**:
- Silinen fonksiyonlar: `getReadinessScore()`, `generateAdaptiveRecommendation()`, `renderAdaptiveLoad()`, `askClaudeAdaptive()` (4 fn, ~165 satır)
- Silinen CSS: `.al-*` class'ları (~27 satır)
- Silinen HTML: `#e-adaptive-load` container + Phase 2 yorumu (2 satır)
- Düzelt: `renderEx()` caller'ı temizlendi (`.renderAdaptiveLoad()` çağrısı kaldırıldı)
- AI helper comment güncellendi

**Bilim Modu (M9) — Hacettepe Lab Iter 15'te gitmişti, geriye sadece L1/L2/L3 toggle kalmıştı**:
- `getEduLevel()` fonksiyonu sadeleştirildi: sabit `return 'L1';` (tüm `getEduLevel()!=='L1'` conditional'lar otomatik false → subtitle/tag/L3 görünmez)
- Silinen fns: `setEduLevel()`, `toggleEduLevel()`, `setEduLevelGlobal()`, `renderEduGlobalCard()`, `toggleExerciseEdu()`, `updateGlossModalLevel()` (6 fn)
- Silinen UI: Settings modal "🔬 Bilim Modu" kartı, Glossary modal "🔬 Bilim Modu Değiştir" butonu, Inline exercise edu accordion (chip + panel)
- Glossary L3 check sadeleştirildi: `l3Wrap.style.display='none'` her zaman (mevcut L3 metinleri kodda kalır, görünmez)
- `openSettingsModal()` comment güncel + `renderEduGlobalCard()` çağrısı temizlendi

**SW cache bump**: `v8-glossary-fix-2026-05-13` → **`v9-cleanup-adaptive-bilim-2026-05-13`**

**Metrikler**:
- index.html satır sayısı: 9912 → **9619** (-293 satır)
- 7 fonksiyon, 3 UI bloğu, 1 CSS bloğu silindi
- Hiçbir conditional render manuel temizlenmedi (getEduLevel sabit L1 olduğu için otomatik gizlendi)
- Kalan iş (sonraki Iter'lara): LEGEND_DEFS l3:'...' alanları (~50 maddede), CSS `.edu-*`/`.al-*` artıkları, BACKUP_KEYS'den `edu_level` çıkarma

**Önem**: PWA daha sade. Kullanıcı bilim modu toggle'ı kaybetmedi (Hacettepe Lab gitmiş, anlamsız kalmıştı). Adaptive Yük Apple Health bağlantısı olmadığı için boş duruyordu, kaldırma temiz.

---

### Iter 19 — Faz 3 LIVE: Cloudflare Worker AI proxy deploy + CORS fix

Büyük milestone — **Faz 3 tamamlandı**. PWA artık API key'i client'ta tutmuyor.

**Wrangler kurulum**:
- `brew install cloudflare-wrangler` (zsh path'inde brew yoktu) → `npm install -g wrangler` (Node zaten kurulu)
- Wrangler 4.90.1
- `wrangler login` → Cloudflare OAuth (tarayıcı auth)

**Worker projesi (`api-proxy/`)**:
- `api-proxy/wrangler.toml` — `name = "begumnaz-api-proxy"`, `main = "worker.js"`, `compatibility_date = "2024-01-01"`
- `api-proxy/worker.js` — `cloudflare-worker.js`'in kopyası (122 satır)
- `.gitignore` güncel — `api-proxy/.wrangler/`, `dist/`, `node_modules/`, `.dev.vars` dışlandı

**Cloudflare secrets** (3 adet, `wrangler secret put`):
- `ANTHROPIC_API_KEY` — Anthropic API key (sızıntı olayı: ilk key revoke + yenisi alındı, terminal history'de sızdı)
- `ALLOWED_ORIGINS` — `https://bengisusengul.github.io,http://localhost:8000`
- `AUTH_TOKEN` — `openssl rand -hex 24` ile rastgele 48-karakter

**Deploy**:
- `wrangler deploy` → `begumnaz.workers.dev` subdomain'i oluşturuldu (Cloudflare hesabı için kalıcı)
- Worker URL: **`https://begumnaz-api-proxy.begumnaz.workers.dev`**
- Version ID: `97ce35ad-6d64-4c45-a9ea-d5824f5d445d` (ilk deploy)

**Worker health check** (curl):
- OPTIONS preflight → HTTP/2 **204** ✓
- CORS headers → `access-control-allow-origin: https://bengisusengul.github.io` ✓
- GET / → 404 ✓ (sadece POST /v1/messages kabul)
- POST /v1/messages (auth + valid body) → 200 + "Tamam." cevap ✓

**CORS Bug + Fix**:
- PWA'da Test Et → "Failed to fetch" → Console: `Request header field anthropic-version is not allowed by Access-Control-Allow-Headers in preflight response`
- Curl çalışıyordu çünkü curl preflight göndermez (CORS sadece browser kuralı)
- Sebep: `callAnthropic()` browser-side fetch'i `anthropic-version` header'ı gönderiyor, Worker CORS allow-headers listesinde yoktu
- Fix: `cloudflare-worker.js` + `api-proxy/worker.js` → `'access-control-allow-headers': 'content-type, x-begumnaz-token, anthropic-version'`
- `wrangler deploy` (2. kez) → yeni Version

**PWA test (incognito window — preflight cache temiz)**:
- Settings → API Proxy → URL + Token gir → Kaydet → Test Et
- ✓ "Proxy çalışıyor · merhaba" toast
- Diyet → Custom Food → real yemek tahmini → AI cevap döndü ✓

**Önemli notlar (gelecek için)**:
- API key SIZINTI prevention: `wrangler secret put X` komutu çalıştırdıktan SONRA prompt geliyor — değeri komut satırına EKLEME, Enter'a basıp prompt sonrası yapıştır.
- Browser preflight cache 24 saat (`access-control-max-age: 86400`). Worker CORS değişikliği sonrası ana window'da değişiklik görmek için: DevTools → Network → Disable cache + reload.
- `cloudflare-worker.js` (ana repo) ve `api-proxy/worker.js` (deploy klasörü) iki ayrı dosya — değişiklik yaparken İKİSİNİ DE güncelle. Gelecek Iter'da symlink veya wrangler.toml `main = "../cloudflare-worker.js"` deneyebilir.

---

### Iter 18 — README cheetah hero + görsel iyileştirme

Faz 2 son temizlik kalemi: repo README görsel olarak çıplaktı, başlık metinden ibaretti.

**Eklenen**:
- `hero-image.jpeg` (208 KB, 736×1223, cheetah, JPEG) — `Begumnaz-program/gorseller/`'dan repo'ya kopyalandı (Iter 9'da CSS pembe/bordo teması için referans alınmıştı, şimdi README hero olarak da kullanılıyor).
- README başına `<p align="center"><img src="hero-image.jpeg" width="400"></p>` (HTML center, 400px width).
- Tema notu (blockquote): "Cheetah hero — gücün ve hassasiyetin birlikteliği. PWA pembe/bordo teması (Playfair Display, Billie Eilish ref) bu görselden esinlenildi."

**Yapılmayan** (gelecek Iter'a):
- PWA ekran görüntüleri (Dashboard/Cycle/Diet/Skin/Workout) — kullanıcının PWA'yı kendi cihazında açıp screenshot alması gerekecek.
- GitHub Pages deploy URL badge.

---

### Iter 17 — Glossary Bengisu kalıntıları temizliği + SW v8

PWA glossary'sinde (`LEGEND_DEFS`, satır 7280-7400 civarı) kapsamlı Bengisu kalıntıları bulundu — bazıları **yanlış tıbbi bilgi** içeriyordu. Iter 7'de "KAPSAMLI Bengisu temizliği" yapılmış olmasına rağmen glossary bölümü atlanmıştı.

**Silinen 4 glossary maddesi** (Begümnaz protokolünde yok):
- `calciday` — Kalsiyum karbonat efervesan (Bengisu E89.2 paratiroid yetersizliği için)
- `qalyviz` — Aktif D vit (Bengisu)
- `levotiroksin` — Sentetik T4 (Bengisu tiroidektomi için)
- `endo komplikasyonu` — Paratiroid yetersizliği (Bengisu E89.2)

**Yanlış tanım tamamen yeniden yazıldı**:
- `endometriozis` def: "Tiroid bezinin cerrahi alınması" ← TAMAMEN YANLIŞ TIBBİ BİLGİ. Doğru tanım: "Endometrium dokusunun uterus dışında bulunması" + Begümnaz context (Visanne tamamlandı, içerde kalan endo, bütüncül protokol, endo flare, süt+dana+tavuk yasak).

**Yanlış tıbbi cümleler temizlendi**:
- `t4` glossary'sinde `Lugol iyot (levotiroksin) sentetik T4` ← Lugol ≠ levotiroksin (Lugol potasyum iyot çözeltisi). Yerine: Begümnaz selenyum/iyot düşük → Lugol reçete bağlamı.
- `t4` l3'te `Total endometriozis sonrası life-long T4 replacement` cümlesi (Bengisu için).
- `tsh` def'te `Tiroidektomi sonrası replacement dozu` cümlesi. Yerine: Anti-TPO negatif → Hashimoto yok.
- `bmr` l3'te `Tiroidektomi T4 replacement uygunsa...` cümlesi. Yerine: Begümnaz T3 hafif yüksek → BMR hafif artmış.
- Satır 2614 yorum: `// Tiroidektomi: ≥35 minimum (post-thyroidectomy adjustment)` → `// EA ≥35 minimum (endo flare/post-isotretinoin adjustment)`.

**Yeni eklenen madde**:
- `post-isotretinoin` — Begümnaz için tam bağlamlı (8 ay × 40 mg Zoretanin etki etmedi, bariyer onarımı 12-24 ay, PIE/PIH/güneş lekeleri, tret 2x/hf sandwich, mezoterapi öncesi/sonrası 5 gün retinoid kes).

**Yapısal**:
- Bölüm başlığı `// ── Tıp/Tiroid (6) ──` → `// ── Tıp/Begümnaz (5) ──` (Bengisu silindi → madde sayısı eşleşti).

**SW cache bump**:
- `sw.js:4` → `begumnaz-v7-no-hacettepe-2026-05-12` → `begumnaz-v8-glossary-fix-2026-05-13` (eski cache invalide olacak, kullanıcı ilk açılışta yeni glossary'yi görür).

**Tıbbi önem**: Kullanıcı glossary kartlarını açtığında daha önce Bengisu'nun tiroidektomi geçmişine ait yanlış bilgilerle karşılaşıyordu. Özellikle "endometriozis = tiroidektomi" tanımı klinik açıdan kritik yanlış. Iter 17 ile glossary Begümnaz tıbbi profiline (post-isotretinoin + endometriozis + Anti-TPO negatif) tam uyumlu hale getirildi.

---

### Iter 16 — DEPLOY-API-PROXY.md path/origin fix

Faz 3 (Cloudflare Worker AI proxy deploy) öncesi tarama → `DEPLOY-API-PROXY.md`'de **3 tutarsızlık** bulundu ve düzeltildi:

| Satır | Eski | Yeni | Neden |
|---|---|---|---|
| 15 | `begumnazsengul.github.io` | `bengisusengul.github.io` | Origin açıklama metni |
| 39 | `cd ~/Desktop/begumnaz-program` | `cd ~/Desktop/bnsp-repo` | macOS case-insensitive FS path collision (PROGRESS.md "Kritik Hatırlanması Gerekenler"da belgeli) |
| 62 | `begumnazsengul.github.io,http://localhost:8000` | `bengisusengul.github.io,http://localhost:8000` | `ALLOWED_ORIGINS` secret değeri |

**Önem**: Rehberi takip eden kullanıcı Worker'ı yanlış konfigüre ederse origin kontrolü tüm AI çağrılarını 403 ile reddederdi. Faz 3 deploy'una geçmeden temizlendi.

`cloudflare-worker.js` satır 8'deki comment'te `bengisusengul.github.io` doğru yazılmış — sadece rehber tutarsızdı.

---

## 📜 Önceki Oturum (12 Mayıs 2026)

Bugünkü iterasyonlar **9-15 arası**. Önceki oturumlardan devralınan + bu oturumda eklenen:

### Iter 9 — Pembe/Bordo Tema (Billie Eilish + Cheetah ref)
- `hero-image.jpeg` (cheetah) + `fonts.jpg` referansından Begümnaz görsel kimliği
- CSS değişkenleri: cream/sage palette → pink/burgundy + mustard accent
- Font: Inter → **Playfair Display** (h1, h2, .hl-title vb.)

### Iter 10 — Diet sayfası temizlik + SUPPLEMENT_ALARMS
- Bengisu'dan kalan 4 alarm (Levotiron, Calciday vb.) → Begümnaz'ın 16 ürün protokolü
- Diet kartlarında cream-bg + cream-text kontrast sorunu ilk geçiş

### Iter 11 — Glossary + AI prompt Bengisu kalıntıları + JS apostrof fix
- `Begümnaz'da iyot düşük` → `Begümnaz iyot ölçümü` (apostrof JS string kırıyor)
- `KMY'yi etkileyebilir` → `kemik yoğunluğunu`
- AI prompt'larda kalan Hashimoto/post-tiroidektomi referansları temizlendi

### Iter 12 — fixPeriodData20260504 disabled
- Bengisu'nun period seed fonksiyonu her first-run'da `2026-04-28→2026-05-03` ekliyordu
- "1 regl kaydı yüklendi" screenshot → fonksiyon body `return;` yapıldı

### Iter 13 — Diyet kart kontrast agresif override
- `body[data-page="diyet"] .card *` → `color:#2A0E14 !important`
- Inline cream-text style'ları override etmek için son çare

### Iter 14 — "acıkmadan" → "acıkınca" semantik düzeltme
- Kullanıcı screenshot: "1. öğün — kahvaltı (acıkmadan)" = TR olarak yanlış (aç olmadan ye demek)
- 6 satır düzeltildi: topbar, diet section, JS comment, AI slotName, AI prompt, hero
- SW cache: v5-contrast → v6-acikinca

### Iter 15 — Hacettepe Lab tamamen kaldırıldı (bu oturumun son işi)
- Bengisu'nun "🧪 Bilim Modu L3" 4-tab modülü (Veri/Hipotez/PMID/Pedagoji)
- 342 satır silindi (CSS .hl-*/.hlab-* + HTML container + Toolkit butonu + openHacettepeLab + renderHacettepeLab tüm modülü + Bilim Modu L3 desc mention'ları)
- **İlk deneme başarısız** (Python script tek `skip` flag'i CSS+JS bloklarını paylaşıyordu, 3474 satır siliyordu) → `git checkout` ile geri alındı
- **İkinci deneme** (`/tmp/remove_hacettepe_v2.py`) — line-range tabanlı, 342 satır temiz silindi
- JS syntax breakage: `glossary'de` Türkçe apostrofu single-quoted JS string'i kırıyordu → `glossary kartında` ile değiştirildi
- SW cache: v6-acikinca → **v7-no-hacettepe**
- Commit `b2f5a98` (unpushed)

---

## 📋 Bekleyen Görevler

### Doktor cevabı bekleyen (Begümnaz son görüşmede sordu — abla iletecek)

1. **NADH dozu** — Şimdilik **1 tablet sabah AC** uygulanır (varsayım: 5-20 mg sublingual/tablet)
2. **NAC nasıl** — Şimdilik **2×500 mg (sabah AC + ikindi AC)** uygulanır. Doktor "tek sefer 1000 mg" derse o uygulamaya geçilir
3. **Probiyotik markası** — Duobalance BV Cran dışında alternatif var mı?

**KURAL**: Bu 3 cevap dışında **doktor protokolü dışına çıkılmaz**. Doktor 21.04.2026 kan panelini görerek 16 ürünlük protokolü yazdı. Bizim işimiz protokolün **uygulamasını optimize etmek** (saatler, etkileşim, beslenme + yaşam uyumu), ek supplement önermek değil.

### Yapılması düşünülen ama henüz açılmayanlar

- [ ] **Cloudflare Worker AI proxy deploy** — `cloudflare-worker.js` repo'da var ama deploy edilmedi. Begümnaz/abla kendi Anthropic API key girene kadar AI özellikleri (yemek analizi, cilt foto karşılaştırma, tarif üretimi) çalışmaz.
- [ ] **3 yeni cilt ürünü alışverişi** — Yumuşak temizleyici (CeraVe/Bioderma/LRP, 250-450 TL), Niacinamide serum 5-10% (TO/COSRX, 200-350 TL), Azelaic acid 10% (TO/Naturium, 250-450 TL). Bütçe ~700-1200 TL.
- [ ] **Itır yağı + Epsom tuzu** — Eczane/Aksu Vital'den. Ayak banyosu için.
- [ ] **iOS Safari "Ana ekrana ekle"** test — install + offline çalışma + manifest icon kontrolü
- [ ] **Doktor kontrol** — 6-8 hafta sonra Lugol başlangıcı sonrası TSH/T3/T4 tekrar
- [ ] **Pelvik-takip.md** — Her hafta yapılan pelvik taban video'sunun adı/link'i not edilmeli (tekrar engellemek için). `/Users/agent9/Desktop/Begumnaz-program/pelvik-takip.md` dosyası henüz yok, kullanıcı manuel ekleyebilir.

### Açık konular (kullanıcı yönlendirmeli)

- [ ] Begümnaz gym günü sabit olursa → tret günü konumlandırması yeniden yapılır (şu an Sal+Paz, gym günü sabitlenirse o güne yakın olmayan günlere kayar)
- [ ] Mezoterapi tekrar başlarsa → tret+azelaic protokolü 7-10 gün durur, sonra kademeli başlar
- [ ] Visanne tekrar başlarsa → Lugol iyot doktor onayı (etkileşim olabilir)

---

## ⚠️ Kritik Hatırlanması Gerekenler

### Kullanıcı kararları (değişmez)

1. **Repo public, her şey açık** (medical-documents/ dahil). Begümnaz onayı verildi. Sorumluluk ablada.
2. **AI özellikleri korunacak** (Bengisu gibi) — Anthropic API + Cloudflare Worker proxy
3. **Faz 1 markdown dokümantasyon source-of-truth** — `/Users/agent9/.claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md` plan dosyası ana kaynak. Repo SYNTHESIS dosyaları buradan üretilir.
4. **`Desktop/Begumnaz-program/` raw materyal arşivi** — repo'ya kopyalanan ham veriler burada, dokunulmaz
5. **PWA single-file** — `index.html` tek dosya yaklaşımı Bengisu'dan miras, korunuyor

### Begümnaz tıbbi profili (özet)

- **Tanılar**: Endometriozis (Visanne tamamlandı, içerde kalan endo arada şişlik yapıyor) · Post-isotretinoin (8 ay 40 mg Zoretanin etki etmedi) hassas cilt · Hormonal jawline akne · İdrar iyot düşük (27 µg/L) · Selenyum düşük (58 µg/L) · Serum demir yüksek (204) · T3 hafif yüksek · Anti-TPO **negatif** (Hashimoto **YOK**)
- **Cilt geçmişi**: 8 ay isotretinoin + 3× akne+scar mezoterapi (en yenisi 2 ay önce)
- **Doktor protokolü** (Mayıs 2026): 16 ürün — Akavital + Alkemist + Gül sirkesi + NAC + NADH + Anti turmeric + More than + Anti MM-12 + NBT Life Guard + Lifextra On Hepa + Time Mg + Lugol %5 + Colewinde + Benfolife + Duobalance BV Cran + Bach çiçekleri
- **Beslenme**: Mizaç temelli — yasaklar (pirinç, beyaz un, dana/tavuk, süt ürünü, salça, soğuk su, çay/kahve, patlıcan, yer fıstığı vb.) · izinli (kuzu/koyun/hindi 3x/hafta, pişmiş sebze, ancient grain ekmek, sıcak su 5 bardak)
- **Yaşam**: Ayak banyosu (4-5 damla ıtır + 2 yk Epsom) her gece 20:00-20:30 · Karın+bel+popo+ayak sıcak tutma · Itır yağı koklama gün içinde

### Programatik kural notları

- **Acnelyse 0.025% = tretinoin**, retinol DEĞİL (presciption retinoid) — daha güçlü, hassas ciltte 2x/hafta + sandwich tekniği
- **Anti-TPO negatif** → Hashimoto yok, Lugol güvenle başlatılabilir
- **CRP, KCFT, HbA1c normal** → sistemik durum sakin, protokol önleyici
- **Demir takviyesi YASAK** (serum demir 204, paradoks: ferritin 31.7 orta) → 3 ay sonra tekrar test, devam yüksekse HFE C282Y/H63D gen taraması doktor karar verir
- **İyot tedavisi başlangıcında selenyum eksikliği RİSK** — doktora soruldu (Bölüm 5.1 plan)

### Teknik notlar (kodlamada hatırlanması gereken)

- **Türkçe apostrof JS string'i kırıyor**: `Begümnaz'da`, `glossary'de`, `KMY'yi` gibi ifadeler `'...'` single-quoted JS string'inde olduğunda parse hatası → ya escape (`\'`) ya da apostrof'suz yeniden yazım
- **Card text contrast**: Diyet sayfasında inline cream-color style'lar problem yapıyor → `body[data-page="diyet"] .card *` aggressive override kullanıldı (Iter 13)
- **Service Worker cache busting**: Her büyük değişiklikte `CACHE_NAME` versiyonu bump'lanmalı (v7-no-hacettepe son), aksi halde kullanıcı eski versiyonu görmeye devam eder
- **Python script çoklu skip flag**: Tek `skip` değişkeniyle çoklu blok silme HATA (Iter 15 ilk deneme) → her blok için ayrı flag VEYA line-range tabanlı silme (sanity check'li)
- **Repo path collision**: Local repo `bnsp-repo`, GitHub repo adı `begumnaz-program`, raw arşiv `/Users/agent9/Desktop/Begumnaz-program/`. Karıştırma.

---

## 📂 Kritik Dosya Konumları

```
/Users/agent9/
├── .claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md  ← SOURCE OF TRUTH (plan)
├── .claude/projects/-Users-agent9-Desktop-Begumnaz-program/
│   └── memory/MEMORY.md  ← Auto-memory profile linkleri
└── Desktop/
    ├── Begumnaz-program/                  ← Raw materyal arşivi (dokunulmaz)
    │   ├── medical records/               (12 PDF kan testleri)
    │   ├── skin status/                   (cilt fotoğrafları + inuse-product)
    │   ├── body image/, period records/, supplements/, gorseller/
    │   ├── alisveris-listesi.{html,pdf,png}
    │   └── beslenme-ornegi-yasak-listesi.jpg
    └── bnsp-repo/                          ← GİT REPO (deploy edilen)
        ├── index.html                      (PWA — 9912 satır)
        ├── manifest.json, sw.js, cloudflare-worker.js, bg.jpeg
        ├── README.md, CLAUDE.md, PROGRESS.md (bu dosya), DEPLOY-API-PROXY.md, HEALTH_SHORTCUT.md, PWA-ADAPTATION-TODO.md
        ├── skin-ultimate/                  (SYNTHESIS + 3 agent)
        ├── supplements-ultimate/           (SYNTHESIS + 2 agent + photos/)
        ├── workout-ultimate/               (SYNTHESIS + 4 agent)
        ├── diet-ultimate/                  (SYNTHESIS + 3 agent)
        ├── lifestyle-ultimate/             (SAC-BAKIM dahil)
        └── medical-documents/              (KAN-DEGERLERI-TREND + kan-testleri/ + cilt-fotograflari/ + ...)
```

### Git çalışma dizini

`/Users/agent9/Desktop/bnsp-repo` — burada `git status`, `git push` çalıştırılır.

---

## 📊 Commit Geçmişi (24 commit · son 23 bu oturum + önceki iterasyonları)

```
3b469ad  Phase 1: Markdown dokümantasyon iskeleti tamamlandı
4fed444  Faz 2 Iter 1:  PWA dosyaları Bengisu'dan kopyalandı + ilk adaptasyon
d34ca2d  Faz 2 Iter 2:  Dashboard timeline tamamen Begümnaz protokolü
2790138  Faz 2 Iter 3:  Welcome modal + SUPPLEMENTS_INVENTORY + AI prompt temizliği
3b65723  Faz 2 Iter 4:  Diet rules + slot description mizaç temelli
530c739  Faz 2 Iter 5:  Doktor soruları + PDF özet + Bilim modalı temizlik
7532937  Faz 2 Iter 6:  Dashboard mode (sabah/öğlen/akşam/gece) nextActions Begümnaz
780d36b  Faz 2 Iter 7:  KAPSAMLI Bengisu temizliği — tüm referanslar kaldırıldı
76283af  Faz 2 Iter 8:  i18n TR/EN + Akıllı Ölçüm + Bengisu seed data temizliği
0621007  Faz 2 Iter 9:  Pembe & Bordo teması + Playfair Display (Billie Eilish ref)
0f84011  Faz 2 Iter 10: Diet sayfası Bengisu temizliği + SUPPLEMENT_ALARMS + kart kontrastı
ae9c213  Faz 2 Iter 11: Glossary + AI prompt Bengisu kalıntıları + JS apostrof fix
f95d2d7  Faz 2 Iter 12: fixPeriodData20260504 disabled (Bengisu period seed)
f224140  Faz 2 Iter 13: Diyet sayfası kart kontrastı — agresif text override
59bc99a  Faz 2 Iter 14: "acıkmadan" → "acıkınca" (Türkçe semantik düzeltme)
b2f5a98  Faz 2 Iter 15: Hacettepe Lab tamamen kaldırıldı — Bengisu kalıntısı  ⬅ UNPUSHED
aa2c4bf  PROGRESS.md kapsamlı yeniden yazıldı — oturum devamlılık dosyası  ⬅ UNPUSHED
c771a81  Faz 2 Iter 16: DEPLOY-API-PROXY.md path/origin tutarsızlık fix  ⬅ UNPUSHED
64f85bd  PROGRESS.md commit geçmişi listesi: Iter 16 + aa2c4bf eklendi  ⬅ UNPUSHED
a954ba4  Faz 2 Iter 17: Glossary Bengisu kalıntıları temizliği + SW v8  ⬅ UNPUSHED
a196a5f  PROGRESS.md commit geçmişi listesi: Iter 17 + 64f85bd eklendi  ⬅ UNPUSHED
6f3295a  Faz 2 Iter 18: README cheetah hero + görsel iyileştirme  ⬅ UNPUSHED
30cb616  PROGRESS.md commit geçmişi listesi: Iter 18 + a196a5f eklendi  ✅ pushed
59b53d4  Faz 3 LIVE Iter 19: Cloudflare Worker AI proxy deploy + CORS fix  ⬅ UNPUSHED
```

**Not**: UNPUSHED işaretleri 13 Mayıs 09:00 push öncesi durumu yansıtıyordu — 09:00 push'tan sonra `30cb616`'ya kadar tüm commit'ler origin'de. Sadece `59b53d4` (Iter 19) ve bu commit (follow-up) lokal.

---

## 🎯 Stratejik Sıra (yarın ve sonraki oturumlar için)

### Bugünden devralınan (öncelik sırası)

1. **`git push` Iter 15** (manuel — Claude izni kapalı)
2. **Deploy URL'de Hacettepe Lab gerçekten yok mu** kontrol (1 dk iş)
3. **Begümnaz iOS Safari install** (eğer henüz yapmadıysa) → ilk gerçek kullanım feedback'i
4. **Cilt 3 yeni ürün alışveriş** (~700-1200 TL bütçe) — Begümnaz başlayabilsin diye
5. **Itır + Epsom alımı** — bu gece ayak banyosuna başlamak için

### Faz 2 son temizlikler (kalmış küçük şeyler)

- [ ] **AI prompt'lar son tarama** — bilim modu fizyoloji prompt'unda Bengisu kalıntısı kalmış olabilir
- [ ] **Tooltip + glossary contrast pass** — Iter 13 sadece Diyet sayfasını çözdü, diğer sayfalarda kalan kart text-color sorunu olabilir (kullanıcı önceki screenshot'ta "hala okunmayan kısımlar var" demişti — tam çözülmedi)
- [ ] **Repo README görsel iyileştirme** — Hero image + screenshot ekleme

### Faz 3 (Deploy + Stabilizasyon)

- [ ] Cloudflare Worker AI proxy deploy (`DEPLOY-API-PROXY.md` rehberinden)
- [ ] Anthropic API key (Begümnaz/abla kendi) Worker'a koyma
- [ ] Apple Health iOS Shortcut (`HEALTH_SHORTCUT.md` — opsiyonel, manuel input fallback var)
- [ ] Push notification (opsiyonel — sw.js base var)
- [ ] Begümnaz kullanım periyodu 1-2 hafta → ilk gerçek feedback iterasyonu

---

## 🔄 Bu Dosya Nasıl Güncellenir

Her oturumun sonunda **şunları güncelle**:
1. **Son güncelleme** tarihi
2. **Yarın ilk yapılacak** bölümü (yeni session başı için)
3. **Bu Oturumda Yapılanlar** altına yeni iter eklenir
4. **Commit Geçmişi** son commit hash'ı eklenir
5. **Bekleyen Görevler** içinde tamamlananları `~~strikethrough~~` ya da sil
6. **Kritik Hatırlanması Gerekenler** bölümü değişen kararlarda güncellenir

Yarın açılan oturum:
1. **Bu dosyayı oku** (kullanıcı yönlendirir veya auto-context surface eder)
2. "Yarın ilk yapılacak" bölümünden başla
3. Yeni iterasyon başlarken commit'i tamamla, SW cache bump'la, bu dosyaya not düş
