# Checklist Penampilan Driver

Form harian driver (HP) + dashboard monitoring & tindak lanjut untuk admin.
Data masuk ke Google Sheet, foto ke Google Drive. Hosting gratis lewat GitHub Pages.

| File | Fungsi |
|---|---|
| `index.html` | Satu halaman, dua menu: **Isi Checklist** (form driver) dan **Dashboard Admin** (butuh PIN) |
| `apps-script.gs` | Backend: simpan data, baca data, update tindak lanjut |

## Setup (sekali saja)

1. Buka Google Sheet → **Extensions → Apps Script**. Hapus kode lama, tempel isi `apps-script.gs`.
2. Ganti `ADMIN_PIN` di baris atas dengan PIN rahasia Anda. Simpan.
3. Pilih fungsi **doPost** → **Run** → izinkan akses (Review permissions → Advanced → Go to project → Allow).
   Error `postData` setelah itu normal; yang penting izin Drive & Sheets sudah diberikan.
4. **Deploy → New deployment → Web app**: Execute as **Me**, Who has access **Anyone** → Deploy. Salin URL `/exec`.
5. Tempel URL itu ke `SCRIPT_URL` di **`index.html`** (sudah terpasang jika Anda memakai file dari percakapan ini).
6. Upload folder ini ke repo GitHub (Public) → **Settings → Pages** → Branch `main`, folder `/root` → Save.
   - Form driver: `https://<username>.github.io/<repo>/`
   - Dashboard admin: menu **Dashboard Admin** di halaman yang sama, atau langsung `https://<username>.github.io/<repo>/#dashboard`

> Setiap kali `apps-script.gs` diubah: **Deploy → Manage deployments → pencil → New version → Deploy**.
> Buka form lewat link `https://` di Chrome (bukan membuka file dari WhatsApp), agar kamera berfungsi.

## Aturan status kelayakan

| Kondisi | Status |
|---|---|
| Kesehatan "Sakit" | Tidak Layak Bertugas |
| ≥ 3 poin tidak sesuai, atau Kurang Fit + ada poin tidak sesuai | Perlu Ditindak |
| 1-2 poin tidak sesuai, atau Kurang Fit | Perlu Perhatian |
| Semua sesuai & sehat | Layak |

## Tindak lanjut (dashboard)

Klik baris driver → atur **Status** (Belum Ditindak / Dalam Proses / Selesai), **Tindakan**
(Teguran Lisan, SP, Dipulangkan, Pembinaan) dan **Catatan**. Tersimpan ke kolom di Sheet.

## Catatan keamanan

PIN dicek di sisi Apps Script, tetapi tertanam di URL permintaan dashboard. Cukup untuk penggunaan internal;
jangan bagikan link dashboard + PIN ke driver. Untuk keamanan lebih tinggi, batasi akses Sheet & Drive hanya ke admin.
