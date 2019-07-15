### PT. Skyshi Digital Indonesia
##### Jl. Tampomas No. 9, Trihanggo, Kec. Gamping,
##### Kab. Sleman, Daerah Istimewa Yogyakarta, Indonesia, 55291.
##### Phone : (0274) 4547428, Email : hello@skyshi.com 

Frontend Guideline
====================
### Daftar Isi
- [Introduction](#introduction)
- [Frontend Guideline](#frontend-guideline)	
  - [The App](#the-app)
  - [Errors](#errors)
  - [Form](#form)
  - [3rd Party Library](#3rd-party-library) 
  - [Privacy Data](#privacy-data)
  - [Git Convention](#git-convention)
  - [Coding Standard](#coding-standard)
  - [Pagination](#pagination)
  - [API](#api)
  - [Redux](#redux)
  - [Server Side Rendering](#server-side-rendering)
  - [Boilerplate](#boilerplate)
    - [Starting Project](#boilerplate)
    - [Pages and URLs](#pages-and-urls)
    - [Static Files](#static-files)
    - [Playground](#playground)
  - [URL SEO Friendly](#url-seo-friendly)
  - [Clickable Image](#clickable-image)

        
 
## Introduction
**Skyshi Procedure Documentation** yaitu standar dokumentasi untuk setiap divisi dalam mengelola pekerjaan yang akan memudahkan proses birokrasi dalam mengerjakan task yang diberikan, diharapkan dengan menggunakan dokumen ini pekerjaan antara divisi akan lebih mudah dan efisien.

## The App	
- Configs
Menggunakan satu config file atau *.env* (jika support), dan *jangan hardcode*.
Error Logging
- Log the error menggunakan Sentry or *Bugsnag*, jika menggunakan *console.log()*, jangan lupa hapus semua *console.log()* di production.
- Handling State
Handle berbeda antara loading dan empty state. Tambah notifikasi atau label yang menunjukkan kondisi saat ini.
- Components
	Selau mempertimbangkan pembuatan *component baru* agar dapat digunakan kembali.contoh, a <Card> yang akan tambil dibeberapa halaman, structure sama,tetapi konten berbeda, kita dapat membuat menggunakan components tersebut, components ini akan mengurangi waktu penulisan code.
![4](https://user-images.githubusercontent.com/45573867/61206447-cb1b5600-a71c-11e9-92b5-a2682cd02cf5.png)

## Errors	
- Error Handling
Harus menangani setiap status eror di halaman, menampilkan pesan eror menggunakan alert,  pesan text atau sesuatu yang dapat memberikan notifikasi kepada user.
- Error Reporting
Menggunakan `getsentry` untuk real-time error reporting, harus disiapkan diawal inisiasi proyek.

## Form	
- Validasi
	Menambahkan validasi pada setiap input form. Harus ditempatkan dibagian bawah field.
- Disable default action form
Selalu disable action default menggunakan *event.preventDefault()* pada setiap *onSubmitForm()* function
- Submitting form
	Enable atau disable form submission dengan klik button atau tekan ‘enter’ berdasarkan persyaratan.
- Pastikan form terkirim saat user menekan Enter (Kecuali permintaan khusus)
- Pesan eror untuk setiap tampilan inputan form terletak dibawah form input.

## 3rd Party Library	
- Menggunakan aturan coding tunggal , dan linter
- Cek di github repo terlebih dahulu untuk mengetahui support atau tidaknya
- Menentukan jika benar-benar digunakan untuk salah satu fungsi atau berguna bagi secara keseluruhan proyek

## Privacy Data	
- Jangan menyimpan apa pun di samping token pada cookie

## Git Convention	
- Gambar umum (bukan  assets) direktori, direktori node_modules, config file, .env, dll harus termasuk dalam file .gitignore.
- Harus memiliki master (seperti production), development, dan staging
- Harus mendorong cabang sebagai fitur, contoh: feature/social-login
- Hotfix harus menggunakan master source, tidak pernah menggunakan development sebagai source
- Praktekkan dengan mengikuti penamaan konversi berikut ini :

|Instance|Branch|Description|
|:--------|:------|:-----------|
|Stable|stable|Accepts merges from Working and Hotfixes|
|Working|master|Accepts merges from Features/Issues and Hotfixes|
|Features/issues|topic-* |Always branch off HEAD of Working|
|Hotfix|hotfix-* |Always branch off Stable|

Lebih lengkapnya dapat menggunakan referensi berikut ini:
- https://gist.github.com/digitaljhelms/4287848 
- https://github.com/agis/git-style-guide

## Coding Standard	
- Gunakan linter (ESLint) untuk menjaga standard code.
- Gunakan const jika variable adalah statis ( for JS )
- Menulis proses yang sama di function, sehingga dapat digunakan kembali
- Pastikan hapus semua  console.log() sebelum melakukan deployment ke production
- Pastikan links support ‘open new tab’


## Pagination
- GunakanURL untuk perubahan page
Contoh : https://www.yourwebsite.com/destination?page=1, https://www.yourwebsite.com/destination?page=2, dll
- Gunakan library ‘react-paginate’ untuk membantu pembuatan pagination (jika masih layak)
- Gunakan loading (jika perlu) ketika mengubah halaman (menggunakan 
- Use loading ( if necessary ) when changing page ( using prop ‘isLoading’ untuk trigger loading animasi) 
- Pastikan tidak reset data pada reduk ketika mengubah halaman untuk menghindari menampilkan data kosong.

## API
- Pastikan mengambil data dari API sebelum memberikan component ( untuk SSR ) menggunakan getInitialProps()
- Cara maintenance mode halaman 
- Ketika akses API dan tidak menerima balasan ( API Offline ) 
- API maintenance mode hidup  (jika tersedia) untuk kasus ini backend akan mengembalikan status mode maintenance  
- Menampilkan pesan toast ketika user tidak mempunyai koneksi internet
- Mendapat balasan status dari axios/apisauce untuk eror timeout, network error, dll. Setiap gagal memanggil API selalu mendapat balasan - field pesan dalam merespon data, membuat pesan dan ditampilkan.

## Redux
- Gunakan ‘isLoading’ ( boolean ) props untuk trigger aksi loading Set ‘isLoading’ untuk ‘true’ ketika melakukan permintaan, set ‘isLoading’ untuk ‘false’ ketika aksi sukses atau gagal.
- Gunakan ‘isSuccess’ ( boolean ) props untuk menemukan data yang berhasil diambil atau tidaknya, Set ‘isSuccess’ untuk ‘true’ ketika aksi sukses dan  set ‘isFetched’ untuk ‘false’ ketika aksi gagal.
- Gunakan ‘data’ (object) props untuk untuk menyimpan semua data dari API 
Gunakan ‘errorMsg’ (object/string) props untuk penyimpanan pesan eror dari API

## Server Side Rendering	
Server-side rendering (SSR) Memungkinkan google mesin untuk indeks halaman, React js tanpa SSR hanya akan menampilkan <head> tag dan tidak ada didalam <body> tag di view page-source dan google tidak bisa indeks halaman karena menunjukkan tidak ada apapun di dalam server.
Bagaimana cara cek SSR :
- Render aplikasi, kemudian pada browser, buka tampilan page-source, jika semua elemen dapat dilihat di rendered app juka akan menampilkan code dalam tampilan page-source maka itu sudah SSR.
- Coba menggunakan console.log() difungsi utama (e.g inside getInitialProps() function), log mencatat text atau sesuatu, jika tidak muncul pada  browser console maka tidak SSR, itu akan muncul pada command line.
- Render aplikasi, kemudian turn off browser  javascript dan reload halaman, jika tidak menampilkan apapun,maka itu bukan SSR. Anda juga dapat memeriksa dengan menelusuri aplikasi.

## Boilerplate
Cek boilerplate , ini adalah template pemula untuk memulai proyek baru, kita menggunakan Nextjs untuk memungkinkan server-side rendering untuk proyek kami.

### Starting Project	
- Mengkloning repo.
- Jalankan yarn atau npm install untuk install semua dependencies.
- Pastikan semua dependencies menggunakan versi terbaru
- Jalankan yarn start atau npm run start untuk memulai pada server lokal.
- Memulai coding.

### Pages and URLs	
![5](https://user-images.githubusercontent.com/45573867/61209453-fb1a2780-a723-11e9-9747-7fd9eeed53f4.png)

Halaman pada pages directory, nextjs akan otomatis rendernama setiap file pages directory sebagai url.Contoh,jika ada file nama  ‘pages/about.js’, ketika  anda menelusuri {{base_url}}/about, nextjs akan otomatis render ‘pages/about.js’ secara default,atau anda akan konfigurasi semua router url pada file server.js. bacalah Nextjs documentation.

### Static Files	
![6](https://user-images.githubusercontent.com/45573867/61209456-fe151800-a723-11e9-9c7e-329b444e7cad.png)

Semua file static ( compiled css / js, image file, dll ) di directory static.

### Playground
![7](https://user-images.githubusercontent.com/45573867/61209460-00777200-a724-11e9-932b-99a3c3449868.png)

Keajaiban dimulai dari direktori src. Berikut adalah struktur direktori src :
- /src/components Pure React Components
- /src/config App Config
- /src/containers React Redux Components
- /src/layout Predefined Layout
- /src/redux Redux Files (Reducers, Actions)
- /src/sagas Redux Side Effects (Redux-Saga)
- /src/services Services (APIs, etc)
- /src/utils Utils Helpers
- /src/validations Validate.js Constraints

LInk untuk training Trello (dapat diakses menggunakan developer@skyshi.com)

## URL SEO Friendly
Pedoman Dalam Penanganan URL SEO Friendly untuk Frontend
- URL hanya boleh mengandung ID yang pendek apabila memungkinkan hapus ID 
- URL harus SEO friendly dan human readable

## Clickable Image
Pedoman Dalam Penanganan Image Pada Halaman List
- Image dan judul harus bisa di click 







