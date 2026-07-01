# Certificate Batch Generator

A single-page, client-side tool: upload a blank certificate PNG and an Excel
roster, and it generates a zip of individually named certificate PDFs. Runs
entirely in the browser — no server, no files uploaded anywhere — so it's
safe to host as a static GitHub Pages site.

## Put it on GitHub Pages

1. Create a new repository on GitHub (e.g. `certificate-generator`).
2. Add `index.html` (from this folder) to the repo root, then commit and push:

   ```bash
   git init
   git add index.html
   git commit -m "Add certificate batch generator"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

3. On GitHub: go to the repo's **Settings → Pages**, set **Source** to
   "Deploy from a branch", pick the `main` branch and `/ (root)` folder, then
   save.
4. After a minute or two, the tool will be live at:
   `https://<your-username>.github.io/<repo-name>/`

No build step, no dependencies to install — it's one HTML file that loads
SheetJS, jsPDF, and JSZip from a CDN.

## How it works

- **Step 1 / Step 2**: upload the blank certificate PNG and the roster
  `.xlsx`. The "Advanced" panel lets you pick the sheet and which columns map
  to timestamp / name / role, if they don't match the defaults
  (`Timestamp`, `Full Name`, `Officer Role Trained`).
- **Step 3**: click **Generate certificates**. For each row, it draws the
  name, role, and formatted date onto a copy of the template (erasing the
  placeholder text first), converts that to a PDF, and packages everything
  into `certificates.zip`, which downloads automatically.

## Template assumptions

The text-placement coordinates are calibrated to the standard Toastmasters
"Certificate of Completion" layout (NAME / TRAINING_DATE / ROLE placeholders
in the same positions as the reference template), scaled proportionally to
whatever size PNG you upload. If you use a differently laid-out template,
the placeholder text and new text may not land in the right spot — in that
case the coordinates in the `<script>` block (`NAME_LINE`, `ROLE_LINE`,
`DATE_CENTER`, and the matching `*_ERASE` rectangles) will need updating.

## Privacy

Nothing is uploaded anywhere. The PNG, the spreadsheet, and every generated
PDF stay in the browser tab and are assembled into the zip locally.
