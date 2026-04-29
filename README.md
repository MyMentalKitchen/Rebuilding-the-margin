# Rebuilding the Margin — Landing Pages

Static HTML landing pages for the Rebuilding the Margin webinar and programme. Pages are deployed via GoHighLevel (GHL) Custom Code elements; the GHL funnel wraps each page in its own `<html>`/`<head>`/`<body>` shell.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Essay landing page |
| `webinar.html` | Original webinar registration page |
| `webinar-alt.html` | **Canonical source** — current webinar registration page (long-form scroll variant) |
| `webinar-alt-ghl-paste.html` | Derived from `webinar-alt.html` — paste-ready for the GHL Custom Code element |
| `webinar-confirmation.html` | **Canonical source** — post-registration thank-you page |
| `webinar-confirmation-ghl-paste.html` | Derived from `webinar-confirmation.html` — paste-ready for GHL |
| `thank-you.html` | **Canonical source** — essay-funnel thank-you page (after essay signup) |
| `thank-you-ghl-paste.html` | Derived from `thank-you.html` — paste-ready for GHL |
| `programme.html` | Programme details page |

## ⚠️ Keep these pairs in sync

Three pairs of files must move together:

- **`webinar-alt.html`** ↔ **`webinar-alt-ghl-paste.html`** (webinar registration page)
- **`webinar-confirmation.html`** ↔ **`webinar-confirmation-ghl-paste.html`** (webinar thank-you page)
- **`thank-you.html`** ↔ **`thank-you-ghl-paste.html`** (essay thank-you page)

In each pair:
- The first file is the standalone, browser-previewable version (full document with `<!DOCTYPE>`, `<head>`, etc.)
- The second is the same content stripped of document scaffolding (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`) and inline `<title>` / `<meta description>` — those are owned by GHL's SEO panel.

When you edit content, layout, or styles, update **both files of the affected pair in the same commit**. If only the paste version changes (e.g. a GHL-specific tweak), note it explicitly in the commit message so the divergence is intentional and visible.

The session date (`Wed, 14 May`) appears on both the registration page (hero block + reminder section) and the confirmation page (`<dl>`). When the date changes, search across all four files.

## Local preview

```bash
python3 -m http.server 8765
# then open http://localhost:8765/webinar-alt.html
```

Note: the registration form iframe loads from `link.timclements.com` — it may render or behave slightly differently on `localhost` than in production. Layout above and below the form is fully accurate.

## Deploying changes to GHL

1. Edit `webinar-alt.html` (and mirror to `webinar-alt-ghl-paste.html`)
2. Copy the entire contents of `webinar-alt-ghl-paste.html`
3. In the GHL Funnel editor → webinar page → Custom Code element → paste over existing
4. Save → **Publish** (Save alone leaves it in draft)
5. Hard-refresh the live URL (Cmd+Shift+R) to confirm

## SEO meta

Title, meta description, OG image, and favicon are set in the GHL Page SEO panel — **not** in the HTML files. Do not paste a `<title>` or `<meta name="description">` into the Custom Code element; you'll create a duplicate `<head>` that crawlers won't honour.
