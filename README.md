# SIBAKTI Kemenag Futuristik Ready

Paket ini memakai gambar BK Madrasah sebagai background login utama dan tetap memakai database Google Spreadsheet.

## Isi

```text
index.html
wrangler.jsonc
assets/images/bg-login-bk-madrasah.png
apps-script/SIBAKTI_KemenagFuturistikPatch.gs
SCHEMA.md
README.md
```

## Cara upload ke GitHub

Upload semua file/folder ke root repository yang terhubung Cloudflare:

```text
sibakti-madrasah/
├── index.html
├── wrangler.jsonc
├── README.md
├── SCHEMA.md
├── assets/
│   └── images/
│       └── bg-login-bk-madrasah.png
└── apps-script/
    └── SIBAKTI_KemenagFuturistikPatch.gs
```

## Apps Script

1. Buka Apps Script.
2. Paste isi `apps-script/SIBAKTI_KemenagFuturistikPatch.gs` di bawah `Code.gs` lama.
3. Tambahkan action berikut di dalam `doPost(e)` setelah `const action`:

```js
if (action === 'getPublicAppearance') return json_(getPublicAppearance_());
if (action === 'saveAppAppearance') return json_(saveAppAppearance_(payload.token, payload.data || {}));
if (action === 'portfolioSummary') return json_(portfolioSummary_(payload.token, payload.studentId));
if (action === 'listPortfolioItems') return json_(listPortfolioItems_(payload.token, payload.type, payload.studentId));
if (action === 'savePortfolioItem') return json_(savePortfolioItem_(payload.token, payload.type, payload.data || {}));
if (action === 'verifyPortfolioItem') return json_(verifyPortfolioItem_(payload.token, payload.type, payload.portfolioId, payload.approved));
```

4. Jalankan sekali:

```js
setupSibaktiRolePortfolioUpgrade()
```

5. Deploy ulang Apps Script.

## Catatan penting

- Background login default: `assets/images/bg-login-bk-madrasah.png`.
- Hanya role `SUPERADMIN` yang bisa mengubah background/tampilan nasional dari menu Pengaturan Sistem.
- Guru BK dan Siswa hanya menerima tampilan yang sudah ditentukan Superadmin.
