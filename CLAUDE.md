# Break the Block — Development Rules

## Project Structure
- **Static site**: 6 HTML pages (index, introduction, chapter1, chapter2, key-takeaways, resources)
- **Shared styles**: `styles.css` — all reusable CSS lives here
- **Page-specific styles**: Inline `<style>` blocks in each HTML page for page-only layout (e.g. resources.html timeline, key-takeaways.html lesson grid)
- **Resources**: PDFs, images, and documents in `/resources/`
- **Supporting docs**: Wikipedia draft and other non-web files in `/supporting-docs/`

## CSS Rules
1. **No inline `style=""` attributes** — use CSS classes. Move any existing inline styles to `styles.css` or the page's `<style>` block.
2. **All shared styles go in `styles.css`** — if a style applies to more than one page (nav, footer, cards, typography, buttons), it must be in `styles.css`, not duplicated inline.
3. **Page-specific styles stay in `<style>` blocks** — styles unique to a single page (e.g. timeline layout in resources.html) belong in that page's `<style>` block.
4. **Never duplicate styles** — before writing new CSS, check if `styles.css` already has a class for it.
5. **Use CSS variables** — colors, spacing, and fonts use `:root` variables defined in `styles.css`.

## Design System
- **Card borders**: Full `2px solid` border with `border-radius: 8px`. Never use `border-left` for cards.
  - Rail-blue cards: `border: 2px solid rgba(0, 78, 137, 0.15)`
  - Accent cards: `border: 2px solid rgba(255, 107, 53, 0.25)`
  - Hover: `border-color: var(--accent)` with smooth transition
- **Left border is only for blockquotes** (e.g. `.dedication-text`), never for cards or containers.
- **Hover transitions**: Always use `transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1)` on the base element. Never add hover transforms without a transition.
- **Hover lift**: Cards use `translateY(-3px)` or `translateY(-4px)`, not `translateX` or `scale`.
- **Typography**: Space Mono for headings/nav/monospace, Crimson Pro for body text.
- **Colors**: `--primary` (#1a1a1a), `--accent` (#ff6b35), `--secondary` (#f7931e), `--rail-blue` (#004e89), `--light` (#f5f5f0), `--text` (#2d2d2d), `--text-muted` (#555).
- **Border variables**: `--border-blue` (rail-blue at 15% opacity) for blue-accent cards, `--border-accent` (accent at 25% opacity) for orange-accent cards. Never hardcode `rgba()` border colors — use these variables.

## Document Cards (resources.html)
- Each card has a type badge: `<span class="doc-type-badge pdf|link|image|map">TYPE</span>`
- Content split into `<span class="doc-title">` and `<span class="doc-desc">`
- Descriptions should be concise (under 20 words)

## SEO & Schema
- Every page has: meta description, meta keywords, Open Graph, Twitter Card, canonical URL, robots directives
- JSON-LD structured data on every page (Book, BreadcrumbList, page-specific schemas)
- `robots.txt` blocks PDFs and admin paths; allows all AI crawlers
- `sitemap.xml` lists all 6 pages

## Git & Deployment
- Hosted on GitHub Pages at breaktheblock.in
- GoatCounter analytics on all pages
- Always commit with descriptive messages; push only when asked
- `supporting-docs/` is in `.gitignore` — never commit files from this folder (manuscripts, drafts, marketing plans). Use `git add -f` only if the user explicitly asks to override this.
