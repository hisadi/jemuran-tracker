# 👔 Clothing Tracker

Track status pakaian kamu — digantung, keranjang kamar, keranjang laundry, atau lemari.

---

## Setup Supabase

### 1. Buat tabel `clothes`

Buka **SQL Editor** di Supabase, jalankan:

```sql
create table clothes (
  id           uuid primary key default gen_random_uuid(),
  name         text not null,
  category     text not null default 'lainnya',
  status       text not null default 'digantung',
  status_since timestamptz not null default now(),
  created_at   timestamptz default now()
);

-- Row Level Security (kalau mau private, aktifkan auth dulu)
-- Untuk sementara tanpa auth, bisa pakai policy public:
alter table clothes enable row level security;

create policy "Public access"
  on clothes for all
  using (true)
  with check (true);
```

### 2. Isi kredensial

Di `index.html`, ganti:
```js
const SUPABASE_URL = 'https://YOUR_PROJECT_ID.supabase.co'
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY'
```

---

## Deploy ke GitHub Pages

```bash
git init
git add index.html README.md
git commit -m "init: clothing tracker"
git branch -M main
git remote add origin https://github.com/hisadi/hisadi-clothing.git
git push -u origin main
```

Lalu aktifkan GitHub Pages di Settings → Pages → Branch: main.

---

## Fitur

- 4 status: Digantung → Keranjang Kamar → Keranjang Laundry → Lemari
- Warning merah kalau digantung ≥4 hari
- Drag & drop antar kolom
- Notifikasi browser
- Sync semua device via Supabase
