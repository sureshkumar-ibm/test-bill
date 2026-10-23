# Local Billing PWA

Starter offline-first Android billing PWA based on the supplied Excel workbook, sample PDF and VBA logic.

## Included
- Mobile invoice form with multiple line items
- Basic = quantity × rate
- CGST/SGST default to 9% each; rates can be changed
- Indian amount-in-words, including lakh/crore and paise
- Print layout based on the provided invoice PDF; use Chrome/Android print dialog and choose Save as PDF
- Local invoice records in IndexedDB
- History CSV with exact workbook headers: `S.No, Supplier Name, GSTIN, HSN, Qunatity, Invoice No, Date, Basic, CGST 9%, SGST 9%, Total`
- Per-item history rows; Supplier Name and GSTIN values use buyer details, as requested
- JSON backup and merge-style restore
- Offline app-shell caching

## Important
- The supplied VBA is not executed by the web app; its behavior is recreated in JavaScript.
- Supplier details are currently hard-coded to the sample workbook values (Test Company, etc.). Change them in `app.js` before production use if needed.
- PDF output is a browser print layout prototype. Compare and adjust it against the original PDF before using for live billing.
- Tax is rounded per item to paise for history rows. Verify the workbook's exact tax rounding behavior.
- IndexedDB records can be erased if browser/site data is cleared. Export backups regularly.
- This is a prototype, not tax/accounting compliance certification.

## Install on Android
A full PWA requires HTTPS (or localhost) for service worker installation. A file opened directly from `file://` is not a full PWA.
1. Extract the ZIP and publish these static files on an HTTPS static host you control (for example, GitHub Pages). The host serves app files only; invoice records remain in the phone's browser storage.
2. Open the HTTPS URL in Android Chrome while online.
3. Chrome menu → Install app / Add to Home screen.
4. Open it once online; then test with Airplane mode enabled.
5. Backup tab → Export full backup. Upload the JSON file to Google Drive manually.
6. To restore, download the JSON backup from Drive, select it in the app, and tap Restore.

## Desktop local test
Run `python -m http.server 8000` from this directory and open `http://localhost:8000`.
