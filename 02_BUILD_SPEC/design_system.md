# Design System

Chef's Console uses **ShadCN UI** + **Tailwind CSS 4** with CSS variables defined in `frontend/src/app/globals.css`.

## Typography

| Token | Value |
|-------|-------|
| `--font-sans` | Geist Sans (via Next.js font) |
| `--font-mono` | Geist Mono |

## Color tokens (light mode)

Defined as CSS variables in `:root`:

| Token | Usage |
|-------|-------|
| `--background` / `--foreground` | Page base |
| `--primary` / `--primary-foreground` | Primary actions, brand |
| `--secondary` | Secondary buttons |
| `--muted` / `--muted-foreground` | Subtle text, disabled |
| `--destructive` | Delete, error states |
| `--border` / `--input` / `--ring` | Form controls, focus rings |
| `--card` / `--card-foreground` | Card surfaces |
| `--sidebar-*` | Dashboard sidebar theme |
| `--chart-1` … `--chart-5` | Dashboard charts |

Dark mode: `.dark` class overrides same tokens.

## Radius

| Token | Value |
|-------|-------|
| `--radius` | Base border radius |
| `--radius-sm` | calc(var(--radius) - 4px) |
| `--radius-md` | calc(var(--radius) - 2px) |
| `--radius-lg` | var(--radius) |

## Component patterns

### Buttons
- Primary action: `<Button>` default variant
- Destructive: `variant="destructive"` for delete
- Ghost: table row actions

### Tables
- Data tables use ShadCN `Table` with sortable headers
- Inline edit: row expands or dialog — bookings use inline pattern

### Forms
- React Hook Form + Zod validation
- Error text below field in `--destructive` color

### Dialogs
- Create/edit modals: `Dialog` component
- AI extract: full-width dialog with textarea + preview fields

### Status badges

| Domain | Values | Color convention |
|--------|--------|------------------|
| Enquiry status | new, read, replied, approved, rejected, closed | new=blue, approved=green, rejected=red |
| Booking status | pending, confirmed, cancelled, completed | confirmed=green, cancelled=muted |
| Payment | pending, paid, partial, refunded | paid=green, pending=amber |

Implement via `<Badge variant="...">` — map in domain components, not inline hex.

## Layout

| Area | Pattern |
|------|---------|
| Dashboard | Fixed sidebar + scrollable main |
| Marketing | Full-width sections, max-w container |
| Mobile | Sidebar collapses to sheet (verify per page) |

## Icons

Lucide React (`lucide-react`) — consistent stroke icons in nav and actions.

## Do / don't

| Do | Don't |
|----|-------|
| Use CSS variables for colors | Hardcode `#hex` in components |
| Reuse `components/ui/*` | Copy-paste Radix primitives |
| Match spacing scale (Tailwind) | Arbitrary pixel margins |
| Keep invoice PDF styles separate | Mix print CSS into globals |

## Admin app

Admin panel (`admin/`) shares ShadCN + Tailwind setup with simplified palette — no sidebar chart tokens required.
