# Pratiksha Enterprises — 3D pencil-sketch site

A scroll-driven WebGL site for the shop at Khade Bazaar, Belagavi. Everything on
screen is drawn by code — there is not a single image file in the project.

```
site/              one self-contained index.html — drag this folder onto any host
site-multifile/    the same build split into index.html + assets/ (normal hosting)
source/            the Vite + React project, if you ever want to change it
README.md          this file
```

---

## 1. Contact details

The phone number 99805 67888 is already wired in. If it ever changes, there is
one place to edit, `source/src/data.js`:

```js
phoneDisplay: '+91 99805 67888',   // shown on the page
phoneDial:    '+919980567888',     // the tel: link
whatsapp:     '919980567888',      // wa.me number, digits only, 91 first, no +
```

Every Call and WhatsApp button reads from that block. Rebuild after editing
(step 4).

**Still unconfirmed:** the opening time (9:30 am is an assumption; Justdial only
confirms the 8:30 pm close), Sunday being closed, and `since: '2017'` in the
hero, which is the GST registration date rather than the founding year.

## 2. Put it online

**Fastest — Netlify Drop.** Go to `app.netlify.com/drop` and drag the `site`
folder onto the page. Live in about ten seconds.

**Cloudflare Pages / GitHub Pages / Vercel.** Same — upload `site` or
`site-multifile`, both are plain static folders.

**Indian hosting (Hostinger, BigRock, GoDaddy).** Upload the *contents* of
`site-multifile` into `public_html/`. `index.html` must be at the top level.

**Domain.** A `.in` domain is roughly ₹500–900 a year. After you buy it, update
the two `https://www.pratikshaenterprises.in/` lines near the top of the HTML
(`canonical` and `og:url`), plus `sitemap.xml` and `robots.txt`.

## 3. Get the shop on Google

Separate from the website, and more important for walk-in customers.

1. **business.google.com**, signed in with a Gmail the shop owns.
2. Search "Pratiksha Enterprises Belagavi" first — if a listing already exists,
   **claim** it. Two listings for one shop hurt your ranking.
3. Primary category: **Print shop**. Secondaries: *Copy shop*, *Passport agent*,
   *Insurance agency*, *Stationery store*.
4. Drag the map pin to the actual shop door. In Khade Bazaar the auto-placed pin
   is usually in the wrong lane.
5. Verify — take the **video** option if offered. They ask for one unbroken clip
   of the signboard, the street, the counter and the equipment.
6. Add ten or more photos, then the service list, using the words people actually
   search: *passport, PAN card, PF withdrawal, voter ID, Aadhaar, e-Asti, xerox,
   Khade Bazaar*.
7. Ask regular customers for reviews. There are none yet; the first ten matter most.

Then submit the site at `search.google.com/search-console` → add property →
Sitemaps → `sitemap.xml`.

## 4. Changing the site

```bash
cd source
npm install
npm run dev            # local preview with hot reload
npm run build          # -> dist/  (multi-file)
SINGLE=1 npm run build # -> dist/index.html (one self-contained file)
```

**The content lives in one file: `src/data.js`.** Services, their bullet lists,
the "bring this" notes, the three steps, the address and hours are all there.
Add a fifteenth service by appending to the `SERVICES` array — give it a `kind`
that matches one of the motifs in `src/gl/textures.js`, and the card draws itself.

### How it is put together

| File | What it does |
|---|---|
| `src/gl/pencil.js` | The pencil shader. Shading is quantised into four cross-hatch passes whose line spacing is fixed in **screen** space, so strokes stay a constant thickness at any distance — that is what makes the geometry read as drawn rather than textured. Noise displaces each hatch coordinate so the lines wobble like a hand. |
| `src/gl/textures.js` | A pen, in Canvas2D. `stroke()` overshoots its endpoints and wanders off the straight line; `line()` draws twice at low opacity. Everything else — the 14 service cards, the signboard, the step sheets — is built from that pen. No image assets. |
| `src/gl/Card.jsx` | A sheet of paper. The curl is real geometry displaced on the CPU with normals recomputed, not a vertex-shader fake, so the hatching follows the curve. Hover runs through springs. |
| `src/gl/spring.js` | Springs with fixed 1/120 sub-steps, so motion is identical at 144fps and at 20fps, and exponential damping for the camera. |
| `src/gl/Rig.jsx` | GSAP ScrollTrigger scrubs one parameter; that parameter walks a Catmull-Rom path through the five zones; the result is damped again before it reaches the camera. |
| `src/gl/World.jsx` | The five zones laid out down the Y axis: documents adrift, the wall of 14 forms, the counter, the three steps, the shop board. |
| `src/ui/Overlay.jsx` | All the HTML — the Syne display type over the canvas, plus the flat "index" sheets below it. |

### Technical notes

- Pixel ratio is clamped to `Math.min(window.devicePixelRatio, 2)`.
- Pointer interaction uses r3f's raycaster (`onPointerMove` / `onPointerOver`),
  and every response is spring-driven — nothing snaps.
- `prefers-reduced-motion` disables the drift, the pointer lean and the intro move.
- No WebGL, or an old phone that refuses it? The page falls back to the HTML
  layer, which carries all the content on its own.
- Phones get fewer cards, a wider camera and the clusters repositioned below the
  copy rather than behind it.
- The whole thing is one visual world — warm paper, graphite, ink — so there is
  deliberately no dark mode. The hatching is lit for that cream ground.
- `LocalBusiness` structured data is in the `<head>`, so Google can read the
  address, hours, GSTIN and service list.
- No cookies, no tracking, no analytics, no backend.
