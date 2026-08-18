# DECISIONS.md

## 1. Why this approach?

**Invented product (Meridian, API observability) over redesigning an existing one.**

The obvious alternative was to redesign a well-known product's home page (e.g., Vercel, Linear).
I rejected that because: (a) it invites lazy "make it look like Figma" thinking, (b) the constraint
"no fabricated testimonials / fake user counts" is *easier to honour honestly* for an early-stage
product — a beta badge and "limited seats" copy is accurate by design, not a workaround.

Meridian's pitch ("know your APIs before your users do") is specific enough to write real,
defensible copy and show a real product interaction without inventing social proof.

**Single-file HTML/CSS/JS over a framework.**

Vanilla HTML ships immediately to any static host, has zero build-step failure modes, and is
fully readable line-by-line in a follow-up call — which the brief explicitly requires. Inter +
JetBrains Mono are loaded from Google Fonts; everything else is written by hand.

---

## 2. Trade-off made under the time limit

**I built a mock dashboard instead of an animated live-data integration.**

The live log stream and stat jitter are simulated in JavaScript. With a real week, I'd wire this to
a public WebSocket demo endpoint (or a small server-sent events server on Render) so the data is
genuinely live. The interaction pattern — animated sparkline draw on scroll, log stream cycling,
P95/req jitter every 3 s — demonstrates the exact UX without the infra dependency. Under time
pressure, fake-but-honest-looking data beats a broken real connection.

---

## 3. AI tool usage

**Used:** Claude Sonnet to scaffold the overall CSS design token system and the IntersectionObserver
scroll-reveal pattern. Prompted for: "dark-only design tokens, accessible nav with skip-link, SVG
sparkline that draws on scroll, live log stream simulation."

**Personally verified and changed:**

- Rewrote all copy from scratch — every headline, sub-head, feature description, and CTA. The
  AI output used vague marketing language ("powerful", "seamless"); replaced with specific,
  honest claims ("P50, P95, P99 latency … updated on a 5-second heartbeat").
- Replaced fabricated stat cards ("10,000 teams trust us") with plausible in-product metrics that
  a real dashboard would show (latency, error rate, req/min, Apdex).
- Added keyboard accessibility throughout: `aria-label`, `role`, `aria-live` on the log stream,
  `aria-selected` on tabs, Escape key closing the Easter egg overlay.
- Manually tuned every `transition-delay`, cubic-bezier curve, and responsive breakpoint. The AI
  output had too many simultaneous animations; removed all but three intentional ones.
- Added the Konami code Easter egg entirely without AI — it's 12 lines of JS and felt right.
