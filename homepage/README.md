# Homepage latest updates

This directory controls the "Latest Updates" carousel on the MatrixOrigin
homepage. It is synced into the website by `mo-website-redesign` during the
normal blog sync step.

## Files

- `updates.json`: ordered carousel configuration and bilingual copy.
- `images/`: image assets used by the carousel.

## Update rules

- Keep at most five enabled items active at the same time.
- Use `variant: "split"` for a text-left, image-right card.
- Use `variant: "image"` for a full-image card with text overlay.
- Use `startsAt` and `endsAt` as `YYYY-MM-DD` when scheduling visibility.
- Put blog links under `/blog/<slug>`, internal pages under their route, and
  external links as full `https://` URLs.
- Keep image paths rooted at `/content/homepage/images/`.

