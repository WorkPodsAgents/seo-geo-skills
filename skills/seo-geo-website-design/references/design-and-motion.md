# Design and motion

How to make pages pleasant to read and still fast, with animation that never costs rankings.

## Contents

- Calm layout
- Colour and contrast
- Illustrations
- Mobile order
- Motion without hurting Core Web Vitals
- Reference code: deferred loader
- Reference code: fixed slot
- Budgets

## Calm layout

- Short sections with generous space between them. One idea per section and per visual.
- Avoid the template look: an eyebrow, a heading, a paragraph and a grid of rounded cards,
  repeated down the page. Use a few large panels, a table, a diagram or a single strong figure
  instead.
- Keep the reading measure at about 60 to 80 characters for long text.
- Use one typeface family with two or three weights. Load it with `font-display: swap` and
  preload the one file the hero needs.

## Colour and contrast

- One CTA colour for every primary action (header button, hero, closing section), and use it for
  nothing else, so the colour itself means "act here".
- Text links use a different colour from buttons.
- Every text and background pair passes WCAG 2 AA: at least 4.5:1 for normal text and 3:1 for
  large text (about 24 px regular or 18.5 px bold) and for icons and UI parts. Check small mono or
  muted labels on dark themes in particular; they fail most often.
- On a dark theme, brighten brand colours rather than reusing the light-theme values.

## Illustrations

- An illustration acts out what its section says: a mock search result showing the page cited, a
  form with a cursor, a short flow of steps.
- Labels, not sentences. A few words per element. If the illustration needs a paragraph to make
  sense, the section text is not doing its job.
- Any data shown in an illustration is either real and sourced or plainly marked "Example".
- Draw illustrations in HTML and CSS or inline SVG where you can, so the labels are real text,
  and mark purely decorative ones `aria-hidden="true"`.

## Mobile order

On narrow screens, stack each section as: label, heading, the first two sentences, then the
illustration. A phone reader should get the answer before the picture.

## Motion without hurting Core Web Vitals

Animation can make a page memorable, but it must never delay content, block input or move layout.
The rules:

1. **Static first.** The page is complete and readable with JavaScript off. No CSS rule hides
   content (`opacity: 0`, `visibility: hidden`, a blur) unless it is scoped under a class that a
   script adds, so a crawler without JavaScript still reads every word.
2. **Load late.** Import animation code only after the `load` event and then an idle callback,
   with a timeout fallback for browsers that lack `requestIdleCallback`.
3. **Respect the reader.** Skip animation entirely when `prefers-reduced-motion: reduce` matches
   or when the browser reports data saver (`navigator.connection.saveData`, Chromium only).
4. **Reserve space.** Every animated element draws into a slot whose width and height are set in
   CSS before the script runs, so CLS stays at 0.
5. **Stay off the main thread.** Animate `transform` and `opacity`, use `requestAnimationFrame`,
   pause when the tab is hidden or the element is off screen (`IntersectionObserver`).
6. **Finished without motion.** The slot already holds the icon's end state as inline SVG in the
   HTML. Without JavaScript, with reduced motion or with data saver, the reader sees the finished
   icon, never an empty box. Motion only animates its way to that state.
7. **One source of colour.** Scripts read colours from the CSS custom properties
   (`getComputedStyle(document.documentElement).getPropertyValue('--ink')`), so themes and
   contrast fixes live in one place.
8. **Words stay in HTML.** Labels that carry meaning ("6 pm cutoff", "Saturday pickup") are HTML
   text beside or inside the SVG, not text painted on a canvas, which crawlers and screen readers
   cannot read.
9. **Purpose.** Motion acts out the section's idea and stops. Nothing loops beside text someone is
   reading.

## Reference code: deferred loader

A small inline module at the end of `<body>`. It costs a few hundred bytes up front; the animation
code downloads only when the page is idle.

```html
<script type="module">
  // Start optional motion only after the page has loaded and the browser is idle.
  const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches
  const saveData = navigator.connection && navigator.connection.saveData
  if (!reduce && !saveData) {
    const start = () => {
      document.documentElement.classList.add('js-motion')
      import('./motion.js').catch(() => {
        document.documentElement.classList.remove('js-motion')
      })
    }
    const whenIdle = () =>
      'requestIdleCallback' in window
        ? requestIdleCallback(start, { timeout: 2500 })
        : setTimeout(start, 1200)
    if (document.readyState === 'complete') whenIdle()
    else addEventListener('load', whenIdle, { once: true })
  }
</script>
```

Any CSS that prepares an element for animation lives under `.js-motion`, so without the script
nothing is hidden. Never hide content that is already on screen when the class is added; the
reader would see it flash away and back. Give the reveal class only to elements below the fold
(the script can skip any element whose top is inside the viewport), or animate from visible:

```css
.js-motion .reveal { opacity: 0; transform: translateY(8px); }
.js-motion .reveal.is-in { opacity: 1; transform: none; transition: opacity .4s, transform .4s; }
@media (prefers-reduced-motion: reduce) {
  .js-motion .reveal { opacity: 1; transform: none; transition: none; }
}
```

## Reference code: fixed slot

A slot reserves its box in CSS, so whatever the script draws later cannot push text around. It
starts with the finished icon as inline SVG; the script hides that SVG only once its canvas is
ready. In this example the slot is a small icon above the label, so it sits first. A larger
illustration goes after the label, heading and opening text, so phones keep the mobile order.

```html
<section aria-labelledby="delivery">
  <div class="motion-slot" aria-hidden="true">
    <svg viewBox="0 0 200 56" width="200" height="56">
      <circle cx="20" cy="28" r="8" fill="var(--ink)" />
      <path d="M32 28h120" stroke="var(--muted)" stroke-width="2" />
      <circle cx="160" cy="28" r="8" fill="var(--accent)" />
    </svg>
  </div>
  <p class="label">Delivery</p>
  <h2 id="delivery">Bread delivered before 7 am</h2>
  <p>Orders placed by 9 pm arrive the next morning before 7 am...</p>
</section>
```

```css
.motion-slot { width: 200px; height: 56px; margin-bottom: 12px; contain: strict; }
.motion-slot svg, .motion-slot canvas { display: block; width: 100%; height: 100%; }
.motion-slot.is-animated svg { display: none; }
```

```js
// motion.js: draw into each slot only when it scrolls into view.
const slots = document.querySelectorAll('.motion-slot')
const seen = new IntersectionObserver((entries) => {
  for (const entry of entries) {
    if (!entry.isIntersecting) continue
    seen.unobserve(entry.target)
    const canvas = document.createElement('canvas')
    const ratio = Math.min(devicePixelRatio || 1, 2)
    canvas.width = entry.target.clientWidth * ratio
    canvas.height = entry.target.clientHeight * ratio
    entry.target.append(canvas)
    entry.target.classList.add('is-animated')
    drawIcon(canvas.getContext('2d'), ratio, entry.target.closest('section').id)
  }
}, { rootMargin: '0px 0px -20% 0px' })
slots.forEach((slot) => seen.observe(slot))

const css = getComputedStyle(document.documentElement)
const colour = (name) => css.getPropertyValue(name).trim()

function drawIcon(ctx, ratio, name) {
  ctx.scale(ratio, ratio)
  ctx.fillStyle = colour('--ink')
  // Animate toward the same shape as the SVG end state with requestAnimationFrame,
  // and stop once it has formed.
}
```

## Budgets

Set budgets before you design, and check them on every build:

| Budget | Default target |
|---|---|
| JavaScript loaded up front (gzip) | about 5 KB on marketing pages |
| Deferred JavaScript (gzip) | a number you measure and agree, checked in CI |
| Lighthouse mobile LCP | 2.0 s or less |
| Lighthouse mobile TBT | 100 ms or less |
| Lighthouse mobile CLS | 0.05 or less |

These targets are stricter than Google's field thresholds for "good" Core Web Vitals (LCP 2.5 s,
INP 200 ms, CLS 0.1 at the 75th percentile). Lab runs on a developer machine flatter real phones,
so the margin keeps field data in the green.
