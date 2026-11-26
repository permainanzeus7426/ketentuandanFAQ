# FAQ & Pengumuman Zeus2010

Situs statis tersedia di `index.html` dan diterbitkan melalui GitHub Pages saat ada push ke branch `main`.

## Menghubungkan domain

Domain yang disiapkan: `ketentuandanfaqpermainan.com`.

Di repositori GitHub, buka **Settings → Pages** dan pilih **GitHub Actions** sebagai sumber deployment.

Atur DNS domain di penyedia domain:

- Buat empat record A untuk host `@`, masing-masing mengarah ke `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, dan `185.199.111.153`.
- Hapus record A/AAAA lama untuk host `@` yang bertentangan.
- Setelah DNS tersebar dan GitHub Pages mengenali domain, aktifkan HTTPS di pengaturan Pages repositori.

File `CNAME`, `robots.txt`, dan `sitemap.xml` sudah disiapkan untuk domain tersebut. Situs dan sitemap baru dapat diakses setelah perubahan dipush ke `main`, DNS tersebar, dan workflow deployment berhasil.

## Meminta pengindeksan mesin pencari

Tambahkan domain sebagai properti di Google Search Console, verifikasi kepemilikan melalui DNS, lalu kirim `https://ketentuandanfaqpermainan.com/sitemap.xml`. Mesin pencari menentukan sendiri kapan dan apakah halaman dimasukkan ke hasil pencarian; publikasi tidak menjamin pengindeksan atau peringkat tertentu.
