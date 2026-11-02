# AGENTS.md: IELTS Cambridge Test Hub

Hub tautan + pelacak progres latihan IELTS Cambridge.
Buka `index.html` → ikuti panel **Start here** (pilih target band, buka tes pertama, catat skor) → selanjutnya klik **Open test** (opsional: nyalakan Timer) → kerjakan di situs latihan → catat **jawaban benar/40 atau band** di hub (otomatis ditandai selesai). Tombol **Help** (atau `?`) menjelaskan semua istilah.
Semua teks UI (label, tombol, aria-label, toast, alert) berbahasa Inggris; dokumentasi repo tetap berbahasa Indonesia.

---

## 1. Prinsip teknis

1. Hub ini hanya menyimpan **tautan, status, skor, band, catatan, dan tanggal**. Konten tes tetap berada di situs sumber dan dibuka di tab baru.
2. Tautan langsung wajib dicek **HTTP 200** sebelum dimasukkan. Jika belum ada, gunakan tautan **Search** (query Google), jangan menebak URL.
3. Progres disimpan lokal di browser (`localStorage`), dengan **Download backup / Restore backup** (file JSON). Tidak ada server, dan halaman tidak boleh mengirim data atau memuat aset dari situs lain (tanpa `fetch`, skrip CDN, atau web font).
4. Jangan menautkan file PDF/audio unduhan; tautkan halaman latihan/penjelasan.
5. Jangan memakai logo IELTS atau logo situs sumber. Teks **About this site** (footer, disalin otomatis ke Help) wajib tetap sesuai fakta: hub hanya menyusun tautan, tidak meng-host atau menyimpan konten tes, progres hanya di browser, hak cipta buku milik Cambridge University Press & Assessment, IELTS merek dagang IELTS Partners, dan hub tidak berafiliasi. Jika fitur berubah (mis. ada server), perbarui teks itu, README, dan `DESIGN.md`.

---

## 2. Isi satu buku Cambridge IELTS Academic

Satu buku = **4 tes lengkap** (Test 1–4). Setiap tes terdiri dari 4 modul:

| Modul | Isi per tes | Durasi |
|---|---|---|
| Listening | 4 part · 40 soal (Part 1 percakapan sosial, Part 2 monolog sosial, Part 3 diskusi akademik, Part 4 kuliah) | ±30 menit (+10 menit transfer di paper / 2 menit review di computer) |
| Reading | 3 passage · 40 soal (T/F/NG, matching, MCQ, completion) | 60 menit |
| Writing | Task 1 (≥150 kata) + Task 2 (≥250 kata) | 60 menit (20 + 40) |
| Speaking | Part 1 wawancara, Part 2 cue card (1 menit persiapan + 2 menit bicara), Part 3 diskusi | 11–14 menit |

Buku juga memuat **kunci jawaban, transkrip Listening, contoh jawaban Writing**, dan audio (CD atau kode unduhan di edisi baru).
**Jadi 1 buku = 4 tes × 4 modul = 16 sesi latihan.**

---

## 3. Cakupan hub

| Cakupan | Buku | Baris (buku × 4 tes × 4 modul) |
|---|---|---|
| Sekarang | C1–C21 (21 buku) | **336** |

Tautan langsung terverifikasi (HTTP 200, 31 Okt 2026): **setiap baris kini punya minimal 1 tautan langsung**:

| Sumber | L | R | W | S | Jenis |
|---|---|---|---|---|---|
| Engnovate | 84 | 83 (tanpa C19 T1) | 84 | 84 | Tes interaktif lengkap (sumber utama) |
| IELTSXpress | 67 (C4 T2 sampai C20) | 46 (C7–C20, sebagian C7–C9) | - | - | Halaman soal + kunci |
| LangGo | - | - | 24 (C18–C20 Task 1/2) | 12 (C18–C20 Part 1) | Contoh jawaban |

Ditambah 15 halaman ringkasan buku IELTSXpress (C5–C19). Tautan **Search** (Google) tetap ada di setiap baris sebagai cadangan.

Catatan:
- C1–C6 formatnya lebih lama dan kurang relevan untuk persiapan saat ini.
- C21 (2026) tersedia di Engnovate; belum ada di sumber lain.
- Edisi **General Training** punya Reading & Writing berbeda; Listening/Speaking sama. Jika ditambahkan, cakupannya dihitung terpisah.

---

## 4. Struktur file

```
Latihan/
├── index.html                 # Hub + tracker (satu file, offline, tanpa dependensi)
├── AGENTS.md                  # File ini
├── CLAUDE.md                  # Memuat AGENTS.md + pointer antislop (Claude Code)
├── DESIGN.md                  # Arah desain: palet, tipografi, dial, alasan tiap keputusan
├── .claude/skills/antislop*/  # Skill antislop v3.2.24 (filter UI/copy/aksesibilitas/mobile/komentar)
├── README.md                  # Panduan pengguna
├── anti-slop/                 # Laporan audit antislop (temuan + tindak lanjut)
└── research/
    ├── engnovate-links.txt    # 335 URL tes Academic Engnovate (dari sitemap)
    ├── links-source.txt       # URL IELTSXpress C15–C20 (sitemap)
    ├── links-older.txt        # URL IELTSXpress C7–C14 (sitemap)
    ├── langgo-ws-links.txt    # URL LangGo Writing/Speaking
    ├── extra-maps.json        # (arsip) peta L/R lama
    └── ws-maps.json           # (arsip) peta W/S lama
```

---

## 5. Model data di index.html

```js
// Engnovate: URL dibangun dari pola sitemap; pengecualian di EN_MISSING
enUrl(m,b,t) → "https://engnovate.com/ielts-<listening|reading|writing|speaking>-tests/cambridge-ielts-<BB>-academic-<mod>-test-<t>/"
const EN_MISSING = new Set(["R-19-1"]);

const L = { "18-1": IX+"...", ... };               // IELTSXpress Listening: 1 URL per tes
const R = { "18-1": IX+"...", ... };               // IELTSXpress Reading: 1 URL per tes
const W = { "18-1": [{t:"Task 1",u:"..."}, {t:"Task 2",u:"..."}] };  // LangGo contoh jawaban
const S = { "18-1": [{t:"Part 1",u:"..."}] };      // LangGo contoh jawaban
const BOOKPAGE = { 18: IX+"cambridge-ielts-18-tests/" };            // ringkasan buku
```

- `linksFor(m,b,t)` menyusun tautan dengan `kind`: `main` (bergaris biru), `alt` (sumber lain), `ex` (contoh jawaban LangGo), lalu `search` (**Search**) sebagai cadangan.
- localStorage:
  - `ielts-hub-progress-v1`: progres. Kunci `L-18-1`, `R-18-1`, `W-18-1`, `S-18-1`; nilai `{done, score, band, note, date, opened, ts}` (`ts` = epoch ms saat selesai, untuk tren; entri lama tanpa `ts` di-parse dari `date`). **Hanya objek ini yang di-Export/Import.**
  - `ielts-hub-prefs-v1`: modul/tampilan/filter/urutan/tema terakhir, plus `targets` (`{L,R,W,S,O}` → `"6.5"`, target band per skill dan overall) dan `guide` (`""` = panel Start here tampil sampai ada tes selesai, `"hidden"` = disembunyikan pengguna, `"show"` = dibuka lagi dari Help).
- Panel Start here: langkah 1 tercentang jika ada target, langkah 2 jika ada tes yang pernah dibuka, langkah 3 jika ada tes selesai. Selama panel tampil, tombol merahnya satu-satunya tombol utama (ringkasan tidak memberi `.primary`).
  - `ielts-hub-timer-v1`: status timer (tetap jalan setelah reload).
- Listening/Reading: input benar/40 → band otomatis (`TBL.L` / `TBL.R`). Skor di bawah tabel ditampilkan "band < 4.0" (L) / "< 2.5" (R) dan dihitung ≈3.5 / ≈2.0 untuk rata-rata.
- Writing/Speaking: band self-assessment 0–9 (kelipatan 0.5).
- Mengisi skor/band otomatis mencentang **Done**.
- Estimasi overall = rata-rata dari rata-rata tiap modul, dibulatkan ala IELTS (`Math.round(x*2)/2`).
- Priority = skill dengan selisih positif terbesar antara target dan rata-rata band. Tanpa target, tombol utama ada di skill dengan tes selesai paling sedikit.
- Current book = buku pertama (sesuai filter dan urutan) yang belum tuntas 16 sesi.

Tabel band Listening: 39–40→9.0 · 37–38→8.5 · 35–36→8.0 · 32–34→7.5 · 30–31→7.0 · 26–29→6.5 · 23–25→6.0 · 18–22→5.5 · 16–17→5.0 · 13–15→4.5 · 11–12→4.0.
Tabel band Academic Reading: 39–40→9.0 · 37–38→8.5 · 35–36→8.0 · 33–34→7.5 · 30–32→7.0 · 27–29→6.5 · 23–26→6.0 · 19–22→5.5 · 15–18→5.0 · 13–14→4.5 · 10–12→4.0 · 8–9→3.5 · 6–7→3.0 · 4–5→2.5.

---

## 6. Menambah / memperbarui tautan

1. Cari halaman tes di situs latihan (Engnovate, IELTSXpress, LangGo, DOL, dll.). Sitemap paling andal (`/sitemap_index.xml`, `/post-sitemap*.xml`).
2. Verifikasi status: `curl -s -o /dev/null --max-redirs 0 -w "%{http_code}" <url>` → harus `200`.
3. Tambahkan ke objek `L`/`R`/`W`/`S` dengan kunci `<book>-<test>` (atau hapus dari `EN_MISSING` bila Engnovate menambah tes).
4. Perbarui tanggal cek di README (bagian Catatan) dan tabel di §3. Tanggal cek dan jumlah tautan tidak ditampilkan di halaman, karena pengguna tidak membutuhkannya.
5. Jika tautan mati: hapus dari objek (atau tambahkan ke `EN_MISSING`) atau ganti dengan URL baru yang 200. Tautan **Search** tetap tersedia.
6. Jangan mengubah format kunci progres agar data pengguna tidak hilang.

---

## 7. Checklist QA

- [ ] `index.html` terbuka tanpa error JS (terang & gelap, desktop & ±390px tanpa scroll horizontal).
- [ ] 84 baris per modul (336 total untuk C1–C21), setiap baris punya chip utama.
- [ ] Semua tautan langsung HTTP 200.
- [ ] Tautan **Search** berfungsi di setiap baris.
- [ ] Centang + skor + band + catatan tersimpan setelah reload; skor otomatis menandai selesai.
- [ ] Filter Book/Status/Order/Search, Book map (klik kotak → baris), Your progress (target, Priority, "Open test", lompat ke baris), dan tombol detail baris di HP bekerja.
- [ ] Kunjungan pertama (localStorage kosong): panel Start here tampil; pilih target mencentang langkah 1, tombol Open mencentang langkah 2, "Go to the score box" memfokuskan kotak skor, dan skor pertama menyembunyikan panel. Hide guide menyembunyikan panel, dan Help bisa memunculkannya lagi.
- [ ] Help terbuka lewat tombol dan `?`, tertutup lewat Close, Esc, dan klik di luar dialog; fokus kembali ke tombol asal; tabel band cocok dengan `TBL`.
- [ ] Timer mulai/jeda/ulang, bertahan setelah reload, berbunyi saat habis.
- [ ] Download backup menghasilkan JSON; Restore backup (tombol, bisa dengan keyboard) memulihkan progres (kunci tidak valid diabaikan).
- [ ] Teks About this site di footer dan Help masih sesuai fakta (lihat §1 butir 5).
- [ ] Perubahan UI mengikuti `DESIGN.md` dan lolos Delivery Gate antislop: kontras teks ≥ 4.5:1 di kedua tema, target sentuh ≥ 44px di HP, tanpa em dash, setiap kontrol punya nama aksesibel, dan tidak ada teks UI berbahasa Indonesia.

---

## 8. Sumber

- **Engnovate**: tes interaktif gratis Academic L/R/W/S C1–C21 (sumber utama).
- **IELTSXpress**: Listening C4–C20 & Academic Reading C7–C20 (sebagian) + halaman ringkasan buku C5–C19.
- **LangGo**: contoh jawaban Writing Task 1/2 & Speaking Part 1, C18–C20.
- Resmi gratis: IELTS.org, IDP, Cambridge English (tombol di halaman).
