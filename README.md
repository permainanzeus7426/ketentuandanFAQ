# FAQ & Pengumuman Zeus2010

Situs statis tersedia di `index.html` dan diterbitkan melalui GitHub Pages saat ada push ke branch `main`.

URL situs yang disiapkan: <https://zeus2010.com/>

Di repositori GitHub, buka **Settings → Pages**, pilih **GitHub Actions** sebagai sumber deployment, lalu masukkan `zeus2010.com` pada **Custom domain** dan simpan. Akses API yang digunakan untuk deployment tidak memiliki izin menyimpan pengaturan custom domain secara otomatis.

Domain kustom memerlukan DNS yang diarahkan ke GitHub Pages:

- Buat record A untuk host `@` yang mengarah ke `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, dan `185.199.111.153`.
- Hapus record A/AAAA lama untuk host `@` yang bertentangan.
- Jika memakai Cloudflare, gunakan DNS-only (proxy nonaktif) untuk record domain tersebut.
- Setelah DNS tersebar dan GitHub Pages memverifikasi domain, aktifkan HTTPS di pengaturan Pages repositori.

File `CNAME`, canonical URL, `robots.txt`, dan `sitemap.xml` sudah disiapkan untuk domain tersebut. Situs akan tersedia setelah DNS diarahkan dengan benar dan GitHub Pages selesai menerbitkannya.

## Meminta pengindeksan mesin pencari

Tambahkan `https://zeus2010.com/` sebagai properti di Google Search Console, verifikasi kepemilikan, lalu kirim `https://zeus2010.com/sitemap.xml`. Mesin pencari menentukan sendiri kapan dan apakah halaman dimasukkan ke hasil pencarian; publikasi tidak menjamin pengindeksan atau peringkat tertentu.
