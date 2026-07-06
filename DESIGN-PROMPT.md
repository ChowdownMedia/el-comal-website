# Claude Design prompt - El Comal Mexican Restaurant

Design a complete, production website theme for **El Comal, Authentic Mexican Restaurant**, a
single-location family restaurant in Mt. Juliet, Tennessee. I need three fully designed pages that
together define the whole system so nothing else has to be designed later:

1. **Home page** (this is also the location page, one location)
2. **Menu page**
3. **VIP club page** ("Become a VIP")

Deliver them as self-contained static HTML with one shared inline design language (no external CSS/JS
frameworks, no build step). I will wire in real content, forms, and assets myself.

## Brand identity (use the REAL brand, do not invent a new one)
A "comal" is the flat griddle Mexican cooks use to warm handmade tortillas and roast chiles, so El
Comal's identity is the **hearth**: fire, masa, and tradition. The real logo is a **hand-drawn,
woodcut/linocut wordmark**, "El Comal" in warm ember tones that shade from deep maroon into red,
orange and gold, with "Authentic Mexican Restaurant" beneath in a small rustic serif.

Translate that into the site:
- **Palette:** deep chile-red / maroon as the primary, fire orange and golden/masa yellow as the warm
  accents, a warm masa-cream / toasted off-white as the base, and a charred near-black brown for ink.
  Add one fresh accent (tomatillo / cilantro green) so the food reads bright against the warm neutrals.
  The mood is warm, rustic and hearth-lit, NOT beachy, NOT corporate, NOT cool-toned.
- **Motifs (sparing, hand-drawn, as inline SVG):** the round comal griddle as a disc/medallion, simple
  flame or ember lines, a stack of handmade tortillas, roasted chiles, a subtle masa/paper grain. Echo
  the logo's woodcut, slightly-imperfect line quality. Do not use the photographic logo as a texture.
- **Type:** a characterful display face for headings with a warm, slightly rustic or hand-built feel
  (echoing the woodcut lettering) paired with a clean, highly legible sans for body. Self-host both as
  woff2 (see performance). Use the FEWEST display weights that still look right.
- **Tone:** a warm, welcoming, family-run cantina where everything is made by hand from scratch.

## Pages and sections

### Home
- **Text-forward hero** (the large brand headline is the biggest text and the LCP element; do NOT make a
  full-bleed background image the LCP). A warm, hearth-lit backdrop (embers/masa-cream gradient, subtle
  hand-drawn flame or comal motif) is fine as long as it is lightweight and the headline is the LCP.
  Headline, one-line subhead, two CTAs: "Order Online" and "Join the VIP Club". A small lazy-loaded dish
  accent image is fine.
- **Welcome / story** short copy about the comal, handmade tortillas, everything from scratch. Include a
  round brand medallion (I will drop the real logo in) and a small overlapping dish photo.
- **Featured dishes** grid of 6 dish cards (image + name + short description). I will drop in real photos.
- **Gallery** a photo gallery of ~8 images in a responsive grid (2-col mobile up to 4-col desktop),
  every cell a fixed square (`aspect-ratio:1`, `object-fit:cover`), all lazy-loaded with width/height set
  so there is zero layout shift. Clicking a photo opens a **lightbox** (one reused overlay, prev/next +
  close, keyboard support: Esc closes, arrow keys navigate, background click closes). Style it entirely
  from the design tokens so it is reusable across our other sites.
- **Reviews** a horizontal, swipeable card scroller (stars + quote + name). It must NOT cause page-level
  horizontal scroll on mobile (contain it inside its own scroller).
- **Visit us** address, phone, hours, and a **click/scroll-to-load map placeholder** (a styled facade
  that upgrades to a Google Maps embed; keep Google Maps off the initial critical path).
- **Contact** a "Get in Touch" form (First name, Last name, Email, Phone, Message) with designed
  default / loading / success / error states.
- Sticky header (logo left, nav, an "Order Online" CTA, mobile hamburger + menu). Footer with hours,
  address, social links, and a "Powered by Chowdown" line.

### Menu
- Full-menu layout for a LARGE menu (20-30 categories, 150+ items), real dense content.
- A **sticky category filter bar** (horizontally scrollable pills) that shows one category at a time plus
  an "All" view. Clean two/three-column masonry of items (name, price, description; optional dish photo).
  Readable and fast with hundreds of items. Include an allergen/footnote style.

### VIP club
- Warm, celebratory hero ("Join the El Comal VIP Club"), 3 perks with hand-drawn SVG icons, and a signup
  form (First name, Last name, Phone, Email, Date of birth) with a "Get My Pass" button and a success
  state that reveals "Add to Apple Wallet / Google Wallet" buttons. A membership-pass card is a nice touch.

## Hard requirements (build these in, they are non-negotiable)
- **Mobile-first.** Flawless at 390px wide with ZERO horizontal page scroll. Any wide element (menu
  filter, review scroller, gallery, tables) scrolls inside its own container, never the page body.
- **Performance (target Lighthouse mobile 95-100).** Self-host fonts as woff2 with `font-display:swap`
  and NO preload; the hero headline text is the LCP, not an image or map. Lazy-load all below-the-fold
  images, the gallery, and the map. Keep JS minimal and inline. No `scroll-snap-type:x mandatory` on the
  hero, and no hero image without responsive srcset.
- **Accessibility (target 100).** Single h1 then h2/h3 in order, a `<main>` landmark, all color pairs
  pass AA contrast (be careful with orange/gold on light backgrounds, and with light text on the warm
  hero), labeled form fields, visible focus states, alt text. Specific rules that cost points: any
  `<div>` carrying an `aria-label` (e.g. a star rating) needs a `role` such as `role="img"`; if a link or
  button has BOTH visible text and an `aria-label`, the label must contain that visible text (or omit the
  label); the skip link target must exist.
- **No em dashes or en dashes anywhere** in copy or code (use commas/periods; restructure instead).
- **No emojis anywhere.** Inline SVG icons only.
- Clean semantic HTML with the design as one inline `<style>` per page, using CSS custom properties
  (design tokens) for palette/spacing/type so everything is centralized and reusable. Use consistent
  shared class names across all three pages (shared header, footer, buttons, cards, forms, gallery).

## What to hand back
Three HTML files (home, menu, VIP) plus the woff2 fonts (or the exact Google Fonts families + weights you
used so I can self-host them). Self-contained and copy-paste runnable.
