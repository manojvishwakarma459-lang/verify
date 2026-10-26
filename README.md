# U-TECH Certificate Verification (free, GitHub Pages)

Students' certificates carry a QR code. Scanning it opens
`https://manojvishwakarma459-lang.github.io/verify/?id=UTCCS-2026-2058-XXXXXX` and shows **Verified / Not found / Revoked** with the student's details.

## Folder contents
| Path | Purpose | Upload to GitHub? |
|---|---|---|
| `index.html` | Public verification page | Yes |
| `data/certificates.json` | Encrypted certificate records | Yes |
| `assets/logo.png` | U-TECH crest | Yes |
| `.nojekyll` | Tells GitHub to serve files as-is | Yes |
| `tools/generator.html` | Admin tool: creates IDs, QR codes, database | **No — keep on your PC** |

## One-time setup (≈10 minutes)
1. Create a free account at github.com (e.g. `utech-cadcam`).
2. **New repository** → name it `verify` → Public → Create.
3. **Add file → Upload files** → drag `index.html`, `.nojekyll`, `data/` and `assets/` → Commit.
4. **Settings → Pages** → Source: *Deploy from a branch* → Branch `main` / `(root)` → Save.
5. After ~1 minute your site is live at `https://utech-cadcam.github.io/verify/`.
   Test it: `https://utech-cadcam.github.io/verify/?id=UT26-DEMO2026`

**Optional custom domain** (looks more official): in your domain DNS add a CNAME record
`verify` → `utech-cadcam.github.io`, then enter `verify.u-tech.in` in Settings → Pages → Custom domain and tick *Enforce HTTPS*.

## Issuing certificates (every batch)
1. Open `tools/generator.html` on your PC (double-click; works in Chrome/Edge).
2. Step 1: enter your site address (remembered next time).
3. Step 2: load the current `data/certificates.json` (**always do this**, or old records are lost).
4. Step 3: paste/upload the student CSV → **Generate**.
5. Download:
   - `certificates.json` → upload to the repo's `data/` folder (replace old file).
   - `QR badges (ZIP)` → one 1000 px badge per student (`2058_NAME.png`) with QR, Certificate No. and code. Place it on the certificate in Canva (left side, below CERTIFICATE NO.).
   - `Master CSV` → keep safely; it holds every certificate's verification code.

CSV columns: `cert_no, name, course, issue_date` (required) + `module, grade, duration, status, code` (optional). `cert_no` can be `2058` or `UTCCS | 2026 | 2058`; dates `DD-MM-YYYY`.

Each certificate gets a 6-character verification **code** (e.g. `FWC3ZR`) on its QR badge. Because certificate numbers are sequential, the code is what stops anyone from looking up other students' certificates.

## Correcting or revoking
Repeat the row with the same `cert_no` and existing `code` with corrected details (or `status` = `revoked`), load the current database, generate, and upload the new `certificates.json`.

## Security
- Each record is AES-256 encrypted with a key derived from its Certificate ID. The public JSON file reveals no names or courses; details appear only when someone has the real ID.
- Each certificate's 6-character code (≈1 billion combinations) cannot be guessed, even though certificate numbers are sequential.
- Only people with access to your GitHub account can change records. Turn on 2-factor authentication on GitHub.
