# RideNova 🚗

Ride-hailing modern (inspirasi Gojek, branding original) — React + Vite + Express + Socket.IO + SQLite + Leaflet.

## Fitur
- Auth JWT (customer & driver)
- Real-time order + driver matching (Haversine, radius 5km)
- Real-time driver location
- Real-time chat (delivered/read)
- Rating & earnings
- Map OpenStreetMap (gratis, tanpa API key)
- Dark mode, mobile-first UI
- Simulate GPS movement untuk development

## Requirements
- Node.js >= 18
- npm

## Install & Run

### 1) Backend
```bash
cd server
npm install
npm run dev
```
Server berjalan di http://localhost:4000

### 2) Frontend (terminal baru)
```bash
cd client
npm install
npm run dev
```
Buka http://localhost:5173

### 3) Demo 2 browser
- Browser A (Incognito 1): buka `http://localhost:5173/driver/register` → daftar driver → toggle ONLINE → di halaman Dashboard.
- Browser B (Incognito 2): buka `http://localhost:5173/register` → daftar customer → booking.
- Pilih pickup & tujuan dari preset (misal: Monas, Grand Indonesia).
- Klik "Pesan Sekarang".
- Browser A menerima order → klik "Terima".
- Browser B melihat driver & tracking peta.
- Di dashboard driver, buka order → klik "Simulate Movement" → customer melihat marker bergerak real-time.
- Chat: buka tombol 💬.

## Struktur Env (opsional)
Buat `server/.env`:
```
PORT=4000
JWT_SECRET=ubah-ini-di-produksi
```

## Konfigurasi harga
Edit `server/config/index.js`:
```js
pricing: { baseFare: 5000, pricePerKm: 3000, minimumFare: 8000 }
matching: { searchRadiusKm: 5 }
```

## Struktur DB (SQLite, auto-created)
`server/database/ridenova.db` — tabel: users, drivers, vehicles, orders, locations, messages, ratings.

## Migrasi ke PostgreSQL
Semua query terisolasi di `server/services/*` dan `server/database/db.js`. Ganti
`better-sqlite3` dengan `pg`, sesuaikan sintaks SQL (mis. `AUTOINCREMENT` → `SERIAL`,
`?` → `$1`). Struktur controller & socket tidak perlu diubah.