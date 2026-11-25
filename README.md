# CBZ to EPUB

A lightweight Python tool that converts CBZ comics, especially long-strip manhwa, into EPUB files sized for basic Kindle devices.

Long vertical pages are hard to read on an e-reader because the whole strip is squeezed onto one screen. This script fits each page to the Kindle's width and cuts tall ones into screen-sized segments.

## Features

- Converts a single `.cbz`, several files, or a whole folder
- Splits tall pages into Kindle-sized segments without distorting them
- Never enlarges images
- Orders pages naturally (`2.jpg` comes before `10.jpg`)
- Adds an optional cover as the first page and as the EPUB cover
- Skips unreadable images instead of stopping

## Requirements

- Python 3.10 or newer
- [Pillow](https://python-pillow.org/)

## Installation

```bash
git clone https://github.com/CrisGP14/CBZ-to-EPUB.git
cd CBZ-to-EPUB
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install Pillow
```

> [!NOTE]
> `requirements.txt` does not currently list Pillow, so install it directly as shown above.

## Usage

```bash
python3 convert.py my-comic.cbz
```

This creates `my-comic.epub` next to the original file.

| Argument | Description |
|---|---|
| `input` | One or more `.cbz` files, or folders containing them |
| `-o`, `--output PATH` | Output path; ignored when converting more than one file |
| `--cover IMAGE` | Cover image, applied to every converted file |

### Examples

```bash
# Choose the output file
python3 convert.py my-comic.cbz -o output.epub

# Add a cover
python3 convert.py my-comic.cbz --cover cover.jpg

# Convert every CBZ in a folder
python3 convert.py ./my-folder/
```

Transfer the result to your Kindle with [Send to Kindle](https://www.amazon.com/sendtokindle). The program's console messages are in Spanish.

## How it works

1. Reads the images from the archive in natural order. Supported formats: `.jpg`, `.jpeg`, `.png`, `.webp`, `.gif` and `.bmp`.
2. Scales pages wider than 600 px down to 600 px, keeping the aspect ratio.
3. Splits pages taller than 960 px (1.2 × the screen height) into segments of up to 800 px.
4. Encodes every page as JPEG at quality 90 and builds the EPUB, using the file name as the title.

A cover image is scaled to fit 600×800 px, with black bars if needed.

## Limitations

- The target resolution is fixed at 600×800 px (the `KINDLE_W` and `KINDLE_H` constants in `convert.py`).
- Pages are cut at fixed heights, so a cut can fall in the middle of a panel or speech bubble.
- The EPUB language is always set to Spanish (`es`).
- File names containing `&` or `<` produce an invalid EPUB; rename them first.

## Project structure

```text
CBZ-to-EPUB/
├── convert.py         # converter
├── requirements.txt   # see the installation note
├── .gitignore
└── README.md
```
