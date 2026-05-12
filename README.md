# Begümnaz Program — Bütüncül Sağlık Takip Sistemi

Begümnaz için kişiselleştirilmiş haftalık sağlık programı. Endometriozis, post-isotretinoin hassas cilt, hormonal akne ve mizaç temelli bütüncül tıp protokolüne dayalı. Repo hem markdown dokümantasyon (multi-agent sentez) hem de PWA web uygulaması içerir.

## Tıbbi Bağlam

- Endometriozis (ameliyat sonrası Visanne tamamlandı; içerde kalan endo yan etki kontrolü için bütüncül tıp protokolü)
- Cilt: 8 ay × 40 mg isotretinoin (Zoretanin, etki etmedi) + 3× akne+scar mezoterapi → post-iso incelmiş bariyer
- Aktif: hormonal akne (yanak/çene/jawline), PIE (kırmızı izler), PIH (kahve), güneş lekeleri
- Saç: hızlı yağlanan kafa derisi + kuru uçlar paradoksu
- Kan paneli (21.04.2026): İyot düşük (27), Selenyum düşük (58), T3 hafif yüksek (4.20), Demir yüksek (204), B12 yüksek (738), Hashimoto negatif

## Klasör Yapısı

| Klasör | İçerik |
|---|---|
| [`skin-ultimate/`](skin-ultimate/) | Cilt sentezi + günlük rutin + haftalık aktif çizelge + tretinoin protokol + leke stratejisi + 3 ajan perspektifi |
| [`supplements-ultimate/`](supplements-ultimate/) | 16 ürün protokolü + saat çizelgesi + kan değerleri analizi + etkileşim uyarıları + 2 ajan perspektifi + ürün fotoğrafları |
| [`workout-ultimate/`](workout-ultimate/) | Haftalık şema (3 ağırlık + 2 pelvik taban + 2 pilates + 5-6 yürüyüş) + ev/dışarı/gym switch + döngüsel enerji + pelvik taban video havuzu + 4 ajan perspektifi |
| [`diet-ultimate/`](diet-ultimate/) | Mizaç temelli beslenme + günlük örnek + yasaklar/izinli liste + alışveriş görselleri + 3 ajan perspektifi |
| [`lifestyle-ultimate/`](lifestyle-ultimate/) | Ayak banyosu + sıcak vücut + ıtır aromaterapi + uyku + saç bakımı |
| [`medical-documents/`](medical-documents/) | Kan testleri, cilt fotoğrafları, vücut görselleri, period takip |

## PWA Uygulaması

`index.html` — tek dosyalık Progressive Web App. iOS Safari'de "Ana ekrana ekle" ile yüklenir.

**7 sekme**:
- **Dashboard** — Günün özeti
- **Cycle** — Period takip + endo flare farkındalık
- **Supplements** — 16 ürün saat çizelgesi + reminder
- **Diet** — Yemek logu + yasak/izinli + makro
- **Workout** — Egzersiz logu + döngüsel adaptasyon
- **Skin** — Cilt aktif takibi + tolerans + foto karşılaştırma
- **Measurements** — Kilo + vücut ölçü + kan değerleri trend

Veri `localStorage`'da. Anthropic API key ile AI özellikleri aktif olur.

## Kullanım

**Sadece dokümantasyon**: Markdown dosyaları GitHub'da veya local editor'de okunabilir.

**PWA olarak**: GitHub Pages deploy → tarayıcıda aç → iOS Safari → "Ana Ekrana Ekle".

## Doktor Görüşmesinde Bekleyen 3 Soru

1. NADH dozu (şimdilik 1 tablet sabah AC)
2. NAC tek/iki seferli mi (şimdilik 2x500 mg AC)
3. Probiyotik markası (Duobalance BV Cran dışında alternatif)

## Repo İlhamı

Yapı [Bengisu Program](https://github.com/bengisusengul/bengisu-program) reposundan ilham alınarak Begümnaz'ın tıbbi tablosuna uyarlandı. İçerik tamamen sıfırdan, Begümnaz'ın profili üzerinden.

---

**Son güncelleme**: 12 Mayıs 2026
