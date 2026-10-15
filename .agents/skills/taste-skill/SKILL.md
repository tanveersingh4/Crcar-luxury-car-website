---
name: taste-skill
description: Anti-slop frontend design skill for landing pages, portfolios, and redesigns. Gives the AI "good taste" - stops it from generating boring, generic, templated UIs. Infers design direction from the brief, sets variance/motion/density dials, enforces a pre-flight quality checklist. Use when building or redesigning any marketing/landing/portfolio page.
---

> Landing pages, portfolios, and redesigns. Not dashboards, not data tables, not multi-step product UI.
> Every rule below is **contextual**. None of it fires automatically. First read the brief, then pull only what fits.

---

## 0. READ THE BRIEF FIRST

Before touching code or tweaking dials, **infer what the user actually wants**. Most LLM design output is bad because the model jumps to a default aesthetic instead of reading the room.

### 0.A Read these signals first
1. **Page kind** - landing (SaaS / consumer / agency / event), portfolio (dev / designer / creative studio), redesign (preserve vs overhaul), editorial / blog.
2. **Vibe words** - "minimalist", "calm", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "serious B2B", "editorial", "agency-y", "glassy", "dark tech".
3. **Reference signals** - URLs, screenshots, products named, brands competing with.
4. **Audience** - B2B procurement vs design-conscious consumer vs recruiter. Audience picks the aesthetic.
5. **Brand assets** - logo, color, type, photography.
6. **Quiet constraints** - accessibility-first, public-sector, regulated industries. These OVERRIDE aesthetic preference.

### 0.B Output a "Design Read" before generating
Before any code: **"Reading this as: [page kind] for [audience], with a [vibe] language, leaning toward [design system or aesthetic family]."**

### 0.C If ambiguous, ask ONE question
Example: *"Should this feel closer to Linear-clean or Awwwards-experimental?"*
If you can confidently infer, do not ask. Just declare and proceed.

### 0.D Anti-Default Discipline
Do NOT default to: AI-purple gradients, centered hero over dark mesh, three equal feature cards, generic glassmorphism, infinite-loop micro-animations, Inter + slate-900.

---

## 1. SET THREE DIALS

* **DESIGN_VARIANCE: 8** - 1=Perfect Symmetry, 10=Artsy Chaos
* **MOTION_INTENSITY: 6** - 1=Static, 10=Cinematic/Physics
* **VISUAL_DENSITY: 4** - 1=Art Gallery/Airy, 10=Cockpit/Packed Data

**Baseline: 8/6/4** unless design read overrides.

### 1.A Dial Inference
| Signal | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| minimalist/clean/calm/editorial/Linear-style | 5-6 | 3-4 | 2-3 |
| premium consumer/Apple-y/luxury | 7-8 | 5-7 | 3-4 |
| playful/wild/Awwwards/experimental/agency | 9-10 | 8-10 | 3-4 |
| landing page/portfolio/marketing (default) | 7-9 | 6-8 | 3-5 |
| trust-first/public-sector/accessibility | 3-4 | 2-3 | 4-5 |

### 1.B Use-Case Presets
| Use case | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing (SaaS) | 7 | 6 | 4 |
| Landing (Agency/creative) | 9 | 8 | 3 |
| Landing (Premium consumer) | 7 | 6 | 3 |
| Portfolio (Designer/studio) | 8 | 7 | 3 |
| Portfolio (Developer) | 6 | 5 | 4 |
| Editorial/Blog | 6 | 4 | 3 |
| Public-sector | 3 | 2 | 5 |

---

## 2. CHOOSE THE RIGHT FOUNDATION

### 2.A Real Design Systems
| Brief reads as | Reach for |
|---|---|
| Microsoft/enterprise SaaS | @fluentui/react-components |
| Google/Material-flavored | @material/web + Material 3 |
| IBM-style B2B/analytics | @carbon/react + @carbon/styles |
| Shopify app | polaris.js |
| Atlassian/Jira-style | @atlaskit/* |
| GitHub-style devtool | @primer/css or @primer/react-brand |
| UK public-sector | govuk-frontend |
| US public-sector | uswds |
| Fast agency MVP | Bootstrap 5.3 |
| Modern accessible React | @radix-ui/themes |
| Modern SaaS, own components | shadcn/ui |
| Tailwind-based SaaS/AI marketing | Tailwind v4 + dark: variant |

**One system per project. Never mix.**

---

## 3. DEFAULT STACK

### 3.A Stack
* **Framework:** React or Next.js. Default to Server Components (RSC).
* **RSC SAFETY:** Wrap providers with "use client". Motion/scroll components = isolated leaf with 'use client'.
* **Styling:** Tailwind v4. For v4: use @tailwindcss/postcss NOT tailwindcss plugin.
* **Animation:** Motion (motion/react). `import { motion } from "motion/react"`
* **Fonts:** next/font or self-host @font-face + font-display:swap. NEVER link Google Fonts via <link> in production.

### 3.B State
* NEVER use useState to track continuous values (mouse position, scroll, magnetic hover). Use Motion's useMotionValue / useTransform / useScroll.

### 3.C Icons
* Allowed: @phosphor-icons/react, hugeicons-react, @radix-ui/react-icons, @tabler/icons-react
* Discouraged: lucide-react (only if explicitly asked)
* NEVER hand-roll SVG icons. One family per project.

### 3.D Layout Rules
* Viewport Stability: NEVER h-screen. ALWAYS min-h-[100dvh].
* Grid over Flex-Math: ALWAYS CSS Grid, not complex flexbox percentage math.
* Hero Top Padding Cap: max pt-24 at desktop.

---

## 4. ANTI-SLOP DESIGN RULES

### 4.1 Typography
* Display/Headlines: text-4xl md:text-6xl tracking-tighter leading-none
* Discouraged default sans: Inter. Pick Geist, Outfit, Cabinet Grotesk, Satoshi first.
* Pairings: Geist + Geist Mono, Satoshi + JetBrains Mono, Cabinet Grotesk + Inter Tight
* SERIF DISCIPLINE: Very discouraged as default. Only when brief names a serif font, or aesthetic is genuinely editorial/luxury/publication.
* BANNED as defaults: Fraunces and Instrument_Serif

### 4.2 Color
* Max 1 accent color. Saturation < 80%.
* THE LILA RULE: No AI-purple, no random neon gradients. Use neutral bases with high-contrast singular accents.
* COLOR CONSISTENCY LOCK: One accent for the WHOLE page.
* PREMIUM-CONSUMER PALETTE BAN: beige+brass+oxblood+espresso is BANNED for cookware/wellness/luxury briefs.

### 4.3 Layout
* ANTI-CENTER BIAS: Avoid centered hero when DESIGN_VARIANCE > 4. Use Split Screen, Left-aligned, or asymmetric.

### 4.4 Cards
* Use cards ONLY when elevation communicates real hierarchy.
* SHAPE CONSISTENCY LOCK: One corner-radius scale per page.

### 4.5 Interactive States (mandatory)
* Loading: Skeletal loaders matching layout shape. No generic spinners.
* Active feedback: -translate-y-[1px] or scale-[0.98].
* BUTTON CONTRAST CHECK: WCAG AA min 4.5:1.
* CTA BUTTON WRAP BAN: Button text must fit one line at desktop.
* NO DUPLICATE CTA INTENT: Two CTAs with same intent = Pre-Flight Fail.

### 4.6 Hero (mandatory)
* MUST fit in initial viewport: Headline max 2 lines, subtext max 20 words, CTAs visible without scroll.
* HERO STACK - max 4 text elements:
  1. Eyebrow OR brand strip (pick zero or one)
  2. Headline (max 2 lines)
  3. Subtext (max 20 words)
  4. CTAs (1 primary + max 1 secondary)
* Logo wall belongs UNDER the hero, never inside.
* Navigation: single line at desktop, height max 80px.

### 4.7 Section Layout (mandatory)
* Section-Layout-Repetition Ban: Each layout family appears at most ONCE.
* ZIGZAG CAP: Max 2 consecutive image+text-split sections.
* EYEBROW RESTRAINT: Max 1 eyebrow per 3 sections.
* SPLIT-HEADER BAN: "Left big headline + right small explainer" is BANNED.
* Bento Background Diversity: At least 2-3 cells with real visual variation.
* BENTO CELL COUNT: N items = N cells. No empty cells.

### 4.8 Images (mandatory)
* Image-gen tool FIRST. Use generate_image when available.
* Real web images: https://picsum.photos/seed/{descriptive-seed}/{w}/{h}
* Div-based fake screenshots = BANNED. The #1 LLM-design Tell.
* Real company logos: Simple Icons (https://cdn.simpleicons.org/{slug}/ffffff). Not plain text.
* LOGO-ONLY rule: Logo wall = logos only. No category labels below.

### 4.9 Content Density
* Default per section: headline <= 8 words + subparagraph <= 25 words + one visual OR one CTA.
* COPY SELF-AUDIT: Re-read every string. Fix broken or AI-hallucinated phrases.
* No fake-precise numbers without real data.

---

## 5. MOTION PATTERNS

### 5.A GSAP Sticky-Stack Skeleton
```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function StickyStack({ cards }: { cards: React.ReactNode[] }) {
  const ref = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !ref.current) return;
    const ctx = gsap.context(() => {
      const cardEls = gsap.utils.toArray<HTMLElement>(".stack-card");
      cardEls.forEach((card, i) => {
        if (i === cardEls.length - 1) return;
        ScrollTrigger.create({
          trigger: card,
          start: "top top",
          endTrigger: cardEls[cardEls.length - 1],
          end: "top top",
          pin: true,
          pinSpacing: false,
        });
        gsap.to(card, {
          scale: 0.92,
          opacity: 0.55,
          ease: "none",
          scrollTrigger: {
            trigger: cardEls[i + 1],
            start: "top bottom",
            end: "top top",
            scrub: true,
          },
        });
      });
    }, ref);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <div ref={ref} className="relative">
      {cards.map((card, i) => (
        <div key={i} className="stack-card sticky top-0 min-h-[100dvh] flex items-center justify-center">
          {card}
        </div>
      ))}
    </div>
  );
}
```

### 5.B Scroll-Reveal Stagger (lighter)
```tsx
"use client";
import { motion, useReducedMotion } from "motion/react";

export function RevealStagger({ items }: { items: string[] }) {
  const reduce = useReducedMotion();
  return (
    <ul className="grid gap-6">
      {items.map((item, i) => (
        <motion.li
          key={item}
          initial={reduce ? false : { opacity: 0, y: 24 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true, amount: 0.3 }}
          transition={{ duration: 0.6, delay: i * 0.06, ease: [0.16, 1, 0.3, 1] }}
        >
          {item}
        </motion.li>
      ))}
    </ul>
  );
}
```

### 5.C Motion Rules
* window.addEventListener("scroll") = BANNED. Use Motion useScroll(), ScrollTrigger, IntersectionObserver.
* MARQUEE MAX-ONE-PER-PAGE.
* MOTION MUST BE MOTIVATED: hierarchy, storytelling, feedback, or state transition.
* If MOTION_INTENSITY > 4, page must actually animate.

---

## 6. PERFORMANCE & ACCESSIBILITY

* Animate ONLY transform and opacity. Never top/left/width/height.
* Any motion MOTION_INTENSITY > 3 MUST honor prefers-reduced-motion.
* Dark mode: design both modes from start. Respect prefers-color-scheme.
* LCP < 2.5s, INP < 200ms, CLS < 0.1.
* No pure #000000 or #ffffff. Use off-black (zinc-950) and off-white.

---

## 7. AI TELL BANS

### Visual Bans
* NO neon/outer glows by default.
* NO pure black #000000.
* NO excessive gradient text for large headers.
* NO custom mouse cursors.
* NO 3-column equal feature cards. BANNED.

### Content Bans
* NO generic names: John Doe, Sarah Chan - use realistic names.
* NO fake-perfect numbers: 99.99%, 50%.
* NO startup-slop brand names: Acme, Nexus, SmartFlow.
* NO filler verbs: Elevate, Seamless, Unleash, Next-Gen, Revolutionize.

### Pattern Bans
* NO version labels in hero (V0.6, BETA, ALPHA).
* NO section-number eyebrows (00/INDEX, 001 Capabilities).
* NO scroll cues (Scroll, down arrow, Scroll to explore). BANNED.
* NO div-based fake product UI in hero. #1 Tell.
* NO locale/time/weather strips (LIS 14:23 18 deg).
* NO decoration text strip at hero bottom (BRAND. MOTION. SPATIAL.).

### EM-DASH IS COMPLETELY BANNED
NO em-dash anywhere. Zero. Not in headlines, body, quotes, attribution, captions, buttons.
* Use period or comma instead in headlines.
* Use two sentences or comma in body copy.
* Use regular hyphen with spaces in attribution.

---

## 8. PATTERN VOCABULARY

### Hero Types
* Asymmetric Split Hero - text one side, asset other side
* Editorial Manifesto Hero - large type, no asset
* Kinetic-Type Hero - animated typography as primary visual
* Curtain-Reveal Hero - parts on scroll
* Scroll-Pinned Hero - stays pinned while content scrolls

### Layout Types
* Bento Grid - asymmetric tile grouping
* Masonry Layout - staggered, no fixed row height
* Split-Screen Scroll - two halves opposite directions
* Sticky-Stack Sections - pin and stack on scroll
* Horizontal Scroll Hijack - vertical to horizontal pan

### Micro-Interactions
* Magnetic Button - pulls toward cursor (Motion useMotionValue only)
* Directional Hover-Aware Button - fill from cursor side
* Skeleton Shimmer - loading state
* Mesh Gradient Background - organic blobs
* Spotlight Border Card - borders illuminate under cursor

---

## 9. PRE-FLIGHT CHECKLIST

Run every item. If any fails, output is not done.

- [ ] Design Read declared (one-liner)?
- [ ] Dial values explicit and reasoned?
- [ ] ZERO em-dashes anywhere? Non-negotiable.
- [ ] ONE theme for whole page (no section flips)?
- [ ] One accent color used consistently?
- [ ] One corner-radius system?
- [ ] Button contrast WCAG AA 4.5:1?
- [ ] No CTA wraps to 2+ lines at desktop?
- [ ] No duplicate CTA intent?
- [ ] Serif NOT Fraunces or Instrument_Serif?
- [ ] Premium-consumer NOT beige+brass+espresso?
- [ ] Hero fits viewport (headline <= 2 lines, subtext <= 20 words)?
- [ ] Hero top padding max pt-24?
- [ ] Hero max 4 text elements?
- [ ] Eyebrow count <= ceil(sectionCount/3)?
- [ ] No split-header pattern?
- [ ] No 3+ consecutive zigzag sections?
- [ ] Logo wall under hero, real SVG logos?
- [ ] At least 2-3 bento cells with real visual variation?
- [ ] Copy self-audit done (no broken/AI phrases)?
- [ ] Every animation motivated?
- [ ] Max one marquee per page?
- [ ] Navigation single line at desktop, height <= 80px?
- [ ] At least 4 different section layout families?
- [ ] Bento has exact cell count (no empty cells)?
- [ ] Real images used (no div-based fake screenshots)?
- [ ] No pills/labels overlaid on images?
- [ ] No version footers (v1.4.2) on marketing pages?
- [ ] No scroll cues?
- [ ] No section-numbering eyebrows?
- [ ] Content density sane (<= 25-word sub-paragraphs)?
- [ ] Quotes <= 3 lines?
- [ ] No window.addEventListener("scroll")?
- [ ] Reduced motion wrapped for MOTION_INTENSITY > 3?
- [ ] Dark mode tokens defined and tested?
- [ ] Mobile collapse explicit for high-variance layouts?
- [ ] min-h-[100dvh] not h-screen?
- [ ] No AI Tells (Inter, AI-purple, three-equal cards, Jane Doe)?
- [ ] LCP < 2.5s, INP < 200ms, CLS < 0.1 plausible?
- [ ] One design system per project (no mixing)?

---

## 10. SCOPE - NOT FOR

* Dashboards / dense product UI / admin panels
* Data tables (use TanStack Table or AG Grid)
* Multi-step forms / wizards
* Code editors (use Monaco / CodeMirror)
* Native mobile (use Apple HIG / Material)

---

Credit: Based on https://github.com/Leonxlnx/taste-skill (MIT License)
