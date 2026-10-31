# CBZ to EPUB

A lightweight Python tool to convert CBZ comic archives into EPUB files optimized for basic Kindle devices.

## Overview

This project reads comic pages from a `.cbz` archive, converts the images to a Kindle-friendly format, and builds an EPUB document with the right page structure for reading on eReaders.

The script preserves image quality by avoiding unnecessary vertical resizing and splitting extremely tall pages into smaller Kindle-sized segments when needed.

## Features

- Converts `.cbz` archives into `.epub`
- Optimizes output for Kindle-sized screens
- Splits tall pages into multiple segments without excessive vertical distortion
- Supports optional external cover images
- Handles a single file or an entire folder of CBZ files
- Produces a clean EPUB with proper page ordering and metadata

## Requirements

- Python 3.8+
- Pillow

Install dependencies:

```bash
python3 -m pip install -r requirements.txt
```

## Installation

```bash
git clone https://github.com/CrisGP14/cbz_to_epub.git
cd cbz_to_epub
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

Convert a single file:

```bash
python3 convert.py my-comic.cbz
```

Use a custom output file:

```bash
python3 convert.py my-comic.cbz -o my-comic.epub
```

Add a cover image:

```bash
python3 convert.py my-comic.cbz --cover cover.jpg
```

Convert all CBZ files in a directory:

```bash
python3 convert.py ./my-folder/
```

## Output

By default, the script creates an EPUB file with the same base name as the input CBZ archive.

Example:

```bash
python3 convert.py SL112-123.cbz --cover portada.jpg
```

This creates:

```bash
SL112-123.epub
```

And includes the provided cover image as the EPUB cover metadata.

## Notes

- Target resolution is `600x800` for basic Kindle devices.
- Supported image formats inside CBZ files include `.jpg`, `.jpeg`, `.png`, `.webp`, `.gif`, and `.bmp`.
- The script keeps the page width compatible with Kindle while avoiding vertical stretching.
- If a cover file is supplied, it is placed as the first page and marked as the EPUB cover.

## Project structure

```text
cbz_to_epub/
├── convert.py
├── README.md
├── requirements.txt
├── .gitignore
└── cbz_to_kindle/   # included legacy/reference folder
```

## Why this tool

This project is useful when you want to read manga, manhwa, or comics in a simple EPUB format compatible with Kindle or similar devices without relying on heavy external tools.

## License

This project does not currently declare an explicit license in the repository, so please review usage terms according to your project or personal requirements.
