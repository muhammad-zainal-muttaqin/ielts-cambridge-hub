# DESIGN.md: IELTS Cambridge Test Hub

Status: arah "Lembar skor IELTS".
- Versi 1 (31 Okt 2026): biru tinta, disusun dari riset (audit `anti-slop/audit-001-2026-10-31.md`) dan disetujui pemilik.
- Versi 2 (2 Nov 2026): permintaan pemilik. Warna khas IELTS, UX lebih ramah untuk pengguna baru, panduan singkat, Help, dan disclaimer hak cipta.

File ini sumber kebenaran tampilan hub.

Design Read: pelacak latihan pribadi untuk calon peserta IELTS yang baru mulai memakai buku Cambridge, bergaya materi ujian IELTS (pita merah IELTS, indigo, permukaan putih, tabel rapat, angka band tebal di dalam kotak), dial ENERGY 2 / RHYTHM 2 / MOTION 1.

Dial: ENERGY 2 / RHYTHM 2 / MOTION 1

ENERGY naik dari 1 ke 2 karena pita merah di header dan kotak band menyapa lebih kuat. Bagian kerja tetap tenang.

## Dasar riset (kenapa bentuknya begini)

1. **Goal-gradient effect**: usaha naik saat tujuan terasa dekat dan terlihat. Karena itu, angka utama adalah selisih ke target band dan progres buku yang sedang berjalan (16 sesi), bukan "x / 336".
2. **Planner IELTS** yang ada berpusat pada band sekarang vs target per skill dan memprioritaskan skill terlemah. Bagian atas hub mengikuti pola itu.
3. **Tabel data**: angka rata kanan dengan tabular figures, header mengikuti perataan kolomnya, tanpa sel rata tengah, dan lebar kolom mengikuti isi.
4. **Streak dan heatmap kalender tidak dipakai.** Bukti manfaatnya lemah (klaim vendor), dan streak yang putus justru menurunkan motivasi.
5. **Band adalah data berurutan**, jadi diberi skala satu warna (indigo) dari terang ke gelap, bukan warna kategori.
6. **Warna khas IELTS.** Panduan merek mitra IELTS dari British Council (Maret 2025) menyebut dua warna latar: "IELTS Red" dan indigo. Situs ielts.org memakai `#e31837` sebagai warna tile. Nilai hex indigo resmi tidak dipublikasikan, jadi indigo di file ini dipilih sendiri.
7. **Logo IELTS tidak dipakai.** Merek IELTS milik IELTS Partners (British Council, IDP IELTS, Cambridge University Press & Assessment), dan pihak ketiga perlu izin untuk memakainya. Hub hanya memakai warna, bukan logo atau bentuk huruf logo.
8. **Pengguna baru butuh titik mulai.** Audit UX 2 Nov 2026 menemukan:
   - layar pertama penuh "–", "0/84", dan "Not set", tanpa petunjuk langkah pertama;
   - istilah tidak dijelaskan: C21, sesi, sumber utama, Engnovate, Gap, JSON;
   - cara mengisi skor tersembunyi di bagian bawah yang tertutup;
   - empat tombol "Open test" dan empat tombol Timer bersaing di ringkasan.

   Karena itu ada panel "Start here", dialog Help, dan satu kalimat bantu di setiap area kerja.

## Karakter

- Lembar kerja ujian, bukan halaman produk. Setiap elemen membuka tes, mencatat hasil, atau menunjukkan jarak ke target.
- Permukaan putih dan teks tinta, dengan pita merah IELTS di atas. Garis tipis memisahkan baris seperti lembar skor.
- Hanya angka jujur: semua angka berasal dari data tautan terverifikasi atau skor milik pengguna.
- Ramah untuk pengguna baru: setiap istilah dijelaskan di Help, dan setiap area kerja punya satu kalimat bantu.

## Fokus, aksen, motif

- **Fokus layar:**
  - Kunjungan pertama: panel "Start here". Tombol "Open" di panel itu satu-satunya tombol merah.
  - Setelah hasil pertama tercatat: tabel "Your progress". Skill dengan selisih terbesar ke target diberi label "Priority", dan hanya tombol "Open test" di baris itu yang merah penuh.
- **Dua warna inti, dengan peran berbeda:**
  - Merah IELTS untuk identitas dan aksi utama: pita header, satu tombol utama per layar, label Priority, dan tombol hapus.
  - Indigo untuk progres dan tautan: tautan sumber utama, tanda selesai, skala band, baris selesai, dan cincin fokus.
- **Motif identitas:** angka band tebal tabular di dalam kotak bergaris (`6.5`, `7.0`), seperti kotak skor di lembar ujian. Bentuknya sama di ringkasan, baris tes, dan peta buku.
- **Progres buku berjalan:** 16 kotak kecil (4 modul × 4 tes) di ringkasan. Ini tujuan dekat yang terlihat.

## Palet (netral + merah IELTS + indigo)

| Peran | Terang | Gelap | Alasan |
|---|---|---|---|
| Latar / permukaan | `#f4f4f7` / `#ffffff` | `#121119` / `#1b1a25` | Putih dan abu terang seperti materi IELTS. Versi gelap condong ke indigo. |
| Tinta / teks redup | `#1c1b26` / `#555466` | `#ecebf4` / `#a9a7bc` | Teks redup ≥ 6.2:1 di semua permukaan. |
| Garis / garis input | `#dfdee7` / `#8b899b` | `#2f2d3e` / `#77748c` | Garis input ≥ 3:1 terhadap latar dan permukaan. |
| Merah IELTS (pita, tombol utama) | `#e31837`, hover `#c41430` | `#c8102e`, hover `#a80d27` | Warna merek IELTS. Teks putih 4.72:1 (terang) dan 5.88:1 (gelap). Versi gelap lebih redup supaya tidak silau. |
| Teks merah (Priority, hapus) | `#b3122c` | `#ff8e9c` | ≥ 5.8:1 di semua permukaan, termasuk baris yang disorot. |
| Indigo (progres, tautan, fokus) | `#33298a`, lembut `#eceaf8` | `#b4adf6`, lembut `#262250` | Warna latar kedua merek IELTS. Teks indigo ≥ 7:1. |
| Skala band (peta) | `#dad6f3` < 6 · `#9d95dd` 6–6.5 · `#33298a` ≥ 7 · `#555466` selesai tanpa skor | `#2c2858` · `#5b50be` · `#b4adf6` · `#4a4859` | Makin gelap makin tinggi. Memakai indigo, bukan merah, supaya band tinggi tidak terbaca sebagai galat. Setiap kotak juga mencetak band atau tanda. |
| Status (hanya keadaan) | peringatan `#6b4410` di atas `#fbf1dc` | `#f3d9a4` di atas `#2b2212` | Peringatan saat penyimpanan browser diblokir. |

Semua pasangan teks sudah dicek dengan `contrast-check.py` (≥ 4.5:1 di kedua tema).

## Tipografi

- **Judul (h1, h2, h3):** serif sistem (`Iowan Old Style, Palatino, Georgia`). Alasannya, buku Cambridge adalah buku cetak, dan serif memberi suara "lembar ujian" tanpa web font (hub harus jalan offline).
- **UI dan angka:** sans sistem. Angka memakai `tabular-nums` supaya kolom sejajar.
- Sentence case, tanpa label huruf kapital berjarak lebar.
- Bahasa UI: Inggris, kalimat pendek dan langsung (mis. "Open test", "0.5 to go", "Clear filters").

## Tata letak

- Pita header merah selebar layar. Isinya judul, satu kalimat tujuan, serta tombol Help dan Theme.
- Di bawahnya satu kolom, lebar maksimum 1080px, dengan urutan berikut:
  1. panel "Start here" (hanya sampai hasil pertama tercatat, dan bisa disembunyikan);
  2. Your progress;
  3. toolbar;
  4. daftar atau peta, dengan satu kalimat bantu sesuai modul;
  5. format tes IELTS;
  6. sumber resmi;
  7. backup;
  8. footer: catatan tautan, "About this site", dan hak cipta.
- **Panel Start here:** tiga langkah karena proses nyatanya memang tiga: pilih target, buka tes, catat skor. Ini bukan template "How it works": setiap langkah punya kontrolnya sendiri, dan kotak centangnya terisi otomatis dari data.
- **Help:** dialog modal (`<dialog>`), ditutup dengan tombol Close atau Esc. Isinya cara kerja, arti istilah, tabel band, data Anda, pintasan keyboard, dan tentang situs ini.
- **Ukuran kontrol:**
  - semua kontrol di toolbar dan header setinggi 40px;
  - semua kontrol di dalam baris tabel setinggi 34px;
  - di layar sentuh atau HP, semuanya 44px.

  Satu tinggi per konteks, supaya semuanya sejajar.
- Select memakai chevron sendiri yang di tengah secara vertikal, dengan padding kanan untuk teks.
- **RHYTHM 2:** pita header, panel langkah, tabel skill, dan tabel tes per buku punya bentuk berbeda. Setiap grup buku punya bentuk yang sama supaya mata bisa langsung melompat ke nomor tes.
- **Tanpa kartu di dalam kartu.** Panel berbingkai 1px dengan radius 10px hanya membungkus satu tabel atau satu kelompok kontrol. Segmented switch memakai radius 8px, bukan pil.
- Bayangan hanya dipakai pada timer melayang dan dialog Help, karena keduanya berada di atas konten.
- **HP (≤ 760px):**
  - tombol header turun ke bawah judul;
  - tiap tes menjadi satu baris ringkas: nomor tes, sumber utama, skor, centang, dan tombol detail;
  - sumber lain, catatan, tanggal, dan timer dibuka lewat tombol detail;
  - peta buku menampilkan satu modul sekaligus dengan kotak 44px;
  - dialog Help hampir selebar layar dan bisa digulir.

## Ikon dan simbol

- **Tanpa emoji.** Nama modul ditulis sebagai teks, karena teks sudah cukup membedakan.
- **Chevron SVG** dipakai untuk select dan tombol detail baris. Artinya "buka lebih banyak".
- **↗** setelah "book overview" menandai tautan ke situs lain di tab baru.
- **✓ dan •** di kotak peta berarti "Done, no band" dan "Opened".
- **✓** di kotak langkah panel Start here berarti langkah itu selesai. Teksnya juga mengatakan "done" untuk pembaca layar.

## Gerak (MOTION 1)

- Hanya keadaan hover, ditekan, dan fokus. Tanpa transisi atau animasi masuk, termasuk saat dialog dibuka.
- Lompat ke baris memberi latar sorot statis selama 2 detik.
- Saat timer habis, timer berwarna merah dan berbunyi sekali, tanpa berdenyut.

## Keadaan

- **Kunjungan pertama:** panel Start here muncul sampai ada tes yang selesai, kecuali pengguna menyembunyikannya. Help bisa memunculkannya lagi.
- **Kosong:**
  - filter yang tidak cocok menampilkan pesan dan tombol "Clear filters";
  - tanpa target, ringkasan menampilkan ajakan mengisi target;
  - tanpa skor, rata-rata tampil "No score yet".
- **Memuat:** tidak perlu, karena semua data ada di file dan localStorage.
- **Galat:**
  - penyimpanan diblokir memunculkan peringatan tetap;
  - file backup yang tidak valid memunculkan alert;
  - gagal simpan memunculkan toast.

## Hak cipta dan disclaimer

Footer dan Help menyatakan fakta berikut, dengan kalimat yang sama:
- hub adalah alat belajar independen yang hanya menyusun tautan ke halaman di situs lain;
- hub tidak meng-host, menyalin, atau menyimpan soal, audio, kunci jawaban, atau buku;
- progres hanya tersimpan di browser pengguna, dan halaman tidak mengirimnya ke mana pun;
- buku dan tes Cambridge IELTS adalah hak cipta Cambridge University Press & Assessment;
- IELTS adalah merek dagang IELTS Partners;
- konten di situs tertaut milik situs tersebut dan pemegang haknya;
- hub tidak berafiliasi dengan, dan tidak didukung oleh, pihak-pihak tersebut.
