# Audit Modul 4 - Flexbox, Grid, dan Responsive Design

## Hasil uji viewport

| Viewport | Gejala awal | Penyebab | Perbaikan | Hasil uji ulang |
|---|---|---|---|---|
| 360 px | Header, navigasi, kartu katalog, dan field form hanya mengikuti normal flow; struktur layout responsif belum tersedia. | Header/nav belum memakai Flexbox, katalog/form belum memakai Grid. | Menambahkan Flexbox yang dapat membungkus pada header, navigasi, metadata, dan tombol; katalog memakai Grid `auto-fit`; form tetap satu kolom. | Tidak ada horizontal scroll; navigasi membungkus bila perlu, katalog satu kolom, dan semua kontrol form dapat digunakan. |
| 768 px | Hero tetap vertikal dan field form belum dapat memanfaatkan ruang layar. | Belum ada breakpoint berbasis kebutuhan konten. | Pada `48rem`, hero menjadi dua kolom dan `.form-grid` menjadi dua kolom dengan `minmax(0, 1fr)`. | Hero, dua kelompok field form, dan tombol tetap terbaca tanpa overlap. |
| 1280 px | Katalog tidak memiliki aturan jumlah kolom otomatis. | Kartu belum diletakkan dalam layout Grid. | Menambahkan `repeat(auto-fit, minmax(16rem, 1fr))` pada katalog. | Tiga kartu memanfaatkan lebar konten secara proporsional; whitespace tetap wajar. |

## Audit overflow

- Elemen yang menyebabkan overflow: Tidak ditemukan pada pengujian viewport 360 px.
- Bukti pengujian browser: Lebar `document.documentElement.scrollWidth` sama dengan lebar area dokumen pada halaman beranda, katalog, dan peminjaman.
- Aturan penyebab: Risiko overflow sebelumnya berasal dari navigasi tanpa pembungkusan, field dengan `width: 100%`, dan kartu yang belum memiliki track Grid lentur.
- Perbaikan: Menerapkan `box-sizing: border-box`, `flex-wrap`, `minmax(0, 1fr)`, Grid `auto-fit`, serta `max-width: 100%` pada media.
- Hasil uji ulang: Tidak memakai `overflow-x: hidden`; konten tetap berada di dalam viewport pada 360 px.

## Keyboard dan zoom

- Fokus keyboard tetap terlihat melalui outline pada link, input, select, textarea, dan tombol.
- Aturan layout mendukung zoom 200%: header dapat membungkus, tombol form dapat berpindah baris, dan konten utama tidak memakai lebar tetap.

## Catatan breakpoint

- Breakpoint `48rem` digunakan karena pada lebar sekitar 768 px hero dan dua fieldset memiliki ruang cukup untuk berjajar tanpa memaksa lebar konten. Tidak diperlukan breakpoint tambahan karena Grid katalog sudah menyesuaikan kolom secara otomatis.
