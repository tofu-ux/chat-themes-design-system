# Design System for ChatThemes

> The definitive design system specification for ChatThemes — a theming platform for chat interfaces.

---

## 1. Foundation

### 1.1 Design Principles

- **Expressive** — Users should feel ownership over their chat experience through rich customization.
- **Accessible** — All themes must meet WCAG 2.1 AA contrast requirements by default.
- **Consistent** — Shared tokens and components ensure a cohesive feel across all themes.
- **Performant** — Themes load instantly; no layout shifts, no flash of unstyled content.

### 1.2 Brand

- **Name:** ChatThemes
- **Tagline:** *Your chat, your style.*
- **Voice:** Friendly, concise, playful but not childish.

---

## 2. Color System

### 2.1 Semantic Tokens

All colors are defined as semantic tokens, not raw values. Themes override these tokens.

| Token                     | Role                          | Light Default   | Dark Default    |
|---------------------------|-------------------------------|-----------------|-----------------|
| `--color-bg-primary`      | Main background               | `#FFFFFF`       | `#1A1A2E`       |
| `--color-bg-secondary`    | Sidebar / panels              | `#F5F5F7`       | `#16213E`       |
| `--color-bg-chat`         | Chat message area             | `#FAFAFA`       | `#0F3460`       |
| `--color-surface`         | Cards, modals, popovers       | `#FFFFFF`       | `#1A1A2E`       |
| `--color-text-primary`    | Body text                     | `#1C1C1E`       | `#E4E4E7`       |
| `--color-text-secondary`  | Muted / helper text           | `#6B7280`       | `#9CA3AF`       |
| `--color-text-inverse`    | Text on accent backgrounds    | `#FFFFFF`       | `#FFFFFF`       |
| `--color-accent`          | Primary action / links         | `#6366F1`       | `#818CF8`       |
| `--color-accent-hover`    | Accent hover state            | `#4F46E5`       | `#6366F1`       |
| `--color-border`          | Dividers, input borders       | `#E5E7EB`       | `#374151`       |
| `--color-message-sent`    | Sent message bubble           | `#6366F1`       | `#4F46E5`       |
| `--color-message-received`| Received message bubble       | `#F3F4F6`       | `#1F2937`       |
| `--color-status-online`   | Online indicator              | `#22C55E`       | `#22C55E`       |
| `--color-status-away`     | Away indicator                | `#F59E0B`       | `#F59E0B`       |
| `--color-status-offline`  | Offline indicator             | `#9CA3AF`       | `#6B7280`       |
| `--color-error`           | Error states                  | `#EF4444`       | `#F87171`       |
| `--color-success`         | Success states                | `#22C55E`       | `#4ADE80`       |

### 2.2 Theme Structure

A theme is a JSON object that overrides any subset of semantic tokens:

```json
{
  "id": "midnight-indigo",
  "name": "Midnight Indigo",
  "author": "chatthemes",
  "mode": "dark",
  "tokens": {
    "color-bg-primary": "#0D0D1A",
    "color-accent": "#7C3AED"
  }
}
```

---

## 3. Typography

### 3.1 Type Scale

| Token               | Size   | Weight | Line Height | Usage                    |
|----------------------|--------|--------|-------------|--------------------------|
| `--type-display`     | 32px   | 700    | 1.2         | Hero / onboarding        |
| `--type-heading-1`   | 24px   | 600    | 1.3         | Page titles              |
| `--type-heading-2`   | 18px   | 600    | 1.3         | Section headers          |
| `--type-body`        | 15px   | 400    | 1.5         | Chat messages, body text |
| `--type-body-small`  | 13px   | 400    | 1.4         | Timestamps, metadata     |
| `--type-caption`     | 11px   | 500    | 1.3         | Badges, labels           |

### 3.2 Font Stack

```
--font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', monospace;
```

---

## 4. Spacing & Layout

### 4.1 Spacing Scale (4px base)

| Token        | Value |
|--------------|-------|
| `--space-1`  | 4px   |
| `--space-2`  | 8px   |
| `--space-3`  | 12px  |
| `--space-4`  | 16px  |
| `--space-5`  | 24px  |
| `--space-6`  | 32px  |
| `--space-7`  | 48px  |
| `--space-8`  | 64px  |

### 4.2 Border Radius

| Token              | Value | Usage                  |
|--------------------|-------|------------------------|
| `--radius-sm`      | 4px   | Inputs, small elements |
| `--radius-md`      | 8px   | Cards, panels          |
| `--radius-lg`      | 16px  | Message bubbles        |
| `--radius-full`    | 9999px| Avatars, pills         |

### 4.3 Shadows

| Token              | Value                                    | Usage           |
|--------------------|------------------------------------------|-----------------|
| `--shadow-sm`      | `0 1px 2px rgba(0,0,0,0.05)`            | Subtle lift     |
| `--shadow-md`      | `0 4px 12px rgba(0,0,0,0.1)`            | Cards, dropdowns|
| `--shadow-lg`      | `0 12px 32px rgba(0,0,0,0.15)`          | Modals, dialogs |

---

## 5. Components

### 5.1 Message Bubble

```
┌─────────────────────────────────┐
│  Avatar  Name        Timestamp  │
│          ┌───────────────────┐  │
│          │ Message content   │  │
│          │                   │  │
│          └───────────────────┘  │
│          Reactions              │
└─────────────────────────────────┘
```

- Sent: `--color-message-sent` bg, `--color-text-inverse` text, aligned right
- Received: `--color-message-received` bg, `--color-text-primary` text, aligned left
- Border radius: `--radius-lg` with tail corner at `--radius-sm`
- Padding: `--space-3` horizontal, `--space-2` vertical
- Max width: 70% of chat area

### 5.2 Avatar

- Sizes: `24px` (inline), `32px` (message), `40px` (profile), `64px` (settings)
- Shape: `--radius-full`
- Fallback: initials on `--color-accent` background
- Status dot: 10px circle, bottom-right, `2px` white border

### 5.3 Input Bar

- Height: 48px minimum, auto-expands to 160px max
- Background: `--color-surface`
- Border: `1px solid --color-border`, `--radius-md`
- Focus: `2px solid --color-accent` ring
- Includes: attachment button, emoji picker, send button

### 5.4 Sidebar / Channel List

- Width: 260px default, collapsible to 64px (icons only)
- Background: `--color-bg-secondary`
- Active channel: `--color-accent` left border + `--color-accent/10` fill
- Hover: `--color-border` background

### 5.5 Button

| Variant   | Background          | Text                  | Border             |
|-----------|---------------------|-----------------------|--------------------|
| Primary   | `--color-accent`    | `--color-text-inverse`| none               |
| Secondary | transparent         | `--color-accent`      | `--color-accent`   |
| Ghost     | transparent         | `--color-text-primary`| none               |
| Danger    | `--color-error`     | `--color-text-inverse`| none               |

- Sizes: `sm` (32px), `md` (40px), `lg` (48px)
- Border radius: `--radius-sm`
- Disabled: 50% opacity, no pointer events

### 5.6 Badge / Unread Count

- Background: `--color-accent` (or `--color-error` for mentions)
- Text: `--color-text-inverse`, `--type-caption`
- Shape: `--radius-full`, min-width 20px
- Padding: `--space-1` horizontal

### 5.7 Modal / Dialog

- Background: `--color-surface`
- Shadow: `--shadow-lg`
- Border radius: `--radius-md`
- Overlay: `rgba(0,0,0,0.5)`
- Max width: 480px, centered
- Padding: `--space-6`

### 5.8 Toast / Notification

- Position: top-right, stacked
- Background: `--color-surface`
- Shadow: `--shadow-md`
- Auto-dismiss: 5s default
- Variants: info, success, error, warning

---

## 6. Motion

| Token                  | Value                  | Usage                  |
|------------------------|------------------------|------------------------|
| `--duration-fast`      | 100ms                  | Hover states, toggles  |
| `--duration-normal`    | 200ms                  | Panel transitions      |
| `--duration-slow`      | 350ms                  | Modal enter/exit       |
| `--easing-default`     | `cubic-bezier(0.4, 0, 0.2, 1)` | General purpose |
| `--easing-bounce`      | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Playful elements |

- Respect `prefers-reduced-motion` — collapse all durations to 0ms.

---

## 7. Iconography

- Style: Outlined, 1.5px stroke, rounded caps
- Sizes: 16px, 20px, 24px
- Recommended set: Lucide Icons (consistent with outlined style)
- Color: inherits `currentColor`

---

## 8. Accessibility

- All interactive elements must have visible focus indicators (`--color-accent` ring).
- Minimum touch target: 44x44px on mobile.
- Color contrast: 4.5:1 for normal text, 3:1 for large text (18px+ bold or 24px+).
- Themes that fail contrast checks display a warning badge in the theme picker.
- Screen reader announcements for new messages, typing indicators, and status changes.

---

## 9. Responsive Breakpoints

| Token        | Value   | Layout                             |
|--------------|---------|------------------------------------|
| `--bp-mobile`| < 640px | Sidebar hidden, full-width chat    |
| `--bp-tablet`| 640–1024px | Collapsible sidebar             |
| `--bp-desktop`| > 1024px | Sidebar + chat + optional panel |

---

## 10. Theme Authoring Guide

### Creating a theme

1. Start from the base token set (Section 2.1).
2. Override only the tokens you want to change.
3. Set `mode` to `"light"` or `"dark"` — this controls which defaults are used for un-overridden tokens.
4. Test against the contrast checker (built into the theme editor).
5. Export as `.chattheme.json`.

### Theme file structure

```
themes/
  midnight-indigo.chattheme.json
  ocean-breeze.chattheme.json
  custom/
    user-theme.chattheme.json
```

### Validation rules

- All overridden color tokens must be valid hex, rgb, or hsl values.
- `mode` must be `"light"` or `"dark"`.
- `id` must be lowercase, kebab-case, unique.
- `name` max 32 characters.

---

## 11. File & Asset Naming

| Type          | Convention                        | Example                    |
|---------------|-----------------------------------|----------------------------|
| Theme files   | `kebab-case.chattheme.json`       | `sunset-glow.chattheme.json` |
| Components    | `PascalCase.tsx`                  | `MessageBubble.tsx`        |
| Tokens        | `kebab-case` CSS custom properties| `--color-bg-primary`       |
| Icons         | `kebab-case.svg`                  | `send-message.svg`         |
| Images        | `kebab-case-[size].png`           | `avatar-placeholder-64.png`|

---

*This document is the single source of truth for the ChatThemes design system. The corresponding Figma file should mirror these specifications exactly.*

*Figma file name: **ChatThemes Design System***
