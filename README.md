# Pulsa — Network Speed Test

Speed test bergaya Ookla (gauge/jarum berputar) yang berjalan 100% di browser — tidak ada backend, tidak ada database, tidak ada data yang dikumpulkan atau disimpan oleh aplikasi ini.

## Cara kerja

- **Ping & Jitter** — mengirim beberapa request kecil dan mengukur waktu bolak-balik (round-trip time).
- **Download** — mengunduh data dari beberapa koneksi paralel dan menghitung throughput secara real-time.
- **Upload** — mengunggah data acak (dibuat di sisi klien, bukan file Anda) dan menghitung throughput-nya.

Semua pengujian memakai endpoint publik **Cloudflare Speed Test** (`speed.cloudflare.com`) melalui **HTTPS**. Ini adalah infrastruktur yang sama yang dipakai banyak proyek speed test open-source, dan mendukung CORS sehingga bisa dipanggil langsung dari situs statis seperti GitHub Pages.

## Kenapa ini "aman"

- Seluruh koneksi memakai HTTPS (terenkripsi), tidak ada request ke domain yang tidak dikenal.
- Data yang diunggah saat tes upload adalah byte acak yang dibuat di browser Anda sendiri — bukan file, cookie, atau data pribadi apa pun.
- Tidak ada server milik aplikasi ini yang mencatat hasil tes; semua perhitungan terjadi di JavaScript sisi klien.
- Tidak ada dependensi pihak ketiga selain font Google Fonts (opsional, bisa dihapus jika ingin 100% self-contained).
- Cocok di-hosting sebagai situs statis (GitHub Pages, Netlify, Vercel, dll.) karena tidak butuh server/backend sendiri.

## Deploy ke GitHub Pages

1. Buat repository baru di GitHub, misalnya `speedtest`.
2. Upload file `index.html` (dan `README.md` ini) ke repository tersebut.
3. Buka **Settings → Pages** pada repository.
4. Di bagian **Source**, pilih branch `main` dan folder `/ (root)`, lalu klik **Save**.
5. Tunggu 1–2 menit, situs Anda akan aktif di `https://<username-anda>.github.io/<nama-repo>/`.

Tidak perlu build step, tidak perlu Node.js — file `index.html` berdiri sendiri.

## Kustomisasi cepat

Semua parameter penting ada di bagian atas `<script>` pada `index.html`:

```js
const PING_COUNT = 12;
const DOWNLOAD_DURATION_MS = 8000;
const UPLOAD_DURATION_MS = 8000;
const DOWNLOAD_STREAMS = 4;
const UPLOAD_STREAMS = 3;
```

Ubah durasi atau jumlah koneksi paralel sesuai kebutuhan. Warna, font, dan gaya panel ada di bagian `<style>`.

## Batasan yang perlu diketahui

- Karena tidak memakai server sendiri, hasil pengujian bergantung pada jarak/latensi ke jaringan Cloudflare, bukan ke server pribadi Anda — ini normal dan sama seperti cara kerja speedtest publik lain.
- Jika ingin server pengujian milik sendiri (misalnya untuk mengukur ke satu titik tertentu), Anda perlu menambahkan backend kecil yang menerima upload dan mengirim data besar untuk download; struktur front-end di file ini sudah bisa dipakai kembali, tinggal ganti `DOWN_URL_BASE` dan `UP_URL`.
