<div align="center">
  <img src="https://www.pdfpro.co.in/icon.png" alt="PDF Pro Logo" width="120" />
  <h1>WASM PDF Compressor</h1>
  <p><strong>A 100% private, client-side WebAssembly engine for compressing PDFs in the browser.</strong></p>
  
  [![Website](https://img.shields.io/badge/Hosted_UI-Live_Demo-blue?style=for-the-badge)](https://www.pdfpro.co.in/tools/compress-pdf)
  [![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
</div>

---

## 🛑 The Problem with Modern PDF Compressors

Have you ever tried to compress a bank statement, tax return, or medical report?

If you use popular tools like *iLovePDF* or *Smallpdf*, **your highly sensitive documents are uploaded to an external cloud server.** Your Personally Identifiable Information (PII) is processed on a server you don't control, often leaving behind traces or metadata.

## ⚡ The Solution: Client-Side WebAssembly

This repository outlines the architecture for a completely offline, client-side PDF compressor. By leveraging WebAssembly (WASM), we compile native C/C++ PDF processing libraries directly into browser-executable bytecode.

**How it works:**
1. The user selects a PDF file.
2. The file is loaded entirely into the browser's local memory (RAM).
3. The WASM engine parses the PDF structure, downsamples high-resolution raster images, and strips invisible metadata.
4. The optimized PDF is regenerated locally and downloaded.
5. **No network requests are ever made. Your data never leaves your laptop.**

## 🚀 Live Demo (Hosted UI)

Don't want to clone the repo or set up a local build environment? 

You can use the fully hosted, production-ready GUI right now. It uses the exact same WebAssembly architecture described here, ensuring your documents remain completely private.

👉 **[Try the Live WebAssembly Compressor](https://www.pdfpro.co.in/tools/compress-pdf)**

*Note: You can literally turn off your Wi-Fi after the page loads, and the tool will still compress your files perfectly.*

## 💻 Technical Architecture

The core of this engine relies on bridging JavaScript and WASM using `pdfjs-dist` and custom binary manipulation techniques.

### Key Optimizations:
*   **Lossless Text Retention:** Vector graphics and fonts are bypassed during compression, ensuring text remains perfectly crisp for ATS scanners and manual review.
*   **Intelligent Image Downsampling:** Raster images are targeted and downsampled to optimal DPIs (e.g., 144 DPI) using native browser canvas APIs.
*   **Metadata Stripping:** Unnecessary object streams, orphaned resources, and XMP metadata are aggressively pruned from the document dictionary.

## 🛠️ Usage / Implementation

If you want to integrate this approach into your own Next.js or React application, the core flow looks like this:

```javascript
// Example abstract flow of client-side compression
import { getDocument } from 'pdfjs-dist';

async function compressPDFLocally(file) {
  // 1. Load file into local memory array buffer
  const arrayBuffer = await file.arrayBuffer();
  
  // 2. Parse using local WASM engine
  const pdfDoc = await getDocument(arrayBuffer).promise;
  
  // 3. Iterate pages and apply downsampling to image streams...
  // (Core optimization logic)
  
  // 4. Return new binary Blob
  return new Blob([compressedBytes], { type: 'application/pdf' });
}
```

## 🌐 Ecosystem & Other Tools

This architecture isn't just for compression. We've applied the same strict, privacy-first, zero-upload philosophy to other common document utilities:

*   [Word to PDF Converter](https://www.pdfpro.co.in/tools/word-to-pdf) - Lock formatting locally.
*   [PDF Merge Engine](https://www.pdfpro.co.in/tools/merge-pdf) - Combine bank statements offline.
*   [Medical Report Analyzer](https://www.pdfpro.co.in/tools/medical-report-analyzer) - AI-powered local extraction.

## 🤝 Contributing

We believe document privacy should be the default, not a premium feature. If you have ideas for improving the WASM compression algorithms or reducing the final payload size, please open an issue or submit a PR!

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
