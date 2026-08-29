# thebuggeddev/anatomy

- **Source**: https://github.com/thebuggeddev/anatomy
- **Repository description**: An interactive 3D human anatomy explorer built using Three.js with GPT 5.6 Sol
- **Homepage**: https://anatomyatelier.vercel.app
- **GitHub snapshot**: 2,760 stars, 769 forks, 24 open issues (API metadata fetched 2026-08-29)
- **Default branch**: `main`
- **Created**: 2026-08-02
- **Last pushed**: 2026-08-09
- **Primary language**: TypeScript
- **License**: GitHub API metadata does not specify a license

## README summary

The README currently describes the repository as a `vinext-starter`: a full-stack starter built on Cloudflare's vinext, with optional Cloudflare D1 and Drizzle support. It documents Node.js `>=22.13.0`, `npm install`, `npm run dev`, `npm run build`, optional workspace identity headers, and Dispatch-owned Sign in with ChatGPT helpers.

The application code in `app/` is more specific than the generic README: it implements the Anatomy Atelier experience described in the repository metadata.

## Implementation outline

- `app/[locale]/page.tsx` loads a locale dictionary and renders `AnatomyApp`.
- `app/components/AnatomyApp.tsx` owns the library, search, locale switching, comparison strip, lessons, quiz entry point, and organ detail panel.
- `app/components/OrganViewer.tsx` bridges React state to the Three.js viewer, including loading state, auto-rotation, compare mode, and the interactive labelling quiz.
- `app/lib/three/viewer.ts` implements the WebGL scene, orbit controls, render-on-demand loop, hotspots, cross-section/isolation behavior, and authoring probe.
- `app/lib/anatomy-data.ts` defines nine organ structures and stable anatomical hotspot identifiers.
- `app/i18n/` provides UI and organ dictionaries for 12 locales: English, Spanish, Hindi, Chinese, Arabic, Portuguese, French, German, Japanese, Russian, Indonesian, and Korean.
- `public/models/` supplies GLB assets and `public/anatomy/` supplies illustrated specimen assets (the code supports a glyph fallback when an illustration is unavailable).

## Supported organs and anatomy data

The structure registry includes heart, brain, lungs, liver, kidneys, eyeball, intestine, pancreas, and skin. Each organ has a model path, accent color, scientific Latin name, and interactive hotspots. Examples include heart chambers and mitral valve, brain lobes and cerebellum, lung trachea/bronchi, kidney cortex/medulla/ureter, and the three skin layers.

## User experience

- Interactive 3D specimen: drag to rotate, scroll to zoom, auto-rotate toggle, reset, isolate, layers/cross-section tools, and hotspot callouts.
- Organ library with locale-aware search across organ name and system.
- Compare mode, currently pairing the selected organ with a reference organ (the implementation uses brain or heart as the reference).
- Guided lessons, function animation, clinical notes, microscopic view, system context, and common-condition cards.
- Labelling quiz: asks the learner to find every hotspot once in a shuffled order, reports correct/incorrect selections, reveals the target after a miss, and shows a score.
- Accessibility details include labelled canvas instructions, keyboard handling, live quiz status, and RTL measurement isolation for numeric ranges.

## Technology and deployment

- React 19 and Next.js 16 through vinext/Vite.
- Three.js 0.185 for WebGL rendering, `OrbitControls` for camera interaction, and GSAP for reveal/fade animation.
- Tailwind CSS 4, Lucide React icons, TypeScript 5.9, and optional Drizzle ORM/D1 integration.
- Vercel configuration is present; the README also targets Cloudflare vinext workflows.
- Required Node.js version: `>=22.13.0`.

## Assessment

This is a strong example of a design-forward educational web app using a real-time 3D scene rather than a static anatomy catalogue. Its most reusable engineering ideas are the separation of locale-independent anatomical structure from translated content, render-on-demand Three.js behavior, asset prefetching, and a quiz that communicates through long-lived viewer callbacks.

The repository should not be treated as a medically authoritative reference solely on the basis of its UI copy. The project does not state a formal medical-content review process, and the GitHub metadata does not declare a license.
