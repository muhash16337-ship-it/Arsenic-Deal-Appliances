# Arsenic Deal Appliances

A single-page, static product catalogue. Orders are sent to the shop on WhatsApp; this site does not take online payments.

## Run locally

Open `index.html` directly in a browser, or serve the project folder:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Edit catalogue data

Open `index.html` and find the clearly marked **EDITABLE CATALOGUE DATA** block in the inline script. Edit a product's `price` there to update its displayed price. To add a product, add an object with a unique `id`, its exact `name`, numeric `price` (or `null` when the price is not set), `category`, matching `categorySlug`, and its relative `image` path. Add any new category to `CATEGORIES` and place its images in the matching `images/<categorySlug>/` folder. The site catalogue is embedded in the HTML so it works from a local file and static hosting without loading `products.json`.

## Deploy on Cloudflare Pages

1. Push this folder and its `images/` directory to a GitHub repository.
2. In Cloudflare Pages, create a project and connect the repository.
3. Choose **None** for the framework preset, leave the build command empty, and set the output directory to `/` (the repository root).
4. Deploy.

Before launch, replace `https://example.com/` with your real site URL in `sitemap.xml`, `robots.txt`, and the canonical/Open Graph URL fields near the top of `index.html`.
