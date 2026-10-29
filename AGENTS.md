# esl-lesson-adventure Agent Instructions

<!-- BEGIN:cross-agent-agent-rules -->
## Cross-Agent Compatibility

This repository is prepared for both Codex and Claude Code. `AGENTS.md` is the single instruction file for every agent; keep durable project instructions here.

### Start Here
- [README.md](README.md) — README.
- [ARCHITECTURE.md](ARCHITECTURE.md) — required reading: app purpose, folder structure, module map, data flow, gotchas.
- [docs/AGENT_GUIDE.md](docs/AGENT_GUIDE.md) — agent guide.

### Guidance Notes
- Translate Claude-specific tool, memory, slash-command, or subagent wording to Codex equivalents.

### Common Commands
- Install locked dependencies with `npm ci` (Node.js 24, also used in CI).
- Local dev: `npm run dev` (Vite dev server, http://localhost:5173).
- Tests: `npm test` (Vitest regression tests in `tests/`).
- TypeScript validation: `npm run typecheck`.
- Build: `npm run build` (production build to `dist/`).
- Preview production build: `npm run preview`.
- CI: `.github/workflows/ci.yml` runs tests, typecheck, and build on pushes to `main` and pull requests targeting `main`.

### Stack
- React 19 + TypeScript 7 + Vite 8 + Tailwind CSS 4; Vitest 4.1.12 (locked test runner)

### Critical Gotchas
- **No router** — navigation is a flat integer switch (`activeModule`) in `App.tsx`
- **Test suite** — seven Vitest files in `tests/` cover Bingo export, coordinates, emoji lookup, hunt placement, treasure game mechanics, word guessing, and prepared word pictures; run all three CI checks before submitting changes.
- **Module1_AlphabetCreator** is unreachable from nav (superseded by Module0)
- **Module4_Battleships** takes vocab as props, not from context — unique among game modules
- **`Module6_LetterExplanation/`** is imported as `Module7LetterExplanation` — naming mismatch, don't rename without fixing the import
- **Two Module4_ folders** (`Battleships` + `Bingo`) — unrelated games, naming collision
- Default UI language is `'de'` (German) — bilingual app (DE teacher / EN student)
- Images are emoji strings OR `data:image/svg+xml;base64,` — always use `ImageRenderer` component
- `localStorage` keys: `esl-lesson-vocabulary` (vocab) and `esl-lesson-settings` (settings)
- Minimum 15 words required (`MIN_WORDS_FOR_GAMES`) before Games button appears

### Working Rules
- Keep changes small, reviewable, and tied to the requested behavior.
- Prefer existing architecture, naming, and helper patterns over new abstractions.
- Validate data at system boundaries instead of relying on guessed shapes.
- Update docs when behavior, commands, architecture, or setup changes.
- Run the narrowest relevant verification first, then broader checks when risk warrants it.
- If a command cannot run, record the blocker and the residual risk in the handoff.
<!-- END:cross-agent-agent-rules -->

## Notes

Add project-specific architecture, testing, release, and safety rules above or in linked docs as they become stable. Keep this file concise enough to fit comfortably in agent context.
