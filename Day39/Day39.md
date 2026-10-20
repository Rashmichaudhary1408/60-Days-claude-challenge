# Day 39: Build PDF Splitter & Merger

**Create a Premium Browser-Based PDF Utility**

---

## 1. What I built

A single-file web app, `pdf-splitter-merger.html`, with two tools:

- **PDF Splitter**: upload a PDF, see a thumbnail of every page, then split it by ranges, split points, a fixed page count, or a visual selection.
- **PDF Merger**: add several PDFs, put them in order, and download one combined file.

Everything runs in the browser with client-side JavaScript. No file is uploaded to a server.

**Deliverables**

| File | Purpose |
|---|---|
| `pdf-splitter-merger.html` | The complete application (HTML, CSS and JS in one file) |
| `pdf-splitter-merger-poster.png` | A poster showing every tested step with real screenshots |
| `pdf-splitter-merger-poster.html` | Source of the poster |

---

## 2. Why this project matters

Most online PDF tools make you upload private documents (contracts, invoices, IDs) to someone else's server. A browser-only tool avoids that entirely, and it is also a good exercise in:

- working with binary data (`ArrayBuffer`, `Blob`) in JavaScript
- using two PDF libraries that do different jobs
- designing a polished, accessible UI without a framework
- validating messy user input and explaining errors clearly

---

## 3. Tech stack

| Need | Tool | Notes |
|---|---|---|
| Create, copy and merge PDF pages | **pdf-lib 1.17.1** | Loads from cdnjs |
| Render page thumbnails | **pdf.js 3.11.174** | Draws pages onto `<canvas>` |
| UI | Plain HTML, CSS, JavaScript | No framework, no build step |

**Division of labor.** pdf.js is good at *drawing* pages but cannot edit a PDF. pdf-lib is good at *editing* but cannot draw. The app uses each for what it does best: pdf.js for thumbnails, pdf-lib for the actual split and merge.

---

## 4. Features

### PDF Splitter

- Drag-and-drop or file picker upload
- Automatic page count and a lazy-loaded thumbnail for every page
- Click to select a page, Shift+click to select a range
- Four split modes:
  1. **Page ranges**: `1-3, 5, 9-` creates one file per range (`9-` means page 9 to the end)
  2. **After pages**: `3, 7, 12` cuts the document after those pages
  3. **Every N pages**: fixed-size chunks
  4. **Selected pages**: all selected pages go into one new PDF
- Live result preview before anything runs
- Each thumbnail gets a tag (F1, F2, F3) showing which output file it will land in
- Invalid input is highlighted in red with a specific message
- Preview and download each output file

### PDF Merger

- Drag-and-drop or file picker, with the option to keep adding files
- Each file shows a first-page preview, page count and size
- Reorder by dragging, or with up/down buttons for keyboard users
- Summary of total files, total pages and approximate output size
- Merge, preview and download

### Experience

- Dark mode (follows the system setting, with a manual toggle)
- Processing overlay with spinner, and toast notifications
- Responsive layout
- Keyboard focus styles, ARIA roles and live regions, reduced-motion support
- Shortcuts: `Alt+1` Split, `Alt+2` Merge, `Ctrl+Enter` run the current tool

---

## 5. How it works

### 5.1 Reading a PDF

```js
const buf  = await file.arrayBuffer();
const pdf  = await pdfjsLib.getDocument({ data: buf.slice(0) }).promise;
const pages = pdf.numPages;
```

`buf.slice(0)` passes a copy to pdf.js, because pdf.js can take ownership of the buffer it is given. The original is kept for pdf-lib.

### 5.2 Thumbnails

```js
async function renderThumb(pdf, n, canvas, w) {
  const page = await pdf.getPage(n);
  const base = page.getViewport({ scale: 1 });
  const vp   = page.getViewport({ scale: w / base.width });
  canvas.width = vp.width;
  canvas.height = vp.height;
  await page.render({ canvasContext: canvas.getContext('2d'), viewport: vp }).promise;
}
```

An `IntersectionObserver` calls this only when a thumbnail scrolls near view, so long documents open quickly.

### 5.3 Turning user input into a plan

Every split mode produces the same structure, a list of files with their page numbers:

```js
{ files: [{ label: 'Pages 1–3', pages: [1,2,3] }, ...], errs: [], bad: false }
```

The preview, the tags on thumbnails and the actual split all read from this one plan, so what the user sees is exactly what they get.

### 5.4 Splitting with pdf-lib

```js
const src = await PDFDocument.load(buf, { ignoreEncryption: true });
const out = await PDFDocument.create();
const copied = await out.copyPages(src, pageIndexes); // zero-based
copied.forEach(p => out.addPage(p));
const bytes = await out.save();
```

### 5.5 Merging

Same idea: create an empty document, then copy every page of every file in the chosen order.

### 5.6 Downloading

```js
const url = URL.createObjectURL(new Blob([bytes], { type: 'application/pdf' }));
const a = Object.assign(document.createElement('a'), { href: url, download: name });
a.click();
```

---

## 6. Design decisions

- **Palette:** cool grey-blue paper, deep ink text, a strong blue accent, and a red "cut" color used for split markers. The logo is half blue, half red, a split page.
- **Type:** Georgia for headings, a clean system sans-serif for the interface. System fonts keep the app working offline.
- **Structure as information:** the F1/F2/F3 tags and the red-bordered invalid field are there to communicate state, not to decorate.
- **Copy:** buttons say what happens ("Split PDF", "Merge & download"), and errors say what is wrong and how to fix it.

---

## 7. Testing

I ran the app in headless Chromium (Playwright) using three generated sample PDFs, then checked the downloaded files by reopening them.

| Test | Result |
|---|---|
| Load a 12-page PDF | 12 pages detected, all thumbnails rendered |
| Shift+click pages 2 to 5 | Pages 2, 3, 4, 5 selected |
| Range `1-3, 5, 9-` | Previewed as 3 files |
| Range `3-1, 99, x` | Field highlighted red with errors |
| Run the split | Output files had **3, 1 and 4** pages |
| Every 4 pages | Previewed as 3 equal files |
| Merge three PDFs (12 + 5 + 4 pages) after reordering | Output had **21** pages |
| Dark mode | Both tools render correctly |
| Browser console | No errors |

**Not tested:** drag-and-drop reordering, the Preview buttons, password-protected PDFs, and very large files.

---

## 8. Problems I hit and what I learned

1. **"Works offline" has limits in a single file.** The libraries load from a CDN, so the first load needs internet. After that it works offline only if the browser has cached them. For guaranteed offline use, download the two library files, keep them next to the HTML file, and point the `<script>` tags at them.
2. **pdf.js workers and `file://`.** A web worker cannot always be loaded straight from a CDN when the page is opened as a local file. The app creates a small blob worker that imports the CDN worker script to get around this.
3. **Buffers can be consumed.** Passing the same `ArrayBuffer` to pdf.js and then pdf-lib failed until I gave pdf.js its own copy.
4. **One plan, many consumers.** Building a single "plan" object made validation, preview, thumbnail tags and processing consistent, with much less code.
5. **Test environment mismatch.** My test browser was older than the pdf.js build I had locally, which caused a thumbnail error. A small compatibility patch in the *test copy* fixed it. It does not affect the real file.
6. **Verify by reopening the output.** Screenshots show the interface, but only reopening the files and counting pages proves the split and merge are correct.

---

## 9. Known limitations

- Password-protected or damaged PDFs may fail, and the app shows an error message when they do.
- Very large files are limited by browser memory.
- Splitting creates several separate downloads rather than a single ZIP.
- Merging copies pages as they are. Bookmarks and form fields from the source files may not carry over.

---

## 10. Practice ideas

1. Add a **Download all as ZIP** button.
2. Add **page rotation** and **delete page** tools.
3. Add **remove every other page** or **extract odd/even pages** modes.
4. Let the Merger accept images (JPG, PNG) and convert them to pages.
5. Save the user's theme choice and last-used split mode.
6. Bundle the two libraries inline so the file is fully offline from the first load.

---

## 11. Summary

Today I built a privacy-friendly PDF utility that splits and merges documents entirely in the browser. The key ideas were pairing pdf.js (rendering) with pdf-lib (editing), turning every input into one validated plan, and testing the real output rather than trusting the interface. The result is a single HTML file that behaves like a polished commercial tool.
