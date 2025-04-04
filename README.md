# PDF Password Remover

A browser-based application to remove passwords from PDF files entirely client-side, with no server processing required.

## Features

- Remove password protection from PDF files
- **Multiple file processing** - upload and process multiple PDFs at once
- Process files entirely in the browser (no server upload)
- Maintain visual appearance of the PDF
- **Track status** of each file's processing success or failure
- **ZIP download** for batch processing results
- Modern UI with Tailwind CSS
- Private and secure - your files never leave your computer

## How it Works

This application uses modern web technologies to process PDFs directly in your browser:

1. **PDF.js**: Mozilla's PDF rendering engine for decrypting the password-protected PDF
2. **PDF-Lib**: For creating a new unencrypted PDF
3. **JSZip**: For packaging multiple PDFs into a single download
4. **Tailwind CSS**: For the responsive user interface

## Usage

1. Open `index.html` in your web browser
2. Select one or more password-protected PDF files
3. Enter the PDF password (same password will be used for all files)
4. Click "Remove Password"
5. Monitor the processing status for each file
6. Download the unlocked PDFs as a ZIP archive when processing completes

## Running the Application

You can run the application locally using Python's built-in HTTP server:

```
python3 -m http.server 8000
```

Then visit http://localhost:8000 in your browser.

## Privacy

All processing happens directly in your web browser:
- Your PDFs are never uploaded to any server
- Your password stays private and is only used locally
- The unlocked PDFs are generated entirely in your browser

## Limitations

- This approach converts PDF pages to images before placing them in a new PDF document
- This preserves visual appearance but may lose:
  - Text selection/copy functionality
  - Form fields
  - Hyperlinks
  - Document structure
- A single password is used for all files in batch processing

## Python Version

This project also includes a Python version (`remove_pdf_password.py`) which provides more complete PDF processing with full content preservation.

## Requirements for Browser Version

Any modern web browser with JavaScript enabled should work. No additional installation required.

## License

MIT