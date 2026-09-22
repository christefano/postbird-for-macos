# Changelog

All notable changes to postbird. Versions track the definition of done in
`CLAUDE.md`; after v1.0, only migration repairs (Betterbird ESR bumps) are in
scope unless scope is explicitly re-opened.

## [macOS port] — 2026-09-21

Downstream macOS build of [Ocanamat/Postbird](https://github.com/Ocanamat/Postbird).

- Removed the Windows-only PowerShell deploy scripts; added a manual macOS
  install path (README).
- Added dark-mode support: folder pane, main toolbar, tab strip, status bar,
  and compose window now follow `prefers-color-scheme` instead of staying
  pinned to the light palette. The "spaces" icon rail stays pinned light in
  both modes, matching upstream's original intent for that region.
- Fixed the compose window's recipient (To/Cc/Bcc) row and Subject field
  rendering as an unstyled black bar under macOS system dark mode.
- Fixed a native dark-mode text-shadow leftover that made the status bar text
  look embossed/doubled after recoloring it for dark mode.

## [1.1.0] — 2026-07-09

Layout + spaces toolbar, and one-command setup tooling.

### Theme (CSS)
- **Spaces toolbar** (`spacestoolbar.css`): light rail (`#E8E8E8`, matching the
  toolbar), vertically-centered icons, slightly smaller (16px) — with the window
  content shift kept flush (no gap).
- **Folder pane**: hide the whole header bar (New Message / Get Messages / more)
  — FP-12; section divider toned into the pane; symmetric section spacing.
- **Message header**: hide noisy technical rows (message-id, references,
  user-agent, list-\*, …) — MH-09 / "Port A".

### Setup tooling (PowerShell)
- **`deploy.ps1` now does everything in one command**: copies the CSS, applies
  recommended prefs, and applies recommended layout (the latter only if
  Betterbird is closed). `-SkipPrefs` / `-SkipLayout` to opt out.
- **`configure-prefs.ps1`** (`user.js`): message-pane layout = Vertical, Cards
  view, 2-line cards, icon-over-text toolbar, threaded view, show-time,
  multiline, and enabling userChrome.
- **`configure-xulstore.ps1`** (`xulstore.json`): clean mail-toolbar layout
  (native buttons + flexible spaces), folder-pane modes (Unified Folders + All +
  Tags), menu-bar auto-hide, quick-filter hidden, compact message header.

### Docs
- README screenshot; roadmap gains the star-next-to-subject and collapsible-
  header items (userChrome.js layer).

## [Unreleased]

## [1.0.0] — 2026-07-09

First complete theme. Targets **Betterbird 140.12.0esr-bb24**. Recreates
Postbox's "Monterail Dark" look. All colors/sizes are `--pb-*` tokens in
`chrome/postbird/config.css`; every rule is mapped in `docs/selector-map.md`.

### Themed regions
- **Thread pane** — two-line card rows; warm-neutral text (`#4C4C4C` / slate
  `#5E6C79`); unread = bold only; pale-blue unread dot, vertically centered;
  per-account color band (widened); flat list with hairline row dividers;
  solid-orange focused selection; smaller, centered sender gravatar (via the
  add-on's `.recipient-avatar`); chrome-grey header bar.
- **Folder pane** — dark charcoal sidebar (`#343430`) with light text; account
  icons carry their assigned color (subfolders + unified root stay grey); no
  account-row wash; orange focused / muted-orange unfocused selection; orange
  unread pills (borderless, incl. collapsed accounts); compact rows; symmetric
  section spacing; divider toned into the pane; dark header bar.
- **Toolbar** — Monterail two-tone background; per-button flat icon tints;
  tighter icon-over-text buttons; menu bar matched.
- **Tabs** — active tab reads as chrome grey against a darker strip; inactive
  tabs recede; divider under the tab bar.
- **Message header** — chrome-grey band; message body as a floating white card
  on a grey frame (no divider line); "To" shown and bottom-aligned; smaller
  avatar.
- **Composer** — toolbars + header on the chrome band; menu bar matched;
  writing area as a card matching the reader.
- **Status bar** — thin chrome strip, top divider, muted text.
- **Email body** (`userContent.css`) — line-width cap on plain/flowed text
  (HTML mail untouched); `pre` wraps; muted accent quote border; faded
  signatures; accent selection.

### Known limitations (see `docs/backlog.md`)
- Coloring thread/header text *per account* isn't possible CSS-only (Betterbird
  applies the account color as an inline background/border, not a token).
- Multi-hue toolbar icons would need asset replacement.
- Postbox's Focus Pane has no Betterbird equivalent.
