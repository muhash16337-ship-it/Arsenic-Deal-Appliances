# Cursor prompt: Arsenic Deal Appliances website

You are a senior front-end developer. Build a professional, modern, animated website for **Arsenic Deal Appliances**, an appliance and home-goods shop in Nairobi, Kenya. Customers browse the catalogue and place orders on WhatsApp. There is no online payment.

## Files already in this folder
- `products.json`: the full catalogue (47 products, 9 categories). Fields: `id`, `name`, `price` (number, or `null` when no price is set), `category`, `categorySlug`, `image` (relative path). It also holds `business`, `whatsapp` and `currency`.
- `images/<categorySlug>/<product>.jpg`: one photo per product, already sorted into category folders. Do not rename or move them. Two products (the Mika 8kg and 10kg washing machines) share one photo on purpose.

## Technical rules
- One `index.html` with all CSS and JavaScript inline. Vanilla HTML, CSS and JS only. No frameworks, no libraries, no build step.
- Copy the contents of `products.json` into a `const PRODUCTS` / `CATEGORIES` object inside the script, so the site works when opened from a file and on static hosting. Keep it as one clearly marked block so prices are easy to edit later.
- Use relative image paths so it works unchanged on GitHub and Cloudflare Pages. Use `loading="lazy"` and a proper `alt` on every image. Show a soft placeholder while images load.
- Mobile first. Most visitors are on phones. It must also look excellent on tablet and desktop.
- Never use `alert()`, `confirm()` or `prompt()`. Every dialog is a custom, styled modal.
- Also create `robots.txt` and `sitemap.xml` (use `https://example.com/` as a placeholder domain and tell me where to change it), plus SEO tags: title, meta description, Open Graph, and a favicon (an emoji or inline SVG).

## Design
- Dark charcoal / deep navy background with one bright accent colour (warm orange). Clean, confident, premium retail feel. Do not use the gold-and-black look of any other site.
- Smooth, tasteful animation: fade and slide-up on scroll, card hover lift with a soft glow, a subtle animated gradient background in the hero (not plain black anywhere), button press feedback, animated modal open and close. Respect `prefers-reduced-motion`.
- Use `cursor: pointer` and a hover effect on everything clickable.

## Page structure
1. **Header**: shop name, links to Catalogue, How to order and Contact, and a WhatsApp button. Sticky, with a blur backdrop.
2. **Hero**: strong headline about quality home appliances and furniture in Nairobi, a short line, and two buttons: "Browse the catalogue" and "Order on WhatsApp" (opens a general enquiry to the shop number).
3. **Category tiles**: one tile per category using the photo of the first product in it. Clicking a tile scrolls to the catalogue and applies that filter.
4. **Catalogue**: a search box, category filter chips (All plus the 9 categories) that stay usable on mobile (horizontal scroll), and a sort control (Default, Price low to high, Price high to low). Responsive product grid. Each card shows photo, name, category label and price formatted as `KSh 16,500`. If `price` is `null`, show "Ask for price" and make the card's button "Ask on WhatsApp", which opens an enquiry about that product and does not add it to the cart. Show a friendly empty state when search finds nothing.
5. **How to order**: 3 short steps (choose products, send your order on WhatsApp, we confirm delivery or pickup).
6. **Footer / Contact**: WhatsApp link, "Nairobi, Kenya", and a copyright line. Do not invent an address, opening hours, warranty terms or delivery fees.

## Product modal
Opens when a card is clicked: large photo, name, category, price, a quantity stepper, live line total, and two buttons: **Add to order** and **Order on WhatsApp**. "Order on WhatsApp" adds the product and goes to the order-details step below. Never skip that step.

## Cart and ordering
- The cart lives in memory only. It must be empty every time the site is opened or refreshed. Do not use localStorage or sessionStorage.
- When the cart has items, show a floating order bar at the bottom: "N items · KSh total · Review order". Add enough bottom padding to the page, and keep the bar from covering the hero buttons or the footer content.
- **Review order** opens a checkout modal listing the items, with quantity steppers and a remove button for each, and the running total. Below the list:
  - Name (required)
  - How would you like your order? Two big, well-styled option buttons: **Delivery** and **Pickup**
  - Delivery location (shown and required only when Delivery is chosen)
  - Special instructions (optional)
  - A primary button **Send order on WhatsApp**
- Every route to an order, including ordering a single product from its modal, goes through this same order-details step.
- Build the message and open `https://wa.me/254703789777?text=...` with the text URL-encoded. Format:
  ```
  Hello Arsenic Deal Appliances, I would like to order:

  1. Product name x2 - KSh 33,000
  2. ...

  Total: KSh 00,000
  Order type: Delivery
  Location: ...
  Name: ...
  Notes: ...
  ```
  Items with no price are never in the cart.
- Under the send button, add a fallback line "WhatsApp did not open? Tap here" (same link) and a "Copy order text" button that copies the message and shows a small "Copied" confirmation toast.
- After sending, show a short thank-you state inside the modal and clear the cart.
- Validate with inline error messages (not alerts). Trap focus in modals, close on Escape and on backdrop click, and make everything keyboard accessible.

## Content and data rules
- Use exactly the names, prices and categories in `products.json`. Do not invent specs, brands, discounts or warranty claims.
- The WhatsApp number is `0703789777`, so use `254703789777` in all `wa.me` links and show it as `0703789777` on screen.

## Deliverables
1. `index.html`, `robots.txt`, `sitemap.xml`.
2. A short `README.md` with: how to run it locally (for example `python3 -m http.server 8000`), how to edit a price or add a product, and how to deploy on Cloudflare Pages from a GitHub repo (no build command, output directory is the repo root).

Build the whole thing, then check it at 375px, 768px and 1280px widths and fix any layout problems before you finish.
