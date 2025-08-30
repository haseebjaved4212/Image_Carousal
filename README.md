## Image Carousel

A simple, responsive image carousel built with plain HTML, CSS (Tailwind + custom styles), and  JavaScript. This project shows how to build a clean image slider with navigation buttons and dot indicators. It is a single-page static project suitable for embedding into any static website or using as a learning reference.

### Project status

- Purpose: Learning / small UI component/demo
- Files: Minimal, no build steps required

## Files

- `index.html` — Main HTML file. Contains the layout and the custom styles used for the carousel container and controls. Tailwind CSS is included via CDN for convenience.
- `script.js` — All JavaScript logic lives here: image data, DOM wiring, navigation, dot creation, and optional autoplay code (commented out).

## Features

- Responsive image area with 3:2 aspect ratio.
- Next / Previous navigation buttons.
- Clickable dot indicators for direct navigation.
- Smooth fade transitions for images.
- Small, self-contained code base (no external build tools required).

## How it works (quick)

1. The image list is defined as an array of objects in `script.js` (`images` array). Each item has `src` and `alt`.
2. On page load the script builds the dot indicators (`createDots`) and shows the first image (`updateCarousel`).
3. Clicking next/previous buttons or a dot updates `currentImageIndex` and calls `updateCarousel()` which updates the main image and active dot.
4. Autoplay helpers exist but are commented out; you can enable them if you want automatic cycling.

## Quick start — open locally

Because this is a static project, you can open `index.html` directly in your browser. From PowerShell in the project folder run:

## Customization & common modifications

- To change the images: open `script.js` and edit the `images` array. Each entry is an object with `src` (URL or relative path) and `alt` text. Example:

```js
{
  src: './images/photo1.jpg',
  alt: 'A descriptive alt text',
}
```

- To enable autoplay: in `script.js` find the `startAutoPlay` and `pauseAutoPlay` functions (they are present but commented out). Uncomment them and call `startAutoPlay()` inside the `DOMContentLoaded` callback. You can adjust the interval inside `setInterval(showNextImage, 3000)`.

- To change styling: edit inline styles in `index.html` (under the `<style>` block) or remove the inline styles and use Tailwind utility classes where desired.

## Accessibility notes

- Each image has an `alt` attribute supplied from the `images` array. Provide meaningful alt text for screen readers and users with images disabled.
- Buttons are standard `<button>` elements and keyboard accessible. You can add `aria-label` attributes to `#prevBtn` and `#nextBtn` in the markup to improve clarity:

```html
<button id="prevBtn" class="nav-button" aria-label="Previous image">
  &lt;
</button>
<button id="nextBtn" class="nav-button" aria-label="Next image">&gt;</button>
```

- Consider adding focus outlines and skip links for a fully accessible integration depending on your audience.

## Edge cases and debugging

- Broken image URLs: the `alt` text will be shown if an image fails to load. For more graceful handling you can attach an `onerror` handler to `carouselImage` to replace the `src` with a fallback image.
- No images defined: if `images.length === 0` the current script will try to access `images[0]`. Guard this by checking the array length and hiding controls if empty.

Example guard in `script.js`:

```js
if (!images || images.length === 0) {
  carouselImage.alt = "No images available";
  prevBtn.disabled = true;
  nextBtn.disabled = true;
}
```

## Troubleshooting

- Images not appearing:

  - Make sure `script.js` is correctly linked and loads after the DOM (the project already uses `DOMContentLoaded`).
  - If using local image files, prefer running a local HTTP server rather than opening the file directly due to some browser CORS/security behaviors.

- Buttons or dots not working:
  - Open the browser console (F12) and check for JS errors. Ensure `script.js` path is correct and there are no typos in element IDs.

## Quality gates / suggested improvements

- Add a tiny unit test harness or static checks if integrating into a larger app.
- Add keyboard navigation support (Left/Right to change slides) and pause-on-focus for autoplay.
- Add lazy-loading for images (`loading="lazy"`) when using many images.

## License

This project is unlicensed by default. If you want to reuse it publicly, consider adding an open-source license such as MIT. Example `LICENSE` content can be added at the root.

---

If you'd like, I can also:

- add a small `images/` folder with sample local images,
- enable autoplay by default and add keyboard navigation, or
- add a short demo GIF or screenshots to the README.

Tell me which you'd prefer and I will make the changes.
