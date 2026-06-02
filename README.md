# ImageMagick Image Optimizer (Python)

Resize and optimize images in a folder with ImageMagick. Output files keep the same format (or convert) and are saved alongside the originals or to a separate output directory.

## Requirements
- Python 3.8+
- ImageMagick installed and `magick` available in PATH

## Usage

Basic resize:

```bash
python optimizer.py --input "C:\path\to\images" --suffix "_resized" --max-width 1920 --max-height 1080
```

Only width (height scales proportionally):

```bash
python optimizer.py --input "C:\path\to\images" --suffix "_resized" --max-width 1920
```

Only height (width scales proportionally):

```bash
python optimizer.py --input "C:\path\to\images" --suffix "_resized" --max-height 1080
```

Resize with compression and metadata stripping:

```bash
python optimizer.py --input "images" --suffix "_opt" --max-width 1920 --quality 85 --strip
```

Resize and sharpen after downscaling:

```bash
python optimizer.py --input "images" --suffix "_opt" --max-width 1200 --sharpen "0x1"
```

Convert to WebP and write to a separate output folder:

```bash
python optimizer.py --input "images" --suffix "_opt" --max-width 1920 --format webp --output-dir "optimized"
```

Process subfolders recursively:

```bash
python optimizer.py --input "images" --suffix "_opt" --max-width 1920 --recursive --output-dir "optimized"
```

## Options

| Flag | Description |
|------|-------------|
| `--input`, `-i` | Input folder (required) |
| `--suffix` | Suffix added before extension (required) |
| `--max-width` | Maximum width in pixels |
| `--max-height` | Maximum height in pixels |
| `--recursive` | Process subfolders recursively |
| `--extensions` | Comma-separated list of extensions (default: jpg, jpeg, png, webp, avif, tif, tiff, bmp, gif) |
| `--magick-path` | Path to `magick` executable if not in PATH |
| `--overwrite` | Overwrite existing output files |
| `--dry-run` | Print ImageMagick commands without running them |
| `--quality` | JPEG/WebP compression quality (1-100) |
| `--strip` | Strip metadata (EXIF, ICC profiles, etc.) |
| `--sharpen` | Sharpen after resize (ImageMagick sharpen argument, e.g. `0x1`) |
| `--output-dir` | Write output files to a separate directory (preserves subfolder structure) |
| `--format` | Convert images to a different format (e.g. `webp`, `jpg`, `png`) |
| `--version` | Print version and exit |

## Notes
- Images are resized proportionally to fit within the max width/height.
- Files whose names already end with the suffix are skipped to avoid reprocessing.
- When using `--output-dir`, subfolder structure is preserved when `--recursive` is enabled.
- When using `--format`, the extension changes but the output path is otherwise the same.

## License
This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Development & Tests
Install dev dependencies and run tests:

```bash
python -m pip install -r requirements-dev.txt
pytest
```
