# Design — Project Identity

> This document is project-long-lived. Tokens are not changed without
> the Architect's approval. Developers MUST use these tokens
> instead of improvising their own colors/spacings.

## Style Direction

Calm, technical light console in the spirit of Linear/Stripe: neutral off-white surfaces, one indigo accent, Inter for UI and JetBrains Mono for ids and figures, with clearly distinguishable status badges (colour + text).

## Colors

- `--color-bg`: **#F6F7F9**
- `--color-surface`: **#FFFFFF**
- `--color-fg`: **#14171F**
- `--color-muted`: **#5B6475**
- `--color-border`: **#DDE1E8**
- `--color-accent`: **#4F46E5**
- `--color-accent_hover`: **#4338CA**
- `--color-accent_active`: **#3730A3**
- `--color-accent_soft`: **#EEF0FF**
- `--color-focus_ring`: **#818CF8**
- `--color-status_pending_bg`: **#EEF1F5**
- `--color-status_pending_fg`: **#475066**
- `--color-status_running_bg`: **#E0ECFF**
- `--color-status_running_fg`: **#1E4FB8**
- `--color-status_done_bg`: **#DDF5E6**
- `--color-status_done_fg`: **#14683A**
- `--color-status_failed_bg`: **#FDE4E4**
- `--color-status_failed_fg`: **#A12626**
- `--color-danger`: **#B42318**
- `--color-danger_bg`: **#FEF1F0**
- `--color-warning_bg`: **#FFF6E0**
- `--color-warning_fg`: **#8A5A00**
- `--color-code_bg`: **#F1F3F7**

## Typography

- `font_family`: "Inter", system-ui, "Segoe UI", Roboto, Arial, sans-serif
- `heading_font`: "Inter", system-ui, "Segoe UI", Roboto, Arial, sans-serif
- `mono_font`: "JetBrains Mono", ui-monospace, "Cascadia Mono", Consolas, "Liberation Mono", monospace
- `heading_weight`: 600
- `body_weight`: 400
- `size_xs`: 12px
- `size_sm`: 14px
- `size_base`: 16px
- `size_lg`: 18px
- `size_xl`: 24px
- `size_2xl`: 30px
- `line_height`: 1.5
- `font_loading`: Load fonts only from the product's own origin via design/fonts/inter/font.css and design/fonts/jetbrains-mono/font.css; no CDN, no third-party font requests.
- Inter files: `design/fonts/inter/` — `font.css` holds its @font-face rules, `OFL.txt` its licence
- JetBrains Mono files: `design/fonts/jetbrains-mono/` — `font.css` holds its @font-face rules, `OFL.txt` its licence

## Spacing Scale

- `--space-0`: 4px
- `--space-1`: 8px
- `--space-2`: 12px
- `--space-3`: 16px
- `--space-4`: 24px
- `--space-5`: 32px
- `--space-6`: 48px

## Border-Radii

- `--radius-sm`: 4px
- `--radius-md`: 8px
- `--radius-lg`: 12px
- `--radius-pill`: 999px

## Components

### Button

Primary: bg=accent, fg=#FFFFFF, padding 12px 24px, radius md, font 15px/600, min-height 44px. Hover=accent_hover, active=accent_active plus translateY(1px), focus-visible=2px focus_ring outline with 2px offset, disabled opacity 0.55 with cursor not-allowed and no hover change. Loading state while submitting: label 'Wird gesendet…' and disabled. Secondary: transparent bg, 1px border, fg text, hover bg=code_bg. Full width on mobile (<640px).

### TextArea

Surface bg, 1px border, radius md, padding 12px 16px, min-height 140px, vertical resize, font 16px (no zoom on iOS). Focus: border=accent plus 3px ring accent_soft. Invalid: border=danger, error text 14px danger below. Beneath it a character counter 'n / 10000' in mono 12px muted, turning danger above 10000. Validation feedback appears only after the user typed in it or tried to submit.

### Select

Native select with the same look as TextArea: min-height 44px, radius md, 1px border, padding 0 40px 0 16px, chevron drawn with CSS. Options: 'Wörter zählen', 'Häufigste Wörter', 'Lesezeit schätzen'. Visible label above. Focus as TextArea.

### FormField

Label 14px/500 fg, 8px gap to the control, helper or error line 14px below (muted or danger), 16px gap between fields. Error line has role=alert.

### Card

bg=surface, 1px border, radius lg, padding 24px (16px on mobile), subtle shadow 0 1px 2px rgba(20,23,31,0.05). Optional header with 18px/600 title and muted subtitle.

### StatusBadge

Pill (radius pill), padding 2px 10px, 12px/600, a 6px dot before the label. Labels exactly: 'wartend' (pending_bg/fg, grey dot), 'in Arbeit' (running_bg/fg, blue pulsing dot, pulse disabled under prefers-reduced-motion), 'fertig' (done_bg/fg, green dot), 'fehlgeschlagen' (failed_bg/fg, red dot). Status is never colour-only: label text is always shown.

### JobCard

Card-like row (padding 16px 24px, 1px border, radius lg, 12px gap between rows). Header row: id in mono '#12' muted, analysis label as small neutral tag, created time right-aligned muted 12px, StatusBadge. Body: text preview in 14px fg, max 2 lines (line clamp), ellipsis after about 140 characters. Result area below with a 1px top border, 12px top padding. All user content as plain text nodes, never as HTML. Mobile: header wraps, time moves below the id.

### ResultView

Renders by analysis. word_count: big mono figure 24px/600 plus 'Wörter'. reading_time: '≈ 3 Min. Lesezeit' with muted '(600 Wörter)'. top_words: ordered list of max 5 rows, rank, word in mono, count right-aligned, thin proportional bar in accent_soft. pending/running: muted line 'Ergebnis wird berechnet…' (running) or 'Wartet auf Verarbeitung…' (pending). failed: ErrorMessage block.

### ErrorMessage

Block with bg=danger_bg, 1px border #F5C2BE, radius md, padding 12px 16px, fg danger, 14px, icon prefix. For failed jobs: shows only the short readable error text. For API unreachable: banner 'API nicht erreichbar. Es wird weiter versucht…' with role=alert.

### InfoBanner

Full-width banner inside the container, radius md, padding 12px 16px, 14px. Variants: loading (accent_soft bg, small spinner, 'Aufträge werden geladen…'), error (ErrorMessage style), warning (warning_bg/warning_fg). Spinner is disabled under prefers-reduced-motion.

### EmptyState

Centered inside a dashed-border card (1px dashed border, radius lg, padding 48px 24px): simple line icon 40px muted, title 18px/600 'Noch keine Aufträge', text 14px muted 'Erstelle oben deinen ersten Auftrag – das Ergebnis erscheint hier automatisch.'

### AppHeader

Height 64px, bg=surface, 1px bottom border. Left: logo mark 28px accent square with radius sm plus product name 'Auftragsverarbeitung' 18px/600. Right: LiveIndicator. Not sticky on mobile.

### LiveIndicator

Small text 12px muted 'Aktualisiert alle 3 s' with a 8px green dot (muted grey when API unreachable). Updates in the background without layout shift; the form never loses its input on refresh.

## Layout Principles

- Single-column page, container max-width 880px, centered, horizontal padding 24px (16px below 640px).
- Breakpoints: mobile <640px, tablet 640–1023px, desktop ≥1024px. The layout is one column everywhere; only paddings, button width and header wrapping change.
- Vertical rhythm: 32px between page sections, 12px between job rows, 16px between form fields.
- Minimum touch target 44px for all interactive controls; visible focus ring on every focusable element.
- Rendering rule: job text, results and errors are rendered only as plain text nodes; long words wrap (overflow-wrap:anywhere).
- Format for dates and times: 'TT.MM.JJJJ, HH:MM' in 24h, local time zone of the browser (e.g. '14.03.2025, 09:41'); within the last minute show 'gerade eben'.
- Format for numbers: German thousands separator '1.234'; reading time as whole minutes 'N Min.'; word counts as 'N Wörter'; job ids as '#N'.
- Animations are short (150ms) and are disabled under prefers-reduced-motion. Fonts, icons and assets are served from the own origin only (no CDN or third-party).
