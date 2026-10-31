# Tindak lanjut audit 001 (31 Okt 2026)

Disetujui: semua nomor (1–10, termasuk 5b). Semua sudah dikerjakan.

| No | Status | Yang diubah |
|---|---|---|
| 1 | Selesai | Di HP, tiap tes kini satu baris setinggi 57px (sebelumnya ±260px), dan tinggi halaman turun dari ±22.000px menjadi ±8.400px. Sumber lain, catatan, dan timer pindah ke balik tombol panah. Label urutan dipendekkan menjadi "C21 ke C1". |
| 2 | Selesai | `DESIGN.md` ditulis ulang dengan arah "Lembar skor" berdasarkan riset. Dial ENERGY 1 / RHYTHM 2 / MOTION 1. |
| 3 | Selesai | Kartu "Lanjutkan latihan" dan 6 kartu statistik diganti satu tabel Ringkasan skill. |
| 4 | Selesai | Semua emoji dihapus. Tombol timer kini berlabel teks "Timer 30 mnt". |
| 5 | Selesai | Kontrol toolbar semuanya 40px, kontrol di baris tabel 34px, dan semuanya 44px di HP. Tombol Hapus kini berbingkai dan pindah ke bagian Cadangan data. |
| 5b | Selesai | Select memakai `appearance:none` dengan chevron SVG di `right 12px center` dan padding kanan 34px. |
| 6 | Selesai | Angka rata kanan dengan tabular figures, header mengikuti kolomnya, dan kolom menyesuaikan isi. Nama buku tidak lagi diulang di setiap baris. |
| 7 | Selesai | Label kolom dibedakan: "Benar /40 · band" untuk Listening/Reading, "Band (nilai sendiri)" untuk Writing/Speaking. Keterangan rata-rata kini "dari 2 tes". Intro ditulis ulang. |
| 8 | Selesai | Identitas baru: palet kertas dan tinta, judul serif, dan angka band tebal sebagai motif. |
| 9 | Selesai | Target band per skill dan overall disimpan di `prefs.targets`, dengan kolom Selisih dan label Prioritas. Format kunci progres tidak berubah. |
| 10 | Selesai | "Buku berjalan: C21 · x dari 16 sesi" dengan 16 kotak (L/R/W/S × 4 tes). |

## Delivery Gate

Bukti berasal dari headless Chrome (puppeteer), dijalankan di tema terang dan gelap, lebar 1280px dan 390px.

### Block 1: Hard Gate

- **R-02 PASS:** `grep "—"` menghasilkan 0 di index.html, README, AGENTS, dan DESIGN.
- **R-03 PASS:** tanpa scroll horizontal di 390px pada kedua tema. Target sentuh di bawah 44px: 0 (daftar dan peta, kedua tema).
- **R-17, R-36, R-38 PASS:** semua angka dihitung dari data tautan atau progres pengguna. Tidak ada klaim.
- **R-18, R-28 PASS:** tidak ada testimoni dan tidak ada FAQ.
- **R-23 PASS:** tidak ada logo, avatar, atau aset baru.
- **R-24, R-26 PASS:** setiap tombol punya aksi, dan setiap tautan menuju URL terverifikasi atau pencarian Google.
- **R-25 PASS:** pemindai kontras menemukan 0 kegagalan di 8 kombinasi (2 tema × 2 lebar × daftar/peta).
- **R-27 PASS:**
  - keadaan kosong: filter tanpa hasil, tanpa target, tanpa band;
  - keadaan galat: penyimpanan diblokir, file impor tidak valid, gagal simpan;
  - keadaan memuat tidak diperlukan karena semua data ada lokal.
- **R-32 PASS:**
  - `/` memfokuskan kolom cari, Escape mengosongkannya;
  - `1`–`4` mengganti modul, `M` mengganti daftar/peta;
  - fokus terlihat lewat `:focus-visible` dengan outline 2px.
- **R-33 PASS:** fitur ditulis langsung di source. Skrip di scratchpad hanya untuk merakit file sekali dan untuk pengujian.
- **R-34 PASS:** terang dan gelap sama-sama diuji, termasuk kontras, tata letak, dan chevron di kedua tema.
- **R-35 PASS:** klik-tembus yang tercatat:

  | Aksi | Hasil |
  |---|---|
  | Tab modul L/R/W/S | 84 baris tiap modul |
  | Isi 33 di Reading C20 T2 | band 7.5, otomatis selesai, fokus tetap di baris |
  | Kotak peta W-20-1 | pindah ke Writing, baris disorot, fokus di kolom band |
  | Tombol Tema | Sistem → Terang |
  | Timer baris | 59:59, Jeda/Mulai, preset 60 |
  | Filter C1–C9 + selesai | keadaan kosong dan tombol "Hapus filter", lalu kembali 84 baris |
  | Target L 7.0, R 6.0, O 7.0 | Prioritas di Listening, tombol utama di baris Listening, selisih "kurang 1.8 / tercapai / – / – / kurang 0.5" |
  | Muat ulang | target tetap tersimpan |
  | "C21 · Test 1" di ringkasan | lompat ke baris, fokus di kolom skor |
  | Tombol panah di HP | `aria-expanded=true`, catatan terlihat, isinya tersimpan setelah reload |

  Error JS: 0.
- **R-37 PASS:** `DESIGN.md` disetujui pemilik ("semua") dengan dial tertulis.
- **R-39 PASS:**
  - kontrol tanpa nama: 0;
  - `cursor:pointer` diset di lapisan dasar;
  - hover, ditekan, dan disabled dibedakan;
  - ada `lang`, `<title>`, landmark (header, nav, main, footer), satu h1;
  - zoom tidak diblokir.
- **R-40 PASS:** tidak ada gambar, video, atau skrip pihak ketiga. Performa tidak diukur.

### Block 2: Purpose-Gate

- **R-01:** tanpa gradien atau glow.
- **R-04:** hanya chevron (artinya buka lebih banyak), ↗ (tautan ke situs lain), serta ✓/• di peta (keadaan tanpa warna).
- **R-06:** serif untuk judul dengan alasan tertulis di DESIGN.md. Tidak ada label kapital berjarak lebar.
- **R-07:** tanpa pola latar.
- **R-08:** ↗ hanya di "ringkasan buku".
- **R-09:** satu tag "Prioritas", fungsional.
- **R-10, R-13:** tidak ada.
- **R-12:** bayangan hanya pada timer melayang, dengan alasan tertulis.
- **R-14:** tidak ada kartu fitur.
- **R-19:** tanpa animasi. Rotasi chevron hanya keadaan, tanpa transisi.
- **R-22:** tanpa ilustrasi.

### Block 3: Liveliness

- Dial tertulis (1/2/1), dan Design Read tertulis di DESIGN.md.
- Satu fokus: Ringkasan skill dengan satu tombol terisi.
- Satu aksen: biru tinta.
- Motif identitas: angka band tebal tabular, ditambah 16 kotak buku berjalan.
- RHYTHM 2 terpenuhi: tabel ringkasan dan tabel daftar punya kepadatan berbeda, sedangkan grup buku seragam secara sengaja.

### Block 4: Craftsmanship dan Quality Locks

- **R-05:** bukan template; susunannya mengikuti alur kerja (target → tes berikutnya → daftar).
- **R-11:** radius 10/8/7/5px berjenjang, tanpa pil.
- **R-15:** CTA spesifik ("Buka tes", "Export JSON", "Hapus semua progres").
- **R-16:** tanpa buzzword.
- **R-20:** palet kertas dan tinta dengan motif band.
- **R-21:** toggle tema bekerja di kedua mode.
- **R-29:** netral + 1 aksen, ditambah skala band dari aksen yang sama dan warna status.
- **R-30:** bukan tiruan produk lain.
- **R-31:** alasan setiap keputusan tertulis di DESIGN.md.

Hasil: semua PASS.
