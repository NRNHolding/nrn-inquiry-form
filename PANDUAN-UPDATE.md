# Panduan Update Inquiry Form — Versi 2

Update ini menambah: **Referral, Jenis Inquiry, Tanggal Acara**, mengganti status
**Wait for Confirmation → 📝 Quotation**, dan menambah **Customer Database**,
**filter/pencarian**, **conversion rate**, serta **reminder follow-up (lead aging)**.

Ada 2 bagian: **Backend (Apps Script)** dan **Frontend (form HTML)**.

---

## Status saat ini

✅ **Sudah:** kode `Sosmed KPI.gs` dan `Dashboard.gs` di Apps Script-mu sudah berisi
versi baru (Quotation + Customer Database). Backup di Dropbox `File .gs/` sudah
disamakan dengan Apps Script (nama file & isi sama).

Folder `File .gs/` sekarang berisi tepat 5 file yang mirror Apps Script-mu:
`Config.gs · Sosmed KPI.gs · Dashboard.gs · Formatting.gs · Code.gs`
(File lama yang sudah digabung/tak terpakai — `3_Dashboard`, `FINAL_Dashboard`,
`Fix_Merged`, `Sales_Config`, `Sales_Push` — sudah dihapus.)

---

## BAGIAN 1 — Backend: langkah yang MASIH perlu dijalankan

Buka **Google Sheet NRN** → **Extensions › Apps Script**, lalu:

1. **Cek `Formatting.gs`** — saat kamu export ke txt, file ini kosong (0 byte).
   Pastikan di editor Apps Script isinya **tidak kosong**. Kalau kosong / masih versi
   lama, paste isi `File .gs/Formatting.gs` dari Dropbox (supaya baris Quotation
   ikut diberi warna). Sekalian hapus file kosong **`untitled.gs`** kalau ada.

2. Jalankan **`migrateInquirySheetV2`** sekali (dropdown fungsi → Run):
   menambah 3 kolom (Referral, Jenis Inquiry, Tanggal Acara) ke `📋 Inquiry Tracker`
   **tanpa hapus data lama**, dan ubah status lama `⏳ Wait for Confirmation` → `📝 Quotation`.

3. Jalankan **`rebuildCustomerDatabaseNow`** sekali → membuat tab `👥 Customer Database`.

4. **Re-deploy Web App** (WAJIB, kalau belum):
   **Deploy › Manage deployments** → deployment aktif → pensil (Edit) →
   Version: **New version** → **Deploy**. URL Web App tetap sama.

---

## BAGIAN 2 — Frontend (Form HTML)

File: `deploy/nrn-inquiry-form/index.html` (sudah versi baru; master
`File .html/NRN-Inquiry-Form.html` ikut disinkronkan).

1. Commit & push `index.html` ke repo GitHub Pages `nrn-inquiry-form`.
2. Buka https://nrntimotius.github.io/nrn-inquiry-form/ → hard refresh (Ctrl+Shift+R).

---

## Cek hasil

- [ ] Field baru muncul: Jenis Inquiry, Tanggal Acara, Referral (form & edit).
- [ ] Status dropdown sekarang **📝 Quotation**.
- [ ] KPI bertambah: **📈 Conversion**.
- [ ] Tabel inquiry ada filter/pencarian; baris Quotation > 7 hari berwarna merah (🔥).
- [ ] Tab **👥 Customer Database** tampil & berisi customer unik brand tsb.
- [ ] Submit 1 inquiry uji → masuk ke `📋 Inquiry Tracker` (13 kolom) & `👥 Customer Database`.

## Catatan
- Lead aging "perlu follow up" jika Quotation > **7 hari**. Ubah di `index.html`:
  `const AGING_DAYS = 7;`.
- Customer Database digabung per **Brand + Nama Customer** (huruf besar/kecil diabaikan).
