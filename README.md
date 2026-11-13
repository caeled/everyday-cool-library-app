# Everyday Cool Library App

One of the very Everyday Cool things about the intenet is the vast number of free books availabile from a number of sources. This app puts six of those sources in one small Windows window: search them, download a book, and start reading, with your place saved for when you come back.

An [Everyday Cool](https://github.com/caeled/everyday-cool) subproject.

## Web edition

`web/index.html` is a hosted version of the same library: one static page, no server code, so it runs on any static host (GitHub Pages, a home server, Neocities). Search five of the six sources and read in the page.

Two differences from the desktop app, both imposed by browser rules rather than choice:

- **Wikibooks and Wikisource read natively in the page**, and so do EPUB files you open from your own device. Your library list and reading places are kept in the browser's local storage.
- **Project Gutenberg, Internet Archive and Open Library will not let other pages fetch their book files** (the browser's CORS rule), so there the web edition searches and then hands you to the source's own reader: Archive and Open Library results read in an embedded Archive reader panel, Gutenberg results open at gutenberg.org. **Standard Ebooks** is not in the web edition at all, for the same reason.

## Sources

Tick any combination at the top, type a title or author, hit Search.

- **Project Gutenberg** — the classic public-domain library (on by default).
- **Wikibooks** — open textbooks, built into EPUBs on the fly (on by default).
- **Internet Archive** — the big one, millions of texts (on by default). Only items archive.org offers as an unrestricted download are shown; its lending-only books are filtered out rather than failing at download time. Some Archive books come down as PDFs instead of EPUBs; the reader handles both.
- **Open Library** — archive.org's sister catalog. Different search, same open stock underneath; handy when an Archive search is noisy.
- **Standard Ebooks** — about a thousand public-domain titles, the best-produced EPUBs of the lot. (Their OPDS feed is members-only, so the app goes through the public website instead.)
- **Wikisource** — public-domain works, exported to EPUB. Pick a specific edition when search offers several (for example "The Time Machine (Heinemann text)"); a bare title page with no edition is usually just an index and exports thin.

Archive and Standard Ebooks checks make those searches slower than Gutenberg's. That is the libraries answering, not the app stuck.

## Reading

- **Double-click a result** to download the book and start reading. Downloaded books land in **My Library** (left side).
- **Open local file (EPUB, Word, PDF)...** (under the book list) opens a book you already have on disk. It is copied into your library, titled from the book's own metadata where it has any, and your place is saved for it like any other book. Opening the same file twice does not duplicate it.
  - Word means **.docx** (the modern format). Chapters split on Heading 1 / Title paragraphs when the document has them.
  - PDF means **text-based PDFs**: documents exported from Word, Google Docs, and similar extract cleanly, in page order, grouped five pages to a chapter. Scanned PDFs are images and have no text to read. Design-heavy PDFs (chart reports, brochures) extract with some spacing artifacts, though the text is all there.
- **Reading**: chapter list at the top of the reader, Prev / Next buttons, and A- / A+ for text size.
- **Your place is saved automatically** as you read (checked every few seconds and when you close the app). Reopen a book and you are back on the same chapter, at the same scroll position.
- **Remove selected book** deletes a downloaded book and its file.

## Run it

Needs Python 3 on the machine. Nothing else to install: the app uses only the Python standard library.

Double-click **LibraryApp.bat** (or run `python LibraryApp.py`).

## Build a Windows executable

```
python -m pip install pyinstaller
pyinstaller --noconfirm --windowed --icon LibraryApp.ico --name LibraryApp --add-data "banner.png;." --add-data "LibraryApp.ico;." LibraryApp.py
```

You get `dist\LibraryApp\LibraryApp.exe`. Books and reading places live in a `LibraryData` folder next to the exe, so they survive rebuilds.

## Where things live

Everything sits in a `LibraryData` folder next to the app:

- `LibraryData\Books\` — the book files
- `LibraryData\library.json` — your downloaded books
- `LibraryData\places.json` — reading position per book

Move or back up that folder and your library and places move with it.

## Icon and banner

`LibraryApp.ico` (a stack of books) is the app's window icon; it is also in the folder as `bookstack.png`. `banner.png` is a small version of the Everyday Cool Tech Bench banner, meant to run across the top of the window.

## Known issues

- **The Tech Bench banner does not appear in the PyInstaller-built executable**, even though it loads in a plain script run and is baked into the bundle with `--add-data`. Marked as a bug and parked; see the issue tracker. The app runs fine without it.

## Licenses

Same terms as the rest of Everyday Cool: code is MIT (see `LICENSE`); original writing is CC BY 4.0 (see `LICENSE-CONTENT.md`). Books you download keep their own sources' terms.
