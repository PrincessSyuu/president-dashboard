# TODO - Struktur Dashboard M2IIR/M2IT

## Rencana implementasi
1. Rombak `index.html` menjadi layout baru:
   - Sidebar kiri: General, M2IR, M2IT, Settings
   - Topbar: search bar, profile/admin, notification icon
   - Main dashboard: General / Quick Access M2I / tabel terbaru
2. Tambahkan dummy data realistis (nama, jurusan, compatibility score, status submit, recommendation result).
3. Buat routing UI (tanpa framework) dengan logic JS:
   - tombol sidebar dan Quick Access mengubah halaman (General/M2IR/M2IT)
   - tiap halaman punya warna tema: General=biru, M2IR=ungu, M2IT=hijau
4. Implement filter/sort untuk dashboard M2IR dan M2IT:
   - filter dropdown: by score, by status, by latest submission
   - sortable/filterable user list (sorting sesuai dropdown)
5. General dashboard:
   - Total users
   - Total users sudah isi M2I
   - Total socializer users
   - Card statistik sederhana
   - Table/list user terbaru
6. Pastikan UI modern: rounded cards, soft shadows, responsive.
7. Verifikasi fungsi pencarian topbar (opsional filter global).
8. Uji buka `index.html` dan cek semua tombol.

