<!-- craft-house-rules:start core source=dde09ea31e2e457f5b4653a6e76f7cdf55944bdf sha256=540e6cea75d12d0710c3dca89658328e81e508ecef102446ca5bb95b7c0b92bb -->
## House rules

These apply in every Craft repository. A later rule may be stricter, not weaker. The source is `standards/house-rules-core.md` in `storytold/craft-contrib`. Propose changes there, not in a copy.

1. **A person is accountable.** Whoever runs an agent answers for what it opens and for its review comments.
2. **Check, then claim.** Before writing code, read the issue comments, search pull requests for `#N` and the keywords, and check recent commits on `main`. Comment on the issue first. Release a claim you will not finish.
3. **Verify, don't guess.** Open a definition before using it. Confirm the cause in the code, even when someone names a location.
4. **Keep fixes narrow and tested.** Fix what the issue describes, where the bug is. Add a test that fails without the fix.
5. **Review the diff before opening a pull request.** Identifiers exist as used, the test fails without the fix, nothing unrelated changed, and the description is true.
6. **Look for a better pull request.** If another fixes the same thing, close yours when it is better or equal, and say why.
7. **Report only what ran.** Say what you tested and what you could not run. Without a local build or test, say so and rely on CI before marking ready.
8. **`main` changes through a pull request.** Do not push to it. Branch protection enforces this. There is no exception.
9. **Stop and ask only about** licensing outside the allowlist, publishing, releases, a new remote, secrets, spending money, destructive git, and anything else hard to undo. Otherwise keep working. `plan/` is a gitignored notebook, not rules. Without it, do not ask for it and do not stop.
10. **Keep secrets and personal details out** of the repository, logs and requests.
11. **CI stays shared.** Workflows call `storytold/craft-common-actions`. Do not change CI in a feature or fix pull request. If CI cannot cover a change, open an issue there.
12. **Guards say why.** A check that looks removable says what it prevents. Read that before changing it.
13. **Instructions must be readable by everyone.** No notes about one machine, and no links to files a reader cannot open. `craftrules` is retired. Do not link to it.
14. **Keep pull requests moving.** Concurrent pull requests are fine; unanswered actionable feedback is not. Respond in 7 days, a reminder at 14, closure eligible at 30, from when an actionable request waits on the author. Suggestions and unconfirmed bot findings do not start the clock. A fix, explanation or agreed plan resets it; unrelated activity does not. Waiting on a reviewer or maintainer pauses it and does not count against the author. A maintainer decides closure; it is never automatic. Reuse search results, do not poll, and stop at a rate limit.
15. **No agent attribution.** A pull request does not say an agent wrote it. A repository rule may not require that.
<!-- craft-house-rules:end -->
<!-- craft-house-rules:start rust source=dde09ea31e2e457f5b4653a6e76f7cdf55944bdf sha256=387e0ccb4b49e567f60951d7d6fff7305054c89f43ad812b9993dc7c38528013 -->
## Rust Craft repositories

These apply to native Craft apps and to shared Rust libraries. Select them by repository type. A repository that merely contains some Rust does not take this block. Rules later in a repository's file may be stricter, but not weaker. The source is `standards/house-rules-rust.md` in [storytold/craft-contrib](https://github.com/storytold/craft-contrib).

1. **Never crash.** Non-test code does not panic and has no `unsafe`, except where the repository file names an exception. Return errors, treat input as hostile, and bound recursion and allocations. New production crate roots copy the `deny` attribute from an existing crate: `clippy::unwrap_used`, `clippy::expect_used`, `clippy::panic`, `clippy::unimplemented`, `clippy::todo`, `clippy::unreachable`. Every crash fix comes with a test that panicked before the fix.
2. **Clean room.** Learn from observed behaviour and public specifications. Do not copy another product's code, assets, strings or artwork. Check a dependency's licence before adding it.
3. **Assets and fonts.** Every asset is original or suitably licensed, and is recorded in `ATTRIBUTION.md` in the same change. Font files live in [storytold/craft-fonts](https://github.com/storytold/craft-fonts), not in the app repository.
4. **Rust only for native Craft apps.** No handwritten JavaScript or TypeScript, and no Tauri, Electron or webview shell, in those apps. Shared tooling follows its documented technical scope and maintainer-approved exceptions. Craft PR Review's existing Tauri and TypeScript UI is one such exception. It does not relax this rule for native apps. Preserve any existing web build.
5. **Time goes through `chrono`.** Do not hand-roll calendar conversion. For dates beyond what `chrono` can represent, follow [standards/time.md](https://github.com/storytold/craft-contrib/blob/main/standards/time.md).
6. **Contributor credits.** Add or edit only your own person's entry in `contributors/people.toml`, and only after asking them. Never guess a name or hand-edit `contributors.json`.

## Licence allowlist

Dependencies and assets use SPDX identifiers. An expression is allowed when every identifier is in this list. A repository may name a shorter list. It may not add an identifier here by editing its own copy of these rules.

- `ISC`
- `MIT`
- `BSD-2-Clause`
- `BSD-3-Clause`
- `Apache-2.0`
- `OFL-1.1`
- `Ubuntu-font-1.0`
- `Bitstream-Vera`
- `CC0-1.0`
- `CC-BY-4.0`
- `CC-BY-SA-4.0`
- `LicenseRef-Public-Domain`

`LicenseRef-Storyteller-Trademark` is not in this list. It covers Storyteller brand marks only, where a repository already says so.
<!-- craft-house-rules:end -->

# AGENTS.md — DeckCraft rules

DeckCraft is a clean-room, pure-Rust presentation app aiming at PowerPoint parity and beyond (speed,
openness, agent control). It runs on macOS, Windows, Linux, FreeBSD and the web (WASM). These rules
bind every agent and contributor, before any task or deadline. `CLAUDE.md` imports this file. The
house rules above apply too; this file only adds DeckCraft's own.

## Mirai fork

- The app is called **Mirai Presentations** (`crates/ui-egui/src/brand.rs`); the built-in
  "DeckCraft" theme keeps its name.
- Identifiers keep upstream's DeckCraft names: binary, crates, app id, file format, settings folder,
  installer registry keys and UpgradeCode.
- When merging upstream, keep the Mirai name in titles, About, README and installer display names,
  and keep the ArtCraft name, wordmark and logos (ArtCraft Team trademarks) out, as upstream asks of
  forks.

## 1. Assets

An asset is any non-code material the project ships, embeds, publishes or shows in its docs: icons,
images, screenshots, logos, fonts, colour profiles, sounds, video, templates, themes, sample or test
documents, and anything rendered from them.

- **Nothing from Microsoft, Adobe, Avid or Autodesk**: no asset from their products, installers,
  sites or packages, including the fonts they install (Aptos, Calibri, Cambria, Segoe, Consolas,
  Wingdings…). This holds for openly licensed vendor *visual design* too: Adobe's Source
  Sans/Serif/Han and Noto CJK stay out (`crates/fonts/build.rs` excludes them).
- Never recreate, trace or closely imitate a vendor icon, theme or graphic. Icons are drawn in code
  or come from Lucide (ISC); themes, colours, layouts and sample content are our own.
- Allowed licences: the house rules' allowlist, or contributor-original work under
  `MIT OR Apache-2.0`. Forbidden: non-open system fonts, vendor emoji, stock photos, "free for
  personal use" material, screenshots of other software, anything whose licence you cannot prove at
  its original source.
- Screenshots of DeckCraft are fine if everything visible is allowed (our UI and icons, OFL fonts,
  decks built from allowed assets).
- Never commit files PowerPoint produced. Interoperability tests use decks we generate ourselves, or
  a separate corpus repo of files we created and own.
- Fonts live in [storytold/craft-fonts](https://github.com/storytold/craft-fonts), never here; builds
  embed them through `CRAFT_FONTS_DIR` (`.cargo/config.toml` sets it to a `craft-fonts` checkout next
  to this repo).

**Adding an asset:** take it from its original source under an allowed licence and record the exact
version or commit; add the file, its licence and an `ATTRIBUTION.md` row (author, source, licence,
use) — this covers files committed, fetched at build time (craft-fonts) or bundled through a
Cargo dependency; keep required notices in `NOTICE`; run `cargo xtask assets`, which fails for any file under
`assets/`, `docs/images/` or `examples/` without a row. If origin or licence is unclear, don't add
it. If you find an asset that breaks these rules, remove it from the repo and every output at once
and tell the user.

## 2. Clean room

- PowerPoint may only be observed black-box: run it on synthetic decks and take window screenshots
  into `plan/powerpoint/screenshots/`, which are never committed, published, linked or traced. Never
  read, disassemble or copy anything inside the Office bundle; copy no Microsoft wording beyond
  feature and menu names.
- Formats come from public standards: ECMA-376 / ISO/IEC 29500 (OOXML) and ISO 32000 (PDF). Preset
  shape and warp geometry come from the shared `craft_drawingml` crate (craft-libs), re-exported by
  `crates/geom`.
- Never copy GPL, AGPL, LGPL or MPL code (LibreOffice, Calligra…). Permissive crates may be
  dependencies; code may be copied from sibling Craft apps.
- Before adding file-format, codec, protocol or reusable UI code, check `storytold/craft-libs` and
  its open PRs; extend the shared library instead of duplicating it. Keep app-specific policy and
  model mapping here, and keep behaviour, security and resource limits, attribution and regression
  tests through any cutover.

## 3. Never crash

A crash loses someone's talk, so this outranks feature work. Beyond the house rules: input-derived
numbers (files, commands, MCP and control params) are hostile, so use `get()` not `[i]`, checked
arithmetic, no NaN casts, capped allocations and bounded recursion. `Session::execute` runs each
command in a panic guard (`crates/engine/src/guard.rs`) that keeps the presentation unchanged; it is
a safety net, not a licence.

## 4. Architecture

Layers, checked by `cargo xtask layers` (`xtask/src/layers.rs`); a crate depends only on lower
layers:

| Layer | Crates |
|---|---|
| L0 | `geom` (units, transforms, shapes), `color` |
| L1 | `model` (presentation, masters, layouts, slides, shapes, text, themes), `fonts` |
| L2 | `text` (layout), `anim`, `media`, `format` (.deckcraft) |
| L3 | `render` (vello_cpu), `pptx` |
| L4 | `pdf`, `assistant` |
| L5 | `engine` (session, history, commands, tools, keys) |
| L6 | `ui-egui`, `mcp` |
| apps | `deckcraft` (desktop), `deckcraft-cli`, `deckcraft-web` |

- **Everything is a command** (`crates/engine/src/cmd/`): id, label, ribbon or menu place, shortcut,
  params doc, `enabled`, `run`, and tests. Ids follow PowerPoint's ribbon and menus (`slide.new`,
  `format.bold`, `arrange.group`…). Programmatic calls never open dialogs. Pointer gestures go
  through `Session::pointer` and keys through `Session::key`, so the UI, CLI, control channel and MCP
  behave the same.
- **The UI is thin**: panels read engine state and act through commands; colours come from theme
  tokens. egui only, never Tauri. Nothing below `ui-egui` depends on egui, eframe, winit or rfd.
- Never break WASM (`cargo xtask wasm`).

## 5. Before every commit

Run `cargo xtask ci`: fmt check, `pdf-deps`, clippy `-D warnings`, tests (nextest when installed),
doctests, assets, layers and WASM. Commit after each finished piece of work with a task id in the
message (`M1.2: smart guides`). New crates add `workspace = true` under `[lints]` and put the
crate-level lint attributes before any module (only `//!` docs may precede them).

## 6. Running and checking the app

- `cargo run --release -p deckcraft -- --sample --control 7990` opens the sample deck with the
  control channel on `127.0.0.1:7990`. Send JSON lines, e.g.
  `{"id":1,"method":"engine.execute","params":{"command":"shape.insert","params":{"preset":"star5","rect":[100,100,200,200]}}}`
  and `{"id":2,"method":"ui.screenshot","params":{"path":"/tmp/shot.png"}}`. Methods are in
  `crates/ui-egui/src/control.rs` and `docs/control-protocol.md`.
- For UI work, look at the result: take a screenshot and read the PNG. Compare it with the task and
  the committed docs.
- Headless: `deckcraft-cli render --sample --all --scale 1 out/` and
  `deckcraft-cli run --sample --cmd 'slide.new={"title":"Hi"}' --export out.png`.
- MCP: `deckcraft-cli mcp` (headless) or `deckcraft-cli mcp --connect 7990` (drives the running
  app); see `docs/mcp.md`.
- Parallel agents use separate `CARGO_TARGET_DIR`s and edit only the crates they own.

## 7. Progress docs

| File | Holds |
|---|---|
| `docs/gaps.md` | Known shortfalls, ranked: the work list. Pick from the top |
| `docs/parity-checklist.md` | Feature rows scored D/P/M; `cargo xtask parity` regenerates the summary |
| `ROADMAP.md` | Stage, headline numbers, features, languages, progress log |
| `docs/roadmap.md` | Current focus, beta plan, milestones |
| `docs/target-app-parity.md` | Parity assessment against PowerPoint |
| `docs/*-parity.md` | Detail per dimension: file format, UI, hardware, localization, animation, slide show |
| `docs/architecture.md` | How DeckCraft is built today |

When a task lands: re-score its checklist row, update or delete its `gaps.md` entry, add a line to
the `ROADMAP.md` progress log, and update the status line and revision history of each doc you
touched.

## 8. Subagents (OpenCode)

- First choice: GPT-6.1 Terra, preferably from the OpenAI provider. Any available model or provider
  may be used when the task needs it; check what exists with `opencode.models` and never hardcode
  model ids in code or docs.
- Bounded tasks (search, review, implementation, tests) may be delegated. Cross-provider
  verification is not required; the user decides when to ask for a verifier.
- Weigh capability, reliability, cost and availability. If a model fails or runs out of quota, say
  so and switch; don't keep retrying it.
- Escalate hard problems (difficult design, stubborn bugs, high-risk reviews) to stronger models
  such as Claude Opus 5.5 or GPT-6.1 Sol, say why, and go back for routine work.
- The main agent coordinates, decides and reviews delegated work. Every rule here binds subagents.

## 9. Contributor credits

About ▸ Contributors is built from `contributors/contributors.json` (generated; never hand-edit) and
`contributors/people.toml` (names people chose); see `docs/contributors.md`. When you prepare a PR
for someone whose GitHub username has no `[people.<username>]` entry, ask them once whether they
want a real name, display name or their GitHub profile name (`sync_github_name = true`). If yes, add
only their entry, from the template at the top of the file, in their PR. If no, change nothing: they
are credited as `@username`. Never add, edit or guess anyone else's entry or name, and never copy names from git config,
commit authors or GitHub profiles.

## 10. CI

Workflows in `.github/workflows/` only call the shared workflows in
[storytold/craft-common-actions](https://github.com/storytold/craft-common-actions) at `@main`.
Don't add or change CI in a feature or fix PR: if a change can't be built or tested, link or open a
craft-common-actions issue, or send it a small PR that is safe for every app and doesn't lengthen
CI. Some workflow files still run their own jobs; don't add to them. Moving a job to
craft-common-actions is a task of its own, and the job stays here until a shared workflow runs it.
