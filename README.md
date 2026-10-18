# Local image converter

> Convert AVIF and WebP images to JPG, PNG, GIF or WebP, right in your browser. No server, no uploads.

![Version](https://img.shields.io/badge/version-1.2.1-blue)
![Manifest V3](https://img.shields.io/badge/Chrome-Manifest%20V3-green)
![Languages](https://img.shields.io/badge/languages-ES%20%7C%20EN%20%7C%20PT%20%7C%20FR%20%7C%20JA-orange)

**English** · [Español](README.es.md)

<!-- Add a screenshot here, e.g. ![Screenshot](docs/screenshot.png) -->

**Local image converter** is a Chrome extension that finds the images on any web page and converts them in batches, entirely on your computer. Pick the output format, choose a subfolder inside Downloads and get everything as a single ZIP, or file by file.

## Features

- **Detects images on the page**: `<img>`, `srcset`, `<picture>` sources, lazy-loaded images, links to image files and CSS backgrounds.
- **Several ways in**: click the extension icon, right-click an image (*Convert image…*), right-click the page (*Detect images on this page*), or drag and drop files into the converter.
- **Batch conversion** to **JPG, PNG, GIF or WebP**, with a quality slider for JPG and WebP.
- **Animated images**: WebP, AVIF and GIF animations can be converted to animated GIF, keeping frame timing and simple transparency.
- **No needless quality loss**: if the source already has the chosen format, the original file is saved untouched.
- **Filters and selection**: filter by type (AVIF, WebP, JPG, PNG, GIF) and minimum size; *Select visible*, *Deselect* and *Clear selected* buttons.
- **Download options**: subfolder inside Downloads, one ZIP or separate files, optional "Ask where to save", and a notification when the download is complete.
- **Remembers your settings** between sessions.
- **Multilingual**: follows your browser language (Spanish, English, Portuguese, French, Japanese; English as fallback).
- **Private by design**: everything is processed locally in your browser.

## Install

The extension is not on the Chrome Web Store yet, so install it from source:

1. Download the latest ZIP from the [Releases](../../releases) page (or use **Code → Download ZIP**) and unzip it.
2. Open `chrome://extensions` in Chrome.
3. Turn on **Developer mode** (top-right corner).
4. Click **Load unpacked** and select the folder that contains `manifest.json`.
5. Pin the extension from the puzzle-piece menu so its icon is always visible.

Requires a recent version of Chrome (102 or newer). Other Chromium-based browsers may work, but they have not been tested.

**Updating:** replace the folder with the new version and press the reload button on the extension card in `chrome://extensions`.

## How to use

1. Open a page with images and click the extension icon. A new tab opens with every image detected on that page.
2. Select the images you want (click a card, or use **Select visible**). Use the type chips and the minimum size to narrow the list.
3. Choose the **output format** and, if you like, a **subfolder** inside Downloads.
4. Press **Convert and download**. You will get a notification when the files are saved.

You can also drop image files from your computer onto the converter page.

## Output formats

| Output | Quality | Notes |
| --- | --- | --- |
| **PNG** | Lossless | Animated images keep only the first frame. |
| **JPG** | Slider (50–100 %) | Transparent areas are filled with the colour you choose. Animated images keep only the first frame. |
| **GIF** | 256 colours per frame | Keeps animation, frame timing and simple (on/off) transparency. |
| **WebP** | Slider (50–100 %) | Lossy even at 100 %. Animated images keep only the first frame. |

## Permissions

| Permission | Why it is needed |
| --- | --- |
| `activeTab`, `scripting` | Read the image list of the page you are on when you click the icon. |
| `<all_urls>` (host access) | Fetch the images from whatever site they come from so they can be converted locally. |
| `downloads` | Save the converted files, in a subfolder of Downloads if you set one. |
| `storage` | Remember your settings and pass the detected images to the converter tab. |
| `contextMenus` | The right-click entries. |
| `notifications` | Tell you when the download is complete. |

## Privacy

Nothing is uploaded anywhere. Images are fetched by your browser, converted locally and saved to your disk. The extension has no server, no analytics and no tracking.

## Known limitations

- Chrome only allows saving **inside your Downloads folder**. An absolute path such as `D:\Images` is reduced to its last folder name.
- Some sites block images from being fetched outside their own pages (hotlink protection), so a few images may fail to load.
- Chrome's internal pages (`chrome://…`, Web Store) cannot be scanned; use drag and drop there.
- GIF output is limited to 256 colours per frame by the format itself.

## Project structure

```
manifest.json        Extension manifest (Manifest V3)
background.js        Image detection, context menus
converter.html/.css  Converter page
converter.js         Decoding, encoding, downloads, i18n
_locales/            Translations (es, en, pt_BR, pt_PT, fr, ja)
lib/                 gifenc and fflate (bundled, no network needed)
icons/ images/       Icons and background image
```

## Adding a language

Copy `_locales/en` to a new folder named after the language code (for example `de`), translate the `message` values in `messages.json` and reload the extension.

## Credits

Created by **[Angel4RS](https://github.com/Angel4RS)**.

If you find it useful, you can support the project on **[Ko-fi](https://ko-fi.com/angel4kv1)**.

Built with [gifenc](https://github.com/mattdesl/gifenc) (GIF encoding) and [fflate](https://github.com/101arrowz/fflate) (ZIP creation).
