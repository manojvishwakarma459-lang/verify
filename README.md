# U-TECH Certificate Verification (free, GitHub Pages)

Students' certificates carry a QR code. Scanning it opens
`https://<your-site>/?id=UT26-XXXXXXXX` and shows **Verified / Not found / Revoked** with the student's details.

## Folder contents
| Path | Purpose | Upload to GitHub? |
|---|---|---|
| `index.html` | Public verification page | Yes |
| `data/certificates.json` | Encrypted certificate records | Yes |
| `assets/logo.png` | Your U-TECH crest (add it yourself) | Yes |
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
4. Step 3: paste/upload the student CSV → **Generate certificates**.
5. Download:
   - `certificates.json` → upload to the repo's `data/` folder (replace old file).
   - `IDs + links (CSV)` → your master list; use it for mail-merge into the certificate template.
   - `QR codes (ZIP)` → one 1000 px PNG per student, named `ID_Name.png`, to place on each certificate.
6. Print the **Certificate ID** under the QR on the certificate, so it can also be typed in manually.

CSV columns: `name, course, issue_date` (required) + `id, duration, grade, start_date, end_date, status` (optional). Dates `YYYY-MM-DD` or `DD-MM-YYYY`.

## Correcting or revoking
Put the existing `id` in the CSV row with corrected details (or `status` = `revoked`), load the current database, generate, and upload the new `certificates.json`.

## Security
- Each record is AES-256 encrypted with a key derived from its Certificate ID. The public JSON file reveals no names or courses; details appear only when someone has the real ID.
- IDs are 8 random characters (≈1 trillion combinations), so they cannot be guessed.
- Only people with access to your GitHub account can change records. Turn on 2-factor authentication on GitHub.
- Remove the demo record (`UT26-DEMO2026`) before going live: start your first batch **without** loading the bundled demo database.
