# our-anniversary 💌

Website kejutan hari jadian: amplop pembuka, pilihan kejutan (Journey, Moment, Playlist, Gift),
tema hitam, plum, dan magenta. HTML, CSS, dan JavaScript biasa, tanpa framework dan tanpa build.

## Cara menjalankan

**Paling mudah (VS Code):**
1. Buka folder `our-anniversary` di VS Code (File, Open Folder).
2. Pasang ekstensi **Live Server** (Ritwick Dey).
3. Klik kanan `index.html`, lalu pilih **Open with Live Server**.

Bisa juga langsung klik dua kali `index.html`, karena tidak butuh server.
Butuh internet untuk memuat font Google dan video YouTube.

## Struktur

```
our-anniversary/
├── index.html           kerangka halaman dan urutan file yang dimuat
├── data/content.js      ISI WEBSITE: nama, tanggal jadian, surat, kupon, foto, lagu
├── assets/
│   ├── photos/          foto-foto (photo-1.jpg ... photo-8.jpg)
│   └── icons/favicon.svg
├── css/
│   ├── base.css         warna, font, reset, layar, tombol BACK, hati melayang
│   ├── envelope.css     amplop dan segel
│   ├── menu.css         Choose the Surprise
│   ├── journey.css      polaroid
│   ├── moment.css       surat, perangko, bingkai foto, hitungan waktu
│   ├── playlist.css     pemutar YouTube dan daftar lagu
│   ├── gift.css         hadiah dan kupon
│   ├── admin.css        menu edit (☰), form, tombol tambah/hapus
│   └── responsive.css   aturan layar kecil
└── js/
    ├── config.js        kunci penyimpanan dan nama parameter URL
    ├── utils.js         fungsi bantu ($, el, toast, go)
    ├── store.js         memuat dan menyimpan data
    ├── envelope.js      membuka amplop
    ├── admin.js         mode edit (foto, lagu, teks)
    ├── journey.js       halaman Journey
    ├── moment.js        halaman Moment
    ├── playlist.js      halaman Playlist (pemutar YouTube)
    ├── gift.js          halaman Gift
    └── main.js          render, navigasi, hati melayang (dimuat paling akhir)
```

Urutan file di `index.html` penting, jadi jangan diubah-ubah.

## Mengganti isi

Cara paling aman dan terlihat oleh semua orang: edit **`data/content.js`**.

- **Nama, tanggal jadian, surat, kupon:** ubah `her`, `him`, `since`, `letter`, `gift`.
  Format tanggal: `"2026-09-28T00:00"`.
- **Foto:** taruh file di `assets/photos/`, lalu tulis di `photos`, misalnya
  `{ "id": "p9", "src": "assets/photos/foto-baru.jpg" }`. Maksimal 12 foto. Foto bingkai emas diatur di `portrait`.
- **Lagu:** tambah di `songs`: `{ "id": "s3", "t": "Judul", "a": "Artis", "u": "https://youtu.be/xxxxxxxxxxx" }`.
  `u` boleh dikosongkan, nanti hanya membuka pencarian YouTube.

## Mode edit di browser

Menu ☰ di kiri atas berisi **Teks**, **Foto**, **Lagu**, dan **Simpan**. Halaman Journey dan Playlist tetap bersih,
persis seperti yang dilihat pacarmu.

- **Foto:** jendela berisi foto di samping surat (bingkai emas, halaman Moment) dan semua polaroid. Tiap foto punya tombol **Ganti** dan **Hapus**
  (hapus perlu dua ketukan), plus kotak **＋** untuk menambah (maksimal 12).
- **Lagu:** daftar lagu dengan tombol ✎ (edit) dan ✕ (hapus, dua ketukan), plus **＋ Tambah lagu**.
- **Wishlist:** wishlist jalan minggu ini di halaman Gift (maksimal 6): emoji, judul, dan keterangan. Setelah bintang 🌠 diketuk, pacarmu memilih salah satu, menentukan tanggalnya, lalu bisa menyimpannya ke kalender dan menekan **Kabari** untuk membagikan pilihannya ke kamu.
- **Teks:** nama, tanggal jadian, isi surat, dan kupon.

Menu ini muncul otomatis saat web dibuka di komputermu sendiri: klik dua kali `index.html`, Live Server, `localhost`,
atau lewat Wi-Fi rumah. Setelah online (Netlify, GitHub Pages), pengunjung tidak melihatnya.

- `?edit` di ujung alamat memaksa menu edit muncul, di mana pun web dibuka.
- `?view` menyembunyikan menu edit, untuk melihat tampilan seperti yang dilihat pacarmu.
- `?reset` menghapus perubahan yang tersimpan di browser.

Tekan **Simpan** setelah mengubah. Catatan penting: perubahan dari mode edit **disimpan di browser perangkat itu saja**
(localStorage), jadi pacarmu tidak akan melihatnya di HP-nya. Supaya dilihat semua orang, pindahkan hasilnya ke
`data/content.js` lalu deploy ulang.

## Responsif

Tata letak memakai ukuran fleksibel (`clamp`, `min`, `flex`, `grid`), area aman untuk notch HP,
dan satu aturan khusus layar kecil di `css/responsive.css`. Cek lewat DevTools di browser (Ctrl+Shift+M).

## Online (gratis)

- **Netlify:** drag-and-drop folder `our-anniversary` di app.netlify.com/drop.
- **GitHub Pages:** upload ke repo, lalu Settings, Pages, branch `main`.

## Video YouTube tidak muncul (Error 153)?

YouTube hanya mau memutar video di dalam halaman yang punya alamat web sungguhan. Kalau `index.html` dibuka dengan
klik dua kali (alamatnya `file:///...`), pemutar menampilkan "Video player configuration error, Error 153".
Jalankan lewat server: `python -m http.server 8000`, lalu buka `http://localhost:8000`. Setelah online
(Netlify, GitHub Pages) juga otomatis berfungsi. Kalau web dibuka lewat `file://`, halaman Playlist menampilkan
kartu thumbnail yang membuka video di YouTube. Beberapa video juga melarang disematkan, dan itu tidak bisa diakali.
