# Probo Design Assets

This repository contains all design assets for ProboLabs products, including logos, icons, and marketing materials.

## 📁 Repository Structure

```
probo-design/
├── logos/                    # Logo files in various formats and sizes
│   ├── archive/              # Archived logo versions
│   └── [logo files]
└── recorder-landing-page/    # Assets for the recorder landing page
    └── [video/gif files]
```

---

## 🎨 Logos

### Flower Logo (Icon)

The flower icon is available in multiple sizes and color variants.

#### Colorful Variants

| Size  | PNG                                 | SVG                          |
| ----- | ----------------------------------- | ---------------------------- |
| 16px  | ![16px](logos/logo-flower-16.png)   | [SVG](logos/logo-flower.svg) |
| 48px  | ![48px](logos/logo-flower-48.png)   | [SVG](logos/logo-flower.svg) |
| 128px | ![128px](logos/logo-flower-128.png) | [SVG](logos/logo-flower.svg) |
| 512px | ![512px](logos/logo-flower-512.png) | [SVG](logos/logo-flower.svg) |

#### Monochrome (Black) Variants

| Size  | PNG                                       |
| ----- | ----------------------------------------- |
| 16px  | ![16px](logos/logo-flower-16-black.png)   |
| 48px  | ![48px](logos/logo-flower-48-black.png)   |
| 128px | ![128px](logos/logo-flower-128-black.png) |
| 512px | ![512px](logos/logo-flower-512-black.png) |

**SVG Source:** [logo-flower.svg](logos/logo-flower.svg)

---

### Full Logo (Horizontal)

The full ProboLabs logo with text, available in multiple sizes.

#### PNG Variants

| Size           | Preview                             |
| -------------- | ----------------------------------- |
| 160px          | ![160px](logos/logo-full-160.png)   |
| 320px          | ![320px](logos/logo-full-320.png)   |
| 640px          | ![640px](logos/logo-full-640.png)   |
| 1280px         | ![1280px](logos/logo-full-1280.png) |
| 1920px         | ![1920px](logos/logo-full-1920.png) |
| Max (Original) | ![Max](logos/logo-full-max.png)     |

**SVG Source:** [logo-full.svg](logos/logo-full.svg)

---

## 🎬 Recorder Landing Page Assets

### Animated Demo

Animated GIF demonstrating how to start the Probo Recorder extension.

![Recorder Demo](recorder-landing-page/start-recorder-app.gif)

**Source Files:**

- [GIF](recorder-landing-page/start-recorder-app.gif) - Animated GIF (optimized for web)
- [MP4](recorder-landing-page/start-recorder-app.mp4) - Video format
- [MOV](recorder-landing-page/start-recorder-app.mov) - Original video file

---

## 📦 Asset Details

### Logo Files

#### Flower Logo

- **Formats:** PNG, SVG
- **Sizes:** 16px, 48px, 128px, 512px
- **Variants:** Colorful, Monochrome (black)
- **Usage:** Favicons, extension icons, app icons

#### Full Logo

- **Formats:** PNG, SVG
- **Sizes:** 160px, 320px, 640px, 1280px, 1920px, Max
- **Usage:** Headers, marketing materials, documentation

### Video Assets

#### Recorder Demo

- **Formats:** GIF, MP4, MOV
- **Purpose:** Onboarding demonstration
- **Usage:** Landing pages, documentation, tutorials

---

## 🎨 Color Palette

Based on the logo colors:

- **Primary Blue (Dark):** `#385F9C`
- **Primary Blue (Light):** `#58A7EB`
- **Accent Blue:** `#083981`

---

## 📝 Usage Guidelines

### Logo Usage

- Use colorful variants for light backgrounds
- Use monochrome variants for dark backgrounds or when color is not available
- Maintain minimum clear space around logos (recommended: 20% of logo height)
- Do not distort, rotate, or modify the logo proportions

### File Formats

- **SVG:** Use for scalable graphics (web, print at any size)
- **PNG:** Use for fixed-size raster graphics (favicons, app icons)
- **GIF:** Use for animated graphics (web only)
- **MP4/MOV:** Use for video content

---

## 📂 Archive

Historical and deprecated logo versions are stored in the [`logos/archive/`](logos/archive/) directory.

---

## 🛠️ Scripts & Tools

This section documents the scripts and commands used to process and generate the assets in this repository.

### Image Processing

#### Resizing PNG Images

**Using `sips` (macOS):**

```bash
# Resize a PNG to a specific size
sips -z 128 128 input.png --out output-128.png

# Resize maintaining aspect ratio (specify width)
sips -Z 128 input.png --out output-128.png
```

**Using Python PIL (Pillow):**

```python
from PIL import Image

# Resize image
img = Image.open('input.png')
resized = img.resize((128, 128), Image.Resampling.LANCZOS)
resized.save('output-128.png')
```

**Batch resize multiple sizes:**

```bash
# Example: Create multiple sizes from a source image
for size in 16 48 128 512; do
  sips -z $size $size logos/logo-flower-512.png --out logos/logo-flower-${size}.png
done
```

#### Converting to Monochrome (Black & White)

**Using Python PIL:**

```python
from PIL import Image, ImageOps

# Convert to grayscale
img = Image.open('input.png')
gray = ImageOps.grayscale(img)
gray.save('output-black.png')
```

**Using `sips` (macOS):**

```bash
# Convert to grayscale
sips -g input.png --out output-black.png
```

### Video Processing

#### Converting MOV to MP4

**Using `ffmpeg`:**

```bash
# Basic conversion
ffmpeg -i input.mov -c:v libx264 -c:a aac output.mp4

# With quality optimization
ffmpeg -i input.mov -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k output.mp4

# Trim video (first N seconds)
ffmpeg -i input.mov -t 6 -c:v libx264 -c:a aac output.mp4
```

**Parameters:**

- `-c:v libx264`: Use H.264 video codec
- `-preset medium`: Encoding speed/quality balance
- `-crf 23`: Constant Rate Factor (lower = higher quality, 18-28 range)
- `-c:a aac`: Use AAC audio codec
- `-b:a 128k`: Audio bitrate
- `-t 6`: Duration in seconds (for trimming)

#### Converting MP4 to Animated GIF

**Using `ffmpeg`:**

```bash
# Basic conversion
ffmpeg -i input.mp4 output.gif

# Optimized conversion (recommended)
ffmpeg -i input.mp4 \
  -vf "fps=10,scale=800:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" \
  -loop 0 \
  output.gif
```

**With size optimization:**

```bash
# Reduce frame rate and scale for smaller file size
ffmpeg -i input.mp4 \
  -vf "fps=8,scale=600:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=128[p];[s1][p]paletteuse=dither=bayer" \
  -loop 0 \
  output-optimized.gif
```

**Parameters:**

- `fps=10`: Frames per second (lower = smaller file)
- `scale=800:-1`: Resize width, maintain aspect ratio
- `flags=lanczos`: High-quality scaling algorithm
- `palettegen`: Generate optimal color palette
- `paletteuse`: Apply palette for better compression
- `max_colors=128`: Limit palette colors (smaller file)
- `dither=bayer`: Dithering algorithm for better quality
- `-loop 0`: Loop infinitely

**Complete workflow (MOV → MP4 → GIF):**

```bash
# Step 1: Convert MOV to MP4
ffmpeg -i recorder-landing-page/start-recorder-app.mov \
  -c:v libx264 -preset medium -crf 23 \
  -c:a aac -b:a 128k \
  recorder-landing-page/start-recorder-app.mp4

# Step 2: Convert MP4 to optimized GIF
ffmpeg -i recorder-landing-page/start-recorder-app.mp4 \
  -vf "fps=10,scale=800:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" \
  -loop 0 \
  recorder-landing-page/start-recorder-app.gif
```

### Prerequisites

- **macOS:** `sips` is built-in
- **ffmpeg:** Install via Homebrew: `brew install ffmpeg`
- **Python PIL:** Install via pip: `pip install Pillow`

---

## 🔄 Updates

This repository is actively maintained. For requests or updates to design assets, please open an issue or contact the design team.

---

## 📄 License

All design assets in this repository are proprietary to ProboLabs.
