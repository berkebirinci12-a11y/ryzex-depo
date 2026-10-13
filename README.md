# 🎮 RyzexOs

**Oyun için tasarlanmış, tak-çalıştır Arch Linux tabanlı işletim sistemi.**
AMD Ryzen 5 5500 (Zen 3) + Radeon RX 6600 donanımı için özel derlenmiş ve optimize edilmiş.

## 📥 ISO Nasıl İndirilir

1. [Releases](https://github.com/berkebirinci12-a11y/ryzex-depo/releases/tag/stable) sayfasını açın
2. **"RyzexOs ISO"** bölümündeki indirme bağlantısına tıklayın (Gofile / Pixeldrain — hızlı ve ücretsiz)
3. `sha256` doğrulaması yapın
4. USB'ye yazın (Rufus / Ventoy / `dd`) ve önyükleyin

> ISO her güncellemede yenilenir — Releases sayfasındaki bağlantılar her zaman **en son sürümü** verir.

## ⚡ Performans

| Katman | Optimizasyon |
|---|---|
| **Çekirdek** | `linux-ryzex`: Zen 3 (MZEN3), BORE zamanlayıcı, Clang ThinLTO, HZ 1000, tam öncelikli, AutoFDO/PGO hazırlıklı |
| **Derleyici** | `-march=x86-64-v3 -mtune=znver3` + ince LTO — tüm paketler işlemciye özel |
| **Ekran kartı** | Mesa RADV znver3+LTO, GPL, `immediate` sunum, GPU sürekli yüksek saatte |
| **Bellek** | 12 GB zRAM + zstd (16 GB RAM ≈ 35 GB etkili), agresif takas |
| **Gecikme** | `mitigations=off`, spekülasyon azaltmaları derlemede kapalı, busy-poll ağ, watchdog yok |
| **Arka plan** | Baloo, CUPS, Bluetooth, fwupd, PackageKit, oomd... maskeli — oyuna giden her şey açık |

## 🔄 Güncelleme

```bash
sudo ryzexupdate
```
Animasyonlu güncelleme ekranı; sistem + sürücüler + Flatpak tek seferde.
Kurulu sistemler ve canlı USB oturumları bu depodan güncelleme alır.

## 🧪 PGO / AutoFDO (isteğe bağlı — donanımınıza özel derleme)

```bash
ryzex-pgo test          # 10 dk profil topla (veya: ryzex-pgo oyun -- ryzex-oyun steam)
# çıkan .perfdata dosyasını alın, sonra:
bash cekirdek/ryzex-cekirdek-derle.sh --autofdo <dosya>
```

## 🛠 Derleme

```bash
powershell -File baslat.ps1     # WSL üzerinden ISO üretimi (~2-3 saat)
bash yayin/ryzex-yayin.sh       # paketleri yayınla (çekirdek/mesa/ayarlar)
bash yayin/iso-yayin.sh         # ISO'yu doğrula + yayınla
```

## 📦 Depo

Paket deposu: [releases/tag/stable](https://github.com/berkebirinci12-a11y/ryzex-depo/releases/tag/stable)
```
[ryzex]
SigLevel = Optional TrustAll
Server = https://github.com/berkebirinci12-a11y/ryzex-depo/releases/download/stable
```

---
RyzexOs — Arch Linux üzerine inşa edilmiştir. GPL-3.0.