# RGAA v4.1.2 – Theme 1: Images – Detailed Criteria

## Criterion 1.1 – Informative images have text alternatives

Elements to check: `<img>`, `[role="img"]`, `<area>` with href, `<input type="image">`, `<svg>`, `<object type="image/…">`, `<embed type="image/…">`, `<canvas>`

For each element carrying information:
- `<img>` / `[role="img"]`: must have alt, title, aria-label, or aria-labelledby
- `<area>` with href: must have alt, title, aria-label, or aria-labelledby
- `<input type="image">`: must have alt, title, aria-label, or aria-labelledby
- `<svg>`: must have `role="img"` AND a text alternative (aria-label, aria-labelledby, or `<title>`)
- `<object type="image/…">`: must have (alt text + role="img") OR adjacent link to alternative OR replacement mechanism
- `<embed type="image/…">`: same as object
- `<canvas>`: must have (alt text + role="img") OR fallback content between tags OR adjacent link OR replacement mechanism
- Server-side image maps: each clickable zone must be doubled with a device-independent link

WCAG: 9.1.1.1 Non-text Content (A)

## Criterion 1.2 – Decorative images hidden from assistive tech

- `<img>` decorative: alt="" with no other text alternative attributes, OR aria-hidden="true" / role="presentation"
- `<area>` without href decorative: alt="" with no text alternative, OR aria-hidden="true" / role="presentation"
- `<object type="image/…">` decorative: aria-hidden="true", no alt text, no fallback text
- `<svg>` decorative: aria-hidden="true", no alt text on svg or children, no `<title>`/`<desc>`, no title attribute
- `<canvas>` decorative: aria-hidden="true", no alt text, no fallback content
- `<embed type="image/…">` decorative: aria-hidden="true", no alt text

WCAG: 9.1.1.1 (A), 9.4.1.2 (A)

## Criterion 1.3 – Text alternatives are relevant

For every informative image with an alt text, verify:
- alt is not a filename (e.g. "IMG_1234.jpg")
- alt is not generic ("image", "photo", "icon", "picture")
- alt meaningfully describes the information conveyed
- alt is concise (criterion 1.3.9)
- For SVG: `<title>` content is relevant
- For canvas/object/embed: fallback content is relevant

WCAG: 9.1.1.1 (A), 9.4.1.2 (A)

Exception: CAPTCHAs and test images (handled by criterion 1.4)

## Criterion 1.4 – CAPTCHA/test image alternatives identify nature and function

If image is a CAPTCHA or test image, the alternative must identify it as such (e.g. "Security code CAPTCHA") rather than describing the CAPTCHA content.

WCAG: 9.1.1.1 (A)

## Criterion 1.5 – CAPTCHAs have alternative access

If a graphical CAPTCHA exists, at least one of:
- Another non-graphical CAPTCHA form exists
- Another solution to access the secured functionality exists

WCAG: 9.1.1.1 (A)

## Criterion 1.6 – Complex images have detailed descriptions

Images needing detailed descriptions (charts, infographics, complex diagrams) must have:
- A longdesc attribute with URL to description (for `<img>`)
- An alt text referencing an adjacent detailed description
- An adjacent link/button to the detailed description
- aria-describedby pointing to the description
- For SVG: aria-label + adjacent description, aria-labelledby, aria-describedby, or adjacent link
- For canvas: similar mechanisms or fallback content between tags

WCAG: 9.1.1.1 (A)

## Criterion 1.7 – Detailed descriptions are relevant

Verify that existing detailed descriptions accurately and completely describe the image content.

WCAG: 9.1.1.1 (A)

## Criterion 1.8 – Text images replaced by styled text when possible

Images containing only text should be replaced with CSS-styled HTML text.

Exceptions (not applicable):
- Text is part of a logo or trademark
- CAPTCHA or test image
- Image where graphical accuracy is essential to information

WCAG: 9.1.4.5 Images of Text (AA)

## Criterion 1.9 – Captions correctly linked to images

Images with captions must use:
- `<figure>` containing both the image and `<figcaption>`
- `<figure>` has `role="figure"` or `role="group"`
- `<figure>` has `aria-label` matching the figcaption content
- Caption is inside `<figcaption>`

Applies to: img, input[type="image"], [role="img"], object, embed, svg, canvas

WCAG: 9.1.1.1 (A), 9.4.1.2 (A)
