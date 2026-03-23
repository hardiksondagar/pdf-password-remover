# PDF Password Remover

A single-page web app that removes **open passwords** from PDFs entirely in the browser. Files and passwords never leave your device.

## Features

- **True decryption** — Uses [QPDF](https://qpdf.sourceforge.io/) compiled to WebAssembly ([`@neslinesli93/qpdf-wasm`](https://www.npmjs.com/package/@neslinesli93/qpdf-wasm)), so the unlocked PDF keeps the original layout: selectable text, vector graphics, links, and forms where the PDF supports it.
- **Batch processing** — Select multiple PDFs; the same password is tried for each file.
- **Per-file status** — See success or failure for every file in a table.
- **Smart download** — If **exactly one** file unlocks successfully, you get a **single PDF**. If **two or more** unlock, results are bundled in a **ZIP** (`unlocked_pdfs.zip`).
- **Privacy** — No server upload; processing runs locally in your browser.
- **UI** — [Tailwind CSS](https://tailwindcss.com/) (via CDN).

## How it works

1. Your PDF bytes are written into the WASM module’s virtual file system.
2. QPDF runs with `--password=…` and `--decrypt`, producing an unencrypted PDF.
3. **JSZip** packages multiple outputs when needed; otherwise a direct PDF blob is used for download.

Scripts are loaded from CDNs (Tailwind, qpdf-wasm, JSZip). The QPDF WebAssembly binary (~1.3 MB) is fetched on first use.

## Usage

1. Open `index.html` in a modern browser (or serve the folder over HTTP — see below).
2. Choose one or more `.pdf` files.
3. Enter the **open password** (leave blank if the password is empty).
4. Click **Remove Password**.
5. When processing finishes, use **Download PDF** (single success) or **Download All as ZIP** (multiple successes).

## Running locally

Serving over HTTP avoids some browsers’ restrictions on `file://` and matches how you would deploy the app:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` (or open `index.html` directly if your browser allows it).

## Requirements

- A modern browser with JavaScript and WebAssembly enabled.
- Network access the first time, so the CDN can load scripts and the QPDF `.wasm` file.

## Limitations

- You must **know the password**; the tool does not crack or guess passwords.
- **One password per run** applies to all selected files (typical for a batch you locked with the same password).
- **Encryption** must be something QPDF can handle; some rare or damaged PDFs may fail.
- Very large PDFs may be slow or memory-heavy in the browser.

## License

MIT
