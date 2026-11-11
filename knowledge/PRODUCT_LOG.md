# LOG PRODUK & INFO — QJMOTOR

Catatan kronologis semua perubahan data produk, penambahan produk, koreksi, dan info penting.
**Aturan: setiap ada perubahan info produk di room ini, langsung catat di sini** (tanggal, tipe, deskripsi, sumber) — buat pertanggungjawaban & pengecekan ulang di kemudian hari.

Tipe entri: `[TAMBAH]` produk/info baru · `[UBAH]` revisi data · `[KOREKSI]` pembetulan fakta · `[INFO]` info penting non-produk.

---

## 2026-11-10

- `[KOREKSI]` **Viento 180 — touchscreen dashboard bukan fitur besar.** Menurut user (10 Nov): fungsinya cuma speedometer biasa, bedanya ganti menu info lewat layar sentuh; data yang tampil standar (trip distance, konsumsi/jarak bensin, dsb). Klaim guide "real-time vehicle diagnostics" jangan dijadikan angle utama konten — pakai sebagai visual-only atau pindah ke poin lain (bagasi, hybrid engine).
- `[INFO]` **Konteks room Claude "Ide Konten" + "Ide Headline" ditarik ke sini** → `knowledge/CONTENT_CONTEXT.md`: aturan tetap, kuota, jatah produk EP November, format brief, status terakhir (carousel Tourino 700 SX selesai, lanjut carousel Fort 250 Adventure).
- `[KOREKSI]` **Tourino 700 SX rem depan = 320 mm** — tabel spek guide sebelumnya "Dual 20 mm" (typo), diperbaiki jadi "Hydraulic Dual 320 mm Discs with Brembo Calipers" sesuai teks fitur di baris 48–51. Konfirmasi user 9 Nov 2026.
- `[INFO]` Typo sisa OCR dibersihkan: "Hydraulic Single 260 mm}Disc with ABS" → "260 mm Disc".
- `[TAMBAH]` **Line-up dashboard HTML** — dibuat `qjmotor-lineup.html` (root workspace): 16 produk, filter kategori, klik kartu = tanya detail ke chat. Sumber data: `knowledge/PRODUCT_GUIDE_20260609.md`.
- `[KOREKSI]` **"TVC" bukan kategori motor** — TVC = video iklan (Television Commercial). Kategori "Baru · TVC" di dashboard dihapus.
  - **Tourino 250 SX** → klasifikasi **Adventure**.
  - **Fort 180 R-Pro** → klasifikasi **Scooter**.
  - Sumber: koreksi user. Klasifikasi dicatat permanen di `AGENTS.md` → Proyek TVC.
- `[INFO]` **Produk TVC ditandai "PRODUK BARU"** — Tourino 250 SX & Fort 180 R-Pro tampil di dashboard dengan badge merah "PRODUK BARU — RILIS 5 DES 2026 · SPEK MENYUSUL" (dashed border, spek TBA). Spek menunggu kiriman QJ.
- `[UBAH]` **Dashboard → mode artifacts (ala Claude)** — `qjmotor-lineup.html` di-rename jadi `qjmotor-artifacts.html`, ditambah tab switcher: **Line-up 2026** & **Log Produk**. File lama dihapus.
- `[INFO]` **Log Produk tampil visual di dashboard** — tab "Log Produk" merender `knowledge/PRODUCT_LOG.md` sebagai timeline berwarna per tipe entri (TAMBAH/UBAH/KOREKSI/INFO). Live via fetch bila preview mendukung; fallback ke snapshot ter-embed di HTML.
- `[UBAH]` **Aturan klaim cc = angka nama produk** — untuk kepentingan konten, semua klaim cc disamakan dengan nama produk (Fort 180 → "180 cc", Tourino 250 → "250 cc", SRV 600 V → "600 cc"), bukan displacement aktual. Aturan dicatat di `AGENTS.md` → Aturan konten. Dashboard line-up diupdate: badge cc 16 kartu kini menampilkan klaim nama produk (termasuk 2 produk TVC: Tourino 250 SX → 250, Fort 180 R-Pro → 180).
- `[UBAH]` **Styling dashboard untuk render standalone** — saat dibuka di luar frame chat (browser/panel preview), font jatuh ke default serif (Times) tanpa tema → terlihat jelek. Fix: font stack sistem, fallback warna adaptif light/dark (`prefers-color-scheme`) via custom props `--qj-*`, `color-scheme: light dark`. Var tema frame Hermes tetap diprioritaskan (tidak ditimpa).
- `[INFO]` **Dashboard diupload ke Google Drive** — folder "QJMOTOR" (My Drive) berisi `QJMOTOR Product Room.html` (sumber) + `QJMOTOR Product Room (Preview).pdf` (render untuk preview HP).
- `[UBAH]` **Folder Drive QJMOTOR di-share publik** — permission "anyone with link" role reader (permintaan user): link bisa dibuka tanpa login.
- `[UBAH]` **Auto-sinkron Dashboard → Drive** — `tools/sync_drive_pdf.py` + cron Hermes "QJMOTOR Drive Sync" (tiap jam, mode script tanpa LLM). Alur: hash HTML berubah → render PDF via headless Chrome → `files.update` kedua file Drive (ID tetap, link tidak berubah). Diam saat tidak ada perubahan. Catatan teknis: Chrome CLI mengabaikan `@page size` → PDF A4 portrait (ramah HP); background ikut via `print-color-adjust: exact`.
- `[UBAH]` **Hosting web GitHub Pages** — repo publik `pradiptamanuputty-oss/qjmotor-product-room`, live di https://pradiptamanuputty-oss.github.io/qjmotor-product-room/. Isi: `index.html` (dashboard) + `knowledge/PRODUCT_LOG.md` (log live via fetch). Deploy dari branch main.
- `[UBAH]` **Sinkron otomatis jadi 3 arah** — script sinkron kini juga push ke repo GitHub Pages setiap kali dashboard berubah (commit + push otomatis), jadi web selalu terupdate ≤ 1 jam.
