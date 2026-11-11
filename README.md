# myMarkah SKJB: panduan pemasangan

Aplikasi markah ujian tahunan: guru isi markah, analisis subjek/kelas/darjah, slip keputusan, dan portal semakan ibu bapa. Satu fail sahaja (`index.html`).

## 1. Cuba dahulu (mod demo)
Buka `index.html` dalam pelayar. Tanpa Firebase, aplikasi berjalan dalam **mod demo** dengan data rekaan yang disimpan dalam pelayar itu sahaja.
- Pentadbir/Guru: klik butang demo.
- Ibu bapa: tab **Ibu Bapa**, guna No. KP yang ditunjukkan dan PIN `DEMO26`.

## 2. Sambung Firebase (kegunaan sebenar)
Boleh guna projek sedia ada (`skjb-icthub`) atau projek baharu.

1. **Firebase Console → Authentication → Sign-in method** → hidupkan **Email/Password**.
2. **Firestore Database** → Create database (lokasi `asia-southeast1`).
3. **Firestore → Rules** → tampal peraturan dari Tetapan → Pangkalan data dalam aplikasi (atau bahagian `RULES` dalam fail). Gantikan `GANTI_DENGAN_EMEL_PENTADBIR@moe-dl.edu.my` dengan emel pentadbir utama. Publish.
4. **Authentication → Users → Add user**: cipta akaun pentadbir utama (emel yang sama seperti di langkah 3).
5. **Project settings → Your apps → Web app** → salin `firebaseConfig`.
6. Dalam `index.html`, cari baris berikut berhampiran bahagian atas skrip dan isikan:
   ```js
   const FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", projectId: "...", storageBucket: "...", messagingSenderId: "...", appId: "..." };
   const ADMIN_EMAILS = ["emel-pentadbir@moe-dl.edu.my"];
   ```
7. Muat naik `index.html` ke GitHub (contoh: folder `emarkah/` dalam repo `skjalanbintang/destarx`) dan hidupkan GitHub Pages. Tambah domain GitHub Pages dalam **Authentication → Settings → Authorized domains**.

## 3. Persediaan awal oleh pentadbir
1. Log masuk dengan akaun pentadbir.
2. **Tetapan → Ujian**: pilih bilangan ujian tahun ini (2 atau 3) dan namakan (cth. SUMATIF 1, SUMATIF 2, SUMATIF 3).
3. **Tetapan → Kelas / Subjek / Skala gred**: semak. Kelas lalai: Tahun 1–6 × ACHIEVER, BRILLIANT, CHAMPION, DYNAMIC, ENERGETIC (30 kelas); isi nama guru kelas. Import Excel memadankan nama kelas yang sama (cth. "6 ACHIEVER").
4. **Murid & PIN → Import Excel**: muat naik fail seperti `TAHUN 6.xlsx` (setiap helaian kelas). Murid, kelas dan (jika dipilih) markah ujian akan diimport. Ulang untuk setiap darjah.
5. **Tetapan → Pengguna**: daftar guru (satu persatu atau tampal senarai `NAMA, emel`). Beri guru kata laluan sementara; mereka boleh tukar melalui "Lupa kata laluan".
6. **Murid & PIN → Cetak senarai PIN**: edarkan PIN kepada ibu bapa.

## 4. Sepanjang tahun
- Guru: **Isi Markah** → pilih darjah (Tahun 1–6), kemudian tab kelas (Achiever, Brilliant, Champion, Dynamic, Energetic), tab ujian (Sumatif 1 / 2 / 3), kelas dan subjek, isi markah, kemudian tekan **Simpan markah** (atau Ctrl+S). Sel yang belum disimpan berwarna kuning, dan aplikasi memberi amaran jika guru cuba keluar sebelum menyimpan. Dua guru boleh isi subjek berbeza untuk kelas yang sama serentak.
- Setiap simpanan merekod **nama guru dan masa kemas kini terakhir** bagi setiap subjek; dipaparkan di Isi Markah dan Semakan.
- Pentadbir: **Semakan** → jadual kelas × subjek bagi setiap ujian (hijau lengkap, kuning separuh, merah belum diisi). Klik petak untuk senarai murid yang belum diisi dan untuk menetapkan guru subjek. Butang **Salin senarai (WhatsApp)** menyediakan mesej peringatan mengikut guru.
- **Graf Analisis**: taburan gred mengikut kelas, GPMP subjek, peratus lulus, GPK/GPD merentas ujian, taburan GP murid, keputusan murid, serta taburan gred dan purata markah bagi subjek terpilih.
- Pentadbir: **Tetapan → Paparan slip keputusan** → suis untuk papar/sembunyi item slip (No. KP, markah, gred, taksiran, jumlah, purata, GP, analisis, keputusan, kedudukan kelas/darjah, kehadiran, ulasan, tandatangan, graf ibu bapa). Kedudukan yang disembunyikan tidak dihantar ke portal ibu bapa langsung.
- Pentadbir: **Kunci** ujian apabila isian tamat, kemudian tandakan **Terbit** dan klik **Kemas kini portal ibu bapa**.
- Ibu bapa: log masuk dengan No. MyKid + PIN; boleh tambah lebih daripada seorang anak dan lihat semua ujian yang diterbitkan serta graf perkembangan.
- Tahun baharu: **Tetapan → Tahun akademik → Mula tahun baharu**. Data tahun lepas kekal.

## Peraturan pengiraan (sama seperti Excel TAHUN 6)
- Gred: A 82–100, B 66–81, C 50–65, D 35–49, E 20–34, F 0–19, TH = tidak hadir (boleh diubah di Tetapan).
- GP murid = purata nilai gred (A=1 … F=6); subjek TH dikira bernilai 6.
- GPMP subjek / GPK kelas / GPD darjah = purata nilai gred murid yang hadir.
- Keputusan: ada gred F → BELUM MENCAPAI TAHAP MINIMUM; selainnya LULUS.
- Kedudukan (KDK/KDT): murid lulus dahulu, kemudian GP terendah, kemudian jumlah markah tertinggi. Pentadbir menentukan subjek yang dikira untuk kedudukan bagi setiap darjah di **Tetapan → Subjek dikira untuk kedudukan**; slip tetap memaparkan jumlah dan GP semua subjek.

## Keselamatan
- Ibu bapa hanya boleh membaca dokumen keputusan anak mereka yang dikunci dengan No. MyKid + PIN (6 aksara rawak); senarai murid dan markah lain tidak boleh dibaca.
- Hanya pentadbir boleh mengubah tetapan, senarai murid dan menerbitkan portal. Guru boleh membaca dan mengisi markah.
