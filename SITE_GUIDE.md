# Site Guide — shadowscythe03.github.io

Quick reference for adding content, embedding media, and managing site visibility.

---

## 1. Embedding PDFs

PDFs must be publicly hosted. The pattern uses Google Docs Viewer so the PDF renders inline without a download prompt.

### Step 1 — Convert your GitHub blob URL to a raw URL

```
Blob (won't work in iframe):
  https://github.com/shadowscythe03/projects/blob/main/folder/file.pdf

Raw (use this):
  https://raw.githubusercontent.com/shadowscythe03/projects/main/folder/file.pdf
```

Just replace `github.com` → `raw.githubusercontent.com` and remove `/blob`.

### Step 2 — Paste this block into your project markdown

```html
<iframe
  src="https://docs.google.com/viewer?url=RAW_PDF_URL&embedded=true"
  width="100%"
  height="850px"
  style="border: 1px solid #e5e7eb; border-radius: 8px; display: block; margin: 1rem 0;">
</iframe>

[Download PDF](RAW_PDF_URL)
```

Replace `RAW_PDF_URL` in both places. Done.

---

## 2. Embedding Videos

### Option A — GitHub-hosted video (for files under ~25 MB)

Same blob → raw URL conversion as PDFs, then:

```html
<video width="100%" controls style="border-radius: 8px; margin: 1rem 0;">
  <source src="RAW_VIDEO_URL" type="video/mp4">
  Your browser does not support the video tag.
</video>
```

### Option B — YouTube (recommended for large or important videos)

Upload to YouTube (can be **unlisted** if you don't want it publicly searchable), then use Hugo's built-in shortcode — one line, no HTML needed:

```
{{</* youtube VIDEO_ID */>}}
```

The video ID is the part after `?v=` in the YouTube URL, e.g. `https://youtu.be/dQw4w9WgXcQ` → ID is `dQw4w9WgXcQ`.

> **Why YouTube over GitHub for large videos?** GitHub raw URLs don't support byte-range requests, so large videos can't seek and may stall. YouTube handles all of that automatically.

---

## 3. Writing a Blog Post

### Create the file

Each post lives in its own folder under `content/blog/`:

```
content/
  blog/
    my-post-title/
      index.md        ← your post
      featured.jpg    ← optional cover image (rename to featured.*)
```

### Front matter template

Paste this at the top of every `index.md`:

```yaml
---
title: 'Your Post Title Here'
date: 2026-05-22          # publication date (YYYY-MM-DD)
summary: 'One sentence describing the post — shown on the blog listing page.'
tags:
  - Tag One
  - Tag Two
image:
  caption: ''
  focal_point: ''
  preview_only: false     # set true if you only want the image inside the post, not on the card
---
```

### Markdown cheatsheet for posts

```markdown
## Section heading

### Sub-heading

**bold text**   *italic text*   `inline code`

> Blockquote for highlights or quotes

- Bullet list item
- Another item

1. Numbered list
2. Second item

[Link text](https://example.com)

![Alt text](image.png)          ← image in same folder as index.md

---                             ← horizontal rule / divider
```

### Code blocks

````markdown
```python
def hello():
    print("Hello, world!")
```
````

Supported language hints: `python`, `bash`, `javascript`, `json`, `yaml`, `markdown`, etc.

---

## 4. Adding a New Project

### Create the folder and file

```
content/
  projects/
    my-project-name/
      index.md
      featured.jpg    ← optional thumbnail
```

### Front matter template

```yaml
---
title: 'Project Title'
summary: 'One-sentence description shown on the project card.'
date: 2025-01-01
authors:
  - admin
tags:
  - Deep Learning
  - NLP
image:
  caption: ''
  focal_point: ''
  preview_only: false
url_code: 'https://github.com/your/repo'
links:
  - icon: brands/github
    name: GitHub
    url: 'https://github.com/your/repo'
---

Your project content in markdown here.
```

---

## 5. Updating Your Profile

All profile data lives in one file: `content/authors/admin/_index.md`

| What to change | Field |
| --- | --- |
| Bio paragraph | Bottom of the file, below the `---` |
| Role/tagline | `role:` |
| Work experience | `work:` list |
| Education | `education:` list |
| Skills | `skills:` list |
| Awards | `awards:` list |
| Social links | `profiles:` list |

To add a new work entry, copy an existing block under `work:` and update the fields. Leave `date_end: ''` for a current/ongoing role.

---

## 6. Site Indexing & Search Visibility

Your site already has a sitemap and robots.txt generated automatically by Hugo. You just need to submit it to search engines once.

### Google Search Console (most important)

1. Go to **[search.google.com/search-console](https://search.google.com/search-console/)**
2. Click **Add property** → choose **URL prefix** → enter `https://shadowscythe03.github.io/`
3. **Verify ownership** — choose the **HTML file** method:
   - Google gives you a file like `googleXXXXXXXX.html`
   - Drop that file into your `static/` folder in this repo
   - Push to GitHub (it will be served at `https://shadowscythe03.github.io/googleXXXXXXXX.html`)
   - Click **Verify** in Search Console
4. Go to **Sitemaps** → add `sitemap.xml` → click **Submit**
5. Done. Google will start crawling within a few days. Check back in ~1 week to see indexed pages.

### Bing Webmaster Tools (optional but quick)

1. Go to **[bing.com/webmasters](https://www.bing.com/webmasters/)**
2. Sign in with a Microsoft account
3. Add your site → verify the same way (HTML file in `static/`)
4. Submit sitemap: `https://shadowscythe03.github.io/sitemap.xml`

### What the sitemap URL is

```
https://shadowscythe03.github.io/sitemap.xml
```

Hugo generates this automatically on every build — you never have to touch it.

### Social sharing / Open Graph

Hugo Blox automatically generates Open Graph and Twitter Card meta tags from your post title, summary, and featured image. No extra configuration needed. If you want a specific image to appear when sharing a link, name it `featured.jpg` (or `.png`) in the post/project folder.

---

## 7. Quick Reference — File Locations

| What | File |
| --- | --- |
| Site title, base URL | `config/_default/hugo.yaml` |
| Navigation menu | `config/_default/menus.yaml` |
| Theme color, search, footer | `config/_default/params.yaml` |
| Homepage layout | `content/_index.md` |
| Your profile & bio | `content/authors/admin/_index.md` |
| Experience page | `content/experience.md` |
| Blog landing | `content/blog/_index.md` |
| Projects landing | `content/projects/` |
| Coursework page | `content/courses/_index.md` |
| Resume PDF | `static/uploads/resume.pdf` |
