# DESIGN.md: IELTS Cambridge Test Hub

Status: arah "Lembar skor", disusun dari riset (audit `anti-slop/audit-001-2026-10-31.md`) dan disetujui pemilik pada 31 Okt 2026 ("semua"). File ini sumber kebenaran tampilan hub.

Design Read: pelacak latihan pribadi untuk satu calon peserta IELTS yang mengejar target band, bergaya lembar skor cetak (tabel rapat, angka band tebal, satu warna tinta), dial ENERGY 1 / RHYTHM 2 / MOTION 1.

Dial: ENERGY 1 / RHYTHM 2 / MOTION 1

## Dasar riset (kenapa bentuknya begini)

1. **Goal-gradient effect**: usaha naik saat tujuan terasa dekat dan terlihat. Karena itu, angka utama adalah selisih ke target band dan progres buku yang sedang berjalan (16 sesi), bukan "x / 336".
2. **Planner IELTS** yang ada berpusat pada band sekarang vs target per skill dan memprioritaskan skill terlemah. Bagian atas hub mengikuti pola itu.
3. **Tabel data**: angka rata kanan dengan tabular figures, header mengikuti perataan kolomnya, tanpa sel rata tengah, dan lebar kolom mengikuti isi.
4. **Streak dan heatmap kalender tidak dipakai.** Bukti manfaatnya lemah (klaim vendor), dan streak yang putus justru menurunkan motivasi.
5. **Band adalah data berurutan**, jadi diberi skala satu warna dari terang ke gelap, bukan warna kategori.

## Karakter

- Lembar kerja, bukan halaman produk. Setiap elemen membuka tes, mencatat hasil, atau menunjukkan jarak ke target.
- Kertas dan tinta: latar netral hangat dan teks hampir hitam. Garis tipis memisahkan baris seperti lembar skor.
- Hanya angka jujur: semua angka berasal dari data tautan terverifikasi atau skor milik pengguna.

## Fokus, aksen, motif

- **Fokus layar:** tabel "Skill summary" di atas, dengan kolom selesai, rata-rata band, target, selisih, dan tes berikutnya.
  - Skill dengan selisih terbesar ke target diberi label "Priority".
  - Hanya tombol "Open test" di baris itu yang berwarna penuh.
- **Satu aksen:** biru tinta, terang `#24408f`, gelap `#a9bdf2`. Dipakai untuk:
  - tombol utama;
  - tautan sumber utama;
  - tanda selesai;
  - skala band.
  
  Tidak ada hijau "selesai" terpisah.
- **Motif identitas:** angka band tebal tabular (`6.5`, `7.0`). Bentuknya sama di ringkasan, baris, dan peta buku.
- **Progres buku berjalan:** 16 kotak kecil (4 modul × 4 tes) di ringkasan. Ini tujuan dekat yang terlihat.

## Palet (netral + 1 aksen + skala band dari aksen yang sama)

| Peran | Terang | Gelap | Alasan |
|---|---|---|---|
| Latar / permukaan | `#f5f3ee` / `#fffdf9` | `#171613` / `#201f1b` | Netral hangat seperti kertas. Beda dari abu slate bawaan, dan nyaman untuk tabel panjang. |
| Tinta / teks redup | `#1d1c19` / `#5f5b53` | `#ece8df` / `#a8a296` | Teks redup tetap ≥ 5.3:1 di semua permukaan. |
| Garis / garis input | `#e2ddd2` / `#8c867a` | `#34322c` / `#7a756b` | Garis input ≥ 3:1 terhadap permukaan. |
| Aksen tinta | `#24408f`, lembut `#e8ecf6` | `#a9bdf2`, lembut `#1f2a45` | Satu warna untuk "lakukan ini" dan "sudah selesai". |
| Skala band (peta) | `#d3dbef` < 6 · `#8fa3d6` 6–6.5 · `#24408f` ≥ 7 · `#5f5b53` selesai tanpa skor | `#2a3556` · `#4c64a8` · `#a9bdf2` · `#4a463f` | Makin gelap makin tinggi. Setiap kotak juga mencetak band atau tanda, jadi warna tidak pernah menjadi satu-satunya sinyal. |
| Status (hanya keadaan, bukan dekorasi) | peringatan `#6b4410` di atas `#fbf1dc`, bahaya `#a3261b` | `#f3d9a4` di atas `#2b2212`, `#f2a69c` | Peringatan penyimpanan diblokir, dan tombol hapus semua progres. |

Semua pasangan teks sudah dicek ≥ 4.5:1 di kedua tema.

## Tipografi

- **Judul (h1, h2):** serif sistem (`Iowan Old Style, Palatino, Georgia`). Alasannya, buku Cambridge adalah buku cetak, dan serif memberi suara "lembar ujian" tanpa web font (hub harus jalan offline).
- **UI dan angka:** sans sistem. Angka memakai `tabular-nums` supaya kolom sejajar.
- Sentence case, tanpa label huruf kapital berjarak lebar.
- Bahasa UI: Inggris, kalimat pendek dan langsung (mis. "Open test", "0.5 to go", "Clear filters").

## Tata letak

- Satu kolom, lebar maksimum 1080px, dengan urutan berikut:
  1. header;
  2. Skill summary;
  3. toolbar;
  4. daftar atau peta;
  5. format tes;
  6. sumber resmi;
  7. cadangan data.
- **Ukuran kontrol:**
  - semua kontrol di toolbar setinggi 40px;
  - semua kontrol di dalam baris tabel setinggi 34px;
  - di layar sentuh atau HP, semuanya 44px.
  
  Satu tinggi per konteks, supaya semuanya sejajar.
- Select memakai chevron sendiri yang di tengah secara vertikal, dengan padding kanan untuk teks.
- **RHYTHM 2:** ringkasan berbentuk tabel skill, dan daftar berbentuk tabel tes per buku. Keduanya tabel tetapi berbeda kepadatan. Setiap grup buku punya bentuk yang sama supaya mata bisa langsung melompat ke nomor tes.
- **Tanpa kartu di dalam kartu.** Panel berbingkai 1px dengan radius 10px hanya membungkus satu tabel atau satu kelompok kontrol. Segmented switch memakai radius 8px, bukan pil.
- Bayangan hanya dipakai pada timer melayang, karena timer berada di atas konten.
- **HP (≤ 760px):**
  - tiap tes menjadi satu baris ringkas: nomor tes, sumber utama, skor, centang, dan tombol detail;
  - sumber lain, catatan, tanggal, dan timer dibuka lewat tombol detail;
  - peta buku menampilkan satu modul sekaligus dengan kotak 44px.

## Ikon dan simbol

- **Tanpa emoji.** Nama modul ditulis sebagai teks, karena teks sudah cukup membedakan.
- **Chevron SVG** dipakai untuk select dan tombol detail baris. Artinya "buka lebih banyak".
- **↗** setelah "book overview" menandai tautan ke situs lain di tab baru.
- **✓ dan •** di kotak peta berarti "Done, no band" dan "Opened".

## Gerak (MOTION 1)

- Hanya keadaan hover, ditekan, dan fokus. Tanpa transisi atau animasi masuk.
- Lompat ke baris memberi latar sorot statis selama 2 detik.
- Saat timer habis, timer berwarna merah dan berbunyi sekali, tanpa berdenyut.

## Keadaan

- **Kosong:**
  - filter yang tidak cocok menampilkan pesan dan tombol "Clear filters";
  - tanpa target, ringkasan menampilkan ajakan mengisi target;
  - tanpa skor, rata-rata tampil "–".
- **Memuat:** tidak perlu, karena semua data ada di file dan localStorage.
- **Galat:**
  - penyimpanan diblokir memunculkan peringatan tetap;
  - file impor yang tidak valid memunculkan alert;
  - gagal simpan memunculkan toast.
