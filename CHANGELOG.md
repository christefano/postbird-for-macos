# Changelog

- Fixed table view's read/unread text color swap: `--unread-color` pointed at
  the dark sender tone and read rows were left on BB's native light color,
  so table view showed white read text and dark unread text on BB's dark
  background. Unread rows now use the sidebar-primary light tone; read rows
  get the Postbox sender tone directly.
- Increased toolbar label size (0.8rem → 0.95rem), folder row height (20px →
  24px), and folder name size (0.9rem → 1.05rem) for readability.
- Removed `CONTRIBUTING.md`, `docs/backlog.md`, and `docs/screenshot.png`
  (stale, not applicable to this fork).
- Removed the Windows-only PowerShell deploy scripts; added a manual macOS
  install path (README).
- Added dark mode support: folder pane, main toolbar, tab strip, status bar,
  and compose window now follow `prefers-color-scheme` instead of staying
  pinned to the light palette. The "spaces" icon rail stays pinned light in
  both modes, matching upstream's original intent for that region.
- Fixed the compose window's recipient (To/Cc/Bcc) row and Subject field
  rendering as an unstyled black bar under macOS system dark mode.
- Fixed a native dark-mode text-shadow leftover that made the status bar text
  look embossed/doubled after recoloring it for dark mode.
- **Spaces toolbar** (`spacestoolbar.css`): light rail (`#E8E8E8`, matching the
  toolbar), vertically-centered icons, slightly smaller (16px) — with the window
  content shift kept flush (no gap).
- **Folder pane**: hide the whole header bar (New Message / Get Messages / more)
  — FP-12; section divider toned into the pane; symmetric section spacing.
- **Message header**: hide noisy technical rows (message-id, references,
  user-agent, list-\*, …) — MH-09 / "Port A".
