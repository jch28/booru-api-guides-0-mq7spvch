---
title: "Batch Watermark Images for Booru Sites — Automated Guide"
description: "Learn how to batch watermark images for booru sites using Python and Pillow. Includes RGBA overlay, EXIF preservation, and R2 storage automation."
---

# Batch Watermark Images for Booru Sites

Watermarking images before uploading to booru sites is essential for protecting your content and driving traffic back to your source. This guide shows how to automate bulk watermarking using open-source tools.

## Why Watermark?

Watermarks ensure that when your images are shared across booru platforms, viewers can always find the original source. A subtle, semi-transparent watermark with your domain name provides attribution without degrading the viewing experience.

## Automation Setup

Using Python with Pillow, you can process hundreds of images per minute:

```python
from PIL import Image, ImageDraw, ImageFont

def apply_watermark(image_path, domain="rule34.ink"):
    img = Image.open(image_path)
    overlay = Image.new('RGBA', img.size, (0, 0, 0, 0))
    draw = ImageDraw.Draw(overlay)
    # Semi-transparent text overlay
    draw.text((10, 10), domain, fill=(255, 255, 255, 60))
    return Image.alpha_composite(img.convert('RGBA'), overlay).convert('RGB')
```

## Storage

Upload watermarked images to R2-compatible storage for fast global delivery. The [rule34.ink](https://rule34.ink) platform provides API access for automated upload pipelines.

## Anti-Detection

Randomize watermark position, opacity (0.15-0.35), and rotation (-15 to +15 degrees) per image to avoid pattern detection. JPEG quality variance (82-92) further diversifies file hashes.

*Part of the [rule34.ink](https://rule34.ink) open-source tool ecosystem.*
