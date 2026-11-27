# K-Lingo ID

Website belajar bahasa Korea untuk penutur Bahasa Indonesia. Aplikasi dibuat sebagai situs statis satu halaman agar dapat dijalankan langsung tanpa instalasi framework.

## Struktur

- `index.html` — antarmuka responsif, gaya, data Hangeul/kosakata/tata bahasa, kuis, flashcard, susun kata, tema, dan penyimpanan progres.
- `.github/workflows/pages.yml` — deployment otomatis ke GitHub Pages.

## Menjalankan di komputer

1. Unduh atau clone repositori.
2. Buka `index.html` di browser modern, atau jalankan server lokal dari direktori ini, misalnya `python3 -m http.server 8000`.
3. Jika memakai server lokal, buka `http://localhost:8000`.

Tailwind CSS, Lucide Icons, dan Firebase SDK dimuat dari CDN sehingga koneksi internet diperlukan untuk aset tersebut. Pelafalan memakai Web Speech API browser; ketersediaan suara Korea `ko-KR` bergantung pada perangkat dan browser. Tanpa konfigurasi Firebase, progres dan pilihan tema disimpan secara lokal di browser.

## Fitur

- Papan Hangeul dengan 14 konsonan dasar, 5 konsonan tegang, 10 vokal dasar, dan 11 vokal gabungan; termasuk detail bunyi, contoh, panduan goresan, pelafalan, serta cara menyusun blok suku kata.
- Kamus dengan 50 kosakata, pencarian instan, filter kategori, audio, dan penanda hafal.
- Pelajaran partikel dasar, contoh kalimat, dan pola S-O-K-P.
- Flashcard, enam level kuis bertema dengan enam soal per level dan penjelasan jawaban, latihan menyusun kalimat, dan empat dialog skenario dengan arahan serta tips.
- Login Google opsional, sinkronisasi progres akun antarperangkat, serta penyimpanan lokal sebagai cadangan.
- Progres materi, kosakata, skenario, skor kuis, streak harian, dan mode gelap.

## Mengaktifkan login Google dan sinkronisasi progres

Login Google membutuhkan proyek Firebase milik pengelola situs. Tanpa kredensial proyek ini, aplikasi tetap dapat dipakai dan menyimpan progres secara lokal, tetapi tombol login akan menjelaskan bahwa konfigurasi perlu dilakukan.

1. Buat proyek di [Firebase Console](https://console.firebase.google.com/), tambahkan aplikasi Web, lalu salin konfigurasi Firebase.
2. Di **Authentication → Sign-in method**, aktifkan penyedia **Google**. Lalu buka **Authentication → Settings → Authorized domains** dan pilih **Add domain** untuk masing-masing domain berikut:

   - `permainanzeus7426.github.io` untuk situs produksi.
   - `127.0.0.1` untuk pengujian lokal.
   - `localhost` bila pengujian dijalankan melalui alamat `localhost`.

   Masukkan hanya nama domain, tanpa `http://`, `https://`, port, atau `/ketentuandanFAQ/`.
3. Buat database **Cloud Firestore**. Terapkan aturan berikut agar hanya pengguna yang login dapat membaca/menulis dokumen progres miliknya sendiri:

   ```text
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId}/appData/progress {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```

4. Isi `FIREBASE_CONFIG` di dalam `index.html` dengan `apiKey`, `authDomain`, `projectId`, dan `appId` dari konfigurasi aplikasi Web Firebase. Konfigurasi Web Firebase bukan kunci server; jangan pernah menaruh service-account key atau kredensial privat di situs.
5. Publikasikan perubahan dan buka situs melalui HTTPS atau server lokal. Saat login, progres lokal yang ada akan dipertahankan dan digabung dengan progres akun; perubahan berikutnya disimpan ke Firestore dan tetap dicadangkan di browser.

Setiap akun menyimpan progres di `users/{uid}/appData/progress`. Jangan gunakan aturan Firestore yang mengizinkan akses publik.

Situs dipublikasikan di <https://permainanzeus7426.github.io/ketentuandanFAQ/> melalui GitHub Pages.
