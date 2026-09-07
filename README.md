# Speedtest

Situs uji kecepatan jaringan sederhana: ping, kecepatan unduh, dan kecepatan unggah — semuanya diukur langsung di peramban Anda, tanpa server sendiri.

## Cara kerja

- Pengukuran ping, unduh, dan unggah dilakukan lewat jaringan pengukuran publik Cloudflare (`speed.cloudflare.com`), diakses lewat pustaka resmi `@cloudflare/speedtest`.
- Nama penyedia layanan (ISP) diambil dari `ipwho.is`. Alamat IP dari respons itu **tidak pernah dibaca, ditampilkan, atau disimpan** — hanya nama penyedianya yang ditampilkan.
- Tidak ada backend, database, atau penyimpanan di sisi server. Semua berjalan di `index.html` satu berkas.

## Menjalankan secara lokal

Buka `index.html` langsung di peramban, atau jalankan server statis sederhana:

```bash
npx serve .
```

## Mengunggah ke GitHub + mengaktifkan GitHub Pages

1. Buat repository baru di GitHub bernama `speedtest`.
2. Di folder ini, jalankan:
   ```bash
   git init
   git add .
   git commit -m "Speedtest awal"
   git branch -M main
   git remote add origin https://github.com/<username-anda>/speedtest.git
   git push -u origin main
   ```
3. Di GitHub: buka **Settings → Pages**, pilih source **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu simpan.
4. Situs akan tersedia di `https://<username-anda>.github.io/speedtest/` dalam beberapa menit.

## Catatan keamanan

- Semua permintaan jaringan diarahkan lewat HTTPS.
- Tidak ada kode yang dievaluasi secara dinamis (`eval`), tidak ada input pengguna yang disisipkan langsung ke HTML.
- Tidak ada pelacakan pihak ketiga, cookie, atau penyimpanan lokal.
