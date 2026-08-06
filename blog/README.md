# How to add a new blog post

Plain-English instructions. No build tools, no npm, no terminal required —
just copying a folder and editing text.

---

## How the blog is put together

```
website/
├── index.html                  ← the homepage (do NOT restyle; Apple reviews it)
├── sitemap.xml                 ← list of pages for Google
├── robots.txt                  ← points Google at the sitemap
└── blog/
    ├── index.html              ← the blog LISTING page (the list of posts)
    ├── blog.css                ← ALL blog styling lives here, shared by every post
    ├── README.md               ← this file
    └── why-learn-ancient-greek-odyssey/
        └── index.html          ← post #1
```

Two rules that make this work:

1. **Each post is a folder containing one `index.html`.** The folder name
   becomes the web address. `why-learn-ancient-greek-odyssey/` is served at
   `atticgreek.com/blog/why-learn-ancient-greek-odyssey` — clean, no `.html`
   on the end.
2. **You never edit `blog.css`.** All colours, fonts and spacing are already
   in there. New posts pick it up automatically and look correct.

---

## Adding post #2 — five steps

### Step 1 — Copy the post folder

Duplicate the folder `why-learn-ancient-greek-odyssey` and rename the copy to
your new post's web address. Use lowercase words separated by hyphens, and put
the main search phrase in it:

- Good: `how-to-read-the-greek-alphabet`
- Good: `what-is-koine-greek`
- Bad: `Post 2` (spaces and capitals break URLs)

### Step 2 — Edit the top of the new `index.html`

Open the copied `index.html`. Everything between `<head>` and `</head>` is
information for Google — not visible on the page. Change these:

| What to change | Where | Notes |
|---|---|---|
| `<title>` | line ~7 | Keep under 60 characters |
| `<meta name="description">` | line ~8 | Keep under 155 characters |
| `<link rel="canonical">` | line ~9 | Must match the new folder name exactly |
| `og:title`, `og:description`, `og:url` | ~lines 15–22 | The Facebook/LinkedIn preview |
| `twitter:title`, `twitter:description` | ~lines 30–33 | The X/Twitter preview |
| `article:published_time` | ~line 26 | Format: `2026-09-14` |

### Step 3 — Update the structured data

Still in `<head>`, there are boxes starting with
`<script type="application/ld+json">`. These are what let Google and AI
assistants quote your article directly. Update:

- **Article block** — `headline`, `description`, `mainEntityOfPage`,
  `datePublished`, `dateModified`
- **FAQPage block** — replace the four questions and answers so they match
  your new article's question-headings. *Every question here must genuinely
  be answered in the article text.* Google penalises FAQ markup that doesn't
  match the visible page.
- **BreadcrumbList block** — update the last `name`

If you delete the FAQ block entirely that's fine too; the page still works.

### Step 4 — Write the article

In the body, replace the `<h1>` and everything inside `<article>`. The pieces
you have to work with:

```html
<!-- Opening paragraph, slightly larger -->
<p class="lead">Your first paragraph.</p>

<!-- Normal paragraph -->
<p>Ordinary text.</p>

<!-- Section heading. Phrase it as a QUESTION people would search. -->
<h2 id="short-name-here">Why does word order matter<span class="qmark">?</span></h2>

<!-- Greek word inside a sentence -->
the word <span class="gk" lang="grc">λόγος</span> means...

<!-- A Greek quote block -->
<blockquote class="greek-quote">
  <p class="gk-text" lang="grc">Greek text goes here.</p>
  <p class="gk-trans">Your English translation.</p>
  <cite>Author, Work 1.1</cite>
</blockquote>
```

Rules that keep the SEO working:

- **Exactly one `<h1>` per page.** It's the article title. Never add a second.
- **Section headings are `<h2>`.** Don't skip to `<h3>` or use `<h2>` for
  decoration.
- **Always include `lang="grc"`** on Greek text. It tells screen readers and
  Google the language is Ancient Greek.
- **Keep the CTA section at the bottom** so every post ends with a trial offer.

### Step 5 — Add it to the two lists

**a) The blog listing page** — open `blog/index.html`, find the comment
`<!-- ── POST 1 ── -->`, copy the whole `<a class="post-card">...</a>` block,
and paste your new one **above** it so newest appears first. Change the
`href`, the date, the title and the excerpt.

Then scroll up to the `"blogPost"` list in the structured data near the top
and add a matching entry.

**b) The sitemap** — open `sitemap.xml` in the main website folder and add:

```xml
<url>
  <loc>https://www.atticgreek.com/blog/YOUR-NEW-FOLDER-NAME/</loc>
  <lastmod>2026-09-14</lastmod>
  <changefreq>yearly</changefreq>
  <priority>0.7</priority>
</url>
```

Done. Upload and it's live.

---

## Checking your work before you publish

1. **Open the file in a browser** (double-click it) and read it top to bottom.
2. **Resize the window narrow** to check it works on a phone.
3. **Validate the structured data** — paste the live URL into
   <https://search.google.com/test/rich-results>. It will tell you if the
   FAQ and Article boxes are correct.
4. **Check the Greek renders correctly** — polytonic accents and breathings
   (ἄ, ὥ, ῳ) should all be visible and properly positioned.

---

## Outstanding items for the site

Small things that aren't blog-specific but affect these pages:

- **`logo.png` doesn't exist yet.** The structured data references
  `https://www.atticgreek.com/logo.png` for the publisher logo. Add a square
  PNG (at least 112×112, ideally 512×512) at the site root, or Google will
  flag a warning.
- **Social share image.** Both blog pages currently use a phone screenshot
  for `og:image`. A purpose-built 1200×630 image would look far better in
  link previews. Replace the `og:image` and `twitter:image` URLs when ready.
- **App Store link.** The post's call-to-action currently points at
  `/#pricing` because the app is still in Apple review. Once it's approved,
  search the post for `WHEN APPLE APPROVES` and swap in the real
  `https://apps.apple.com/...` URL.
- **Readings count.** The homepage says "30 authentic readings" in some
  places and "45" in others. Worth settling before you drive blog traffic to it.
