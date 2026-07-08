# Spatial Canvas — AR image collage

A single-file WebXR app for building image collages in your room. Runs in
Chrome on an ARCore-capable Android phone, served over HTTPS (GitHub Pages
works). All AI features run through [fal.ai](https://fal.ai) with your own API
key, stored only in the browser's localStorage.

`Index.html` and `spatial-canvas.html` are the same app (two entry points).

## Features

- **Generate** — drag a rectangle in AR to frame a plane, describe an image,
  and Nano Banana 2 fills it (aspect ratio matched to your frame).
- **Import** — bring in photos from your device; they're downscaled on-device
  and placed on the surface in front of you.
- **AI Edit** — rewrite any plane's image with a text instruction
  (image-to-image via `nano-banana-2/edit`).
- **Cutout** — remove an image's background (BiRefNet) for a frameless
  sticker floating in space.
- **Isolate** — Segment Anything (SAM 2): tap any element inside an image and
  it pops out as its own plane, cropped to the element and positioned right
  over where it was in the source image.
- **Duplicate** — clone a plane, including its image.
- **Scale & rotate** — pinch to scale, twist to rotate; or use the −/+
  buttons in the edit panel.

## Controls

| Gesture | Action |
| --- | --- |
| drag on empty space | frame a new image plane |
| tap a plane | pick it up (it follows the phone) |
| tap anywhere while carrying | place it |
| double-tap a plane | open the edit panel |
| two-finger pinch / twist | scale / rotate the held or selected plane |
| tap empty space | deselect / close panel |

## fal.ai endpoints used

| Purpose | Endpoint |
| --- | --- |
| text-to-image | `fal-ai/nano-banana-2` |
| image editing | `fal-ai/nano-banana-2/edit` |
| background removal | `fal-ai/birefnet/v2` |
| segmentation | `fal-ai/sam2/image` |

## Running

Serve over HTTPS and open on an ARCore phone in Chrome:

```
npx serve .        # or any static host — WebXR requires HTTPS (or localhost)
```

Paste your fal.ai key (`key_id:key_secret`) on the landing screen and Enter AR.
