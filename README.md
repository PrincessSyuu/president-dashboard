# President University — Admin Dashboard (M2IR / M2IT) By Elbert

Demo dashboard + alur QR → *Mind To Major* → Admin Analytics.

## Tech Stack
- **Frontend:** Pure `HTML/CSS/JS` (single-file admin) + `mindtomajor.html`
- **Auth:** Firebase **Google Sign-In** (Firebase Auth)
- **Database:** Firebase **Cloud Firestore**
- **Chart:** Chart.js (CDN)

## Project Files
- `index.html`
  - Admin dashboard (sidebar/topbar)
  - Tabs: **General / M2IR / M2IT**
  - Reads Firestore and populates M2IR/M2IT tables + counts
- `mindtomajor.html`
  - Page yang diakses dari QR
  - Login Google (Firebase Auth)
  - Input `points` dan menulis hasil ke Firestore
- `firestore_rules_and_sample.md`
  - Contoh struktur koleksi & rules Firestore (MVP)

## Firestore Schema
Collection: `submissions`
- Document id: `token` (dari QR)
- Fields (MVP):
  - `email: string`
  - `points: number`
  - `role: string` (`M2IR` atau `M2IT`)
  - `recommendationResult: string` (sama dengan `role` untuk MVP)
  - `latestSubmission: Timestamp`
  - `createdAt: Timestamp`
  - `updatedAt: Timestamp`

## Setup Firebase (WAJIB)
1. Buat project di **Firebase Console**.
2. Aktifkan **Google Sign-In** di Firebase Auth.
3. Buat Firestore Database.
4. Set **Firestore rules** (lihat `firestore_rules_and_sample.md`).

### Isi Firebase config di 2 file
**A) `mindtomajor.html`**
Cari bagian:
```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```
Ganti semua `YOUR_*` dengan value dari Firebase Console (Web app).

**B) `index.html`**
Cari bagian:
```js
window.__FIREBASE_ADMIN_CONFIG__ = window.__FIREBASE_ADMIN_CONFIG__ || {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```
Ganti semua `YOUR_*`.

> Catatan: Ini demo client-side. Untuk produksi, security rules & access kontrol harus diperketat.

## Cara pakai (End-to-End)
### 1) Buat QR Token
QR harus mengarah ke:
```
mindtomajor.html?token=<TOKEN>
```

Contoh token: `abcd1234`.

### 2) User submit (Mind To Major)
Buka URL dari QR → login Google → masukkan `points` → klik **Submit ke Admin**.
- Rule demo:
  - `points > 10` ⇒ `M2IR`
  - selain itu ⇒ `M2IT`

### 3) Admin melihat dashboard
Buka `index.html` (admin dashboard).
- Tab **M2IR** menampilkan dokumen Firestore `role == 'M2IR'`.
- Tab **M2IT** menampilkan dokumen Firestore `role == 'M2IT'`.

## Publish di GitHub Pages
- Pastikan file di-root (mis. deploy ke GitHub Pages).
- Karena semuanya pure HTML, tidak ada build step.

## Troubleshooting
- Data tidak muncul di tab M2IR/M2IT:
  - Pastikan config Firebase sudah diisi di `mindtomajor.html` dan `index.html`.
  - Pastikan Firestore rules mengizinkan read sesuai auth.
  - Pastikan QR token yang dipakai sama dengan document id yang ditulis.

## A11y & Style
- UI memakai warna tema berbeda:
  - **General:** biru
  - **M2IR:** ungu/pink
  - **M2IT:** hijau/purple
- Komponen cards & tabel dibuat rounded dengan soft shadows.

