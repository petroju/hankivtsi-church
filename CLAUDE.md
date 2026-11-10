# CLAUDE.md — Frontend Website Rules

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.
  If it isn't installed as a skill, read it from https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md
- Read `Church website.md` (the project note) for decisions so far and what's still missing.

## About This Site
- Church: Храм Успіння Пресвятої Богородиці, ПЦУ, с. Ганьківці. YouTube: https://www.youtube.com/@hankivtsi.cherch
- Audience: mostly older parishioners on phones. Body text 18px or larger, high contrast, tap targets 48px or more, plain words on buttons, calm motion only.
- Languages: Ukrainian first, English second (a UA/EN switch).
- No personal data about people. Show only real content the user gave; never invent church facts.

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Use the real assets from `brand_assets/`; use `https://placehold.co/` only where no real asset exists. Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- `serve.mjs` lives in this folder and serves it at `http://localhost:3000` (the home page is `/site/home.html`).
- Start it with the built-in browser: `preview_start` with the name `church-site` (defined in the vault's `.claude/launch.json`). If it's already running, don't start a second instance.

## Screenshot Workflow
- Use the built-in browser (Browser pane) to screenshot `http://localhost:3000/...`. Puppeteer isn't installed on this machine.
- Always check two sizes: phone (`resize_window` preset `mobile`, 375×812) and desktop. Reset to `desktop` when done.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing, and that no text runs off the screen.

## Output Defaults
- Single HTML file, all styles inline, unless user says otherwise. Pages live in `site/`.
- Tailwind CSS via CDN, pinned: `<script src="https://cdn.tailwindcss.com/3.4.17"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT` (only when there's no real photo)
- Mobile-first responsive
- Publishing as a Claude artifact: external images (placehold.co, YouTube thumbnails) are blocked there, so embed photos as data URIs. `site/home.src.html` holds `{{IMG_...}}` tokens that are replaced with the photos from `site/img/` to make `site/home.html`.

## Brand Assets
- Always check the `brand_assets/` folder before designing. It may contain logos, color guides, style guides, or images.
- If assets exist there, use them. Do not use placeholders where real assets are available.
- If a logo is present, use it. If a color palette is defined (`brand_assets/palette.md`), use those exact values — do not invent brand colors.

## Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette (indigo-500, blue-600, etc.). Pick a custom brand color and derive from it.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Never use the same font for headings and body. Pair a display/serif with a clean sans. Apply tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body. Both fonts must support Cyrillic, and headings must stay readable and fit a 375px screen.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing. Respect `prefers-reduced-motion`.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`. Keep photos bright enough to see the church clearly.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
- Do not publish without checking the phone-size screenshot first
