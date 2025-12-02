# Hugo Site Structure Guide

## Overview
Your old static website has been successfully migrated to the Hugo `shifty` theme. The homepage now matches your original design with the info box, background images, and language switcher.

## Homepage
- **Location**: `themes/shifty/layouts/home.html`
- **Features**:
  - Profile info box with your name and bio
  - Links to GitHub, LinkedIn, email, and PGP key
  - Full-screen background images (different for English/Hebrew)
  - Language switcher in footer (desktop and mobile versions)

## Content Structure

### Posts/Blog Articles
Posts are stored in `content/posts/` and will be generated as individual pages.

**Example post structure:**
```markdown
---
title: "My First Post"
date: 2025-12-02
draft: false
tags: ["technology", "development"]
---

Your post content here in Markdown format.
```

**To create a new post:**
```bash
hugo new posts/my-new-post.md
```

### Regular Pages
Create standalone pages in `content/` directory:

```markdown
---
title: "About Me"
date: 2025-12-02
draft: false
---

About page content here.
```

### Multilingual Content
To create content in both languages:

**English:** `content/posts/my-post.md`
```markdown
---
title: "My Post"
---
English content
```

**Hebrew:** `content/posts/my-post.he.md`
```markdown
---
title: "הפוסט שלי"
---
תוכן בעברית
```

## Layouts for Different Page Types

### Section Layout (Post List)
**File**: `themes/shifty/layouts/section.html`
- Displays list of all posts
- Currently inherits from base template
- Can be customized to show post excerpts, dates, tags

### Single Post Layout  
**File**: `themes/shifty/layouts/page.html`
- Displays individual post content
- Can be customized with author info, date, tags, etc.

### Custom Page Types
You can create custom content types:
```bash
content/
  portfolio/
    _index.md
    project1.md
    project2.md
```

Then create matching layout:
```
themes/shifty/layouts/portfolio/
  list.html    # Lists all portfolio items
  single.html  # Individual portfolio item
```

## Styling
- **Main CSS**: `themes/shifty/assets/css/main.css`
- All your original styles are preserved
- Hugo processes CSS automatically via `head/css.html` partial

## Assets
- **Images**: `themes/shifty/static/assets/`
- **Icons**: Already migrated (hoopoe.jpg, flags, favicon)
- **PGP Key**: Accessible at `/assets/a577fd...asc`

## Next Steps to Enhance Posts

### 1. Create a Blog Section Template
Edit `themes/shifty/layouts/section.html` to display posts attractively:
```html
{{ define "main" }}
<div class="posts-container">
  <h1>{{ .Title }}</h1>
  {{ range .Pages }}
  <article class="post-preview">
    <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
    <time>{{ .Date.Format "January 2, 2006" }}</time>
    <p>{{ .Summary }}</p>
    <a href="{{ .RelPermalink }}">Read more →</a>
  </article>
  {{ end }}
</div>
{{ end }}
```

### 2. Enhance Single Post Layout
Edit `themes/shifty/layouts/page.html`:
```html
{{ define "main" }}
<article class="post-content">
  <header>
    <h1>{{ .Title }}</h1>
    <time>{{ .Date.Format "January 2, 2006" }}</time>
    {{ with .Params.tags }}
    <div class="tags">
      {{ range . }}
      <a href="{{ "tags/" | absLangURL }}{{ . | urlize }}">{{ . }}</a>
      {{ end }}
    </div>
    {{ end }}
  </header>
  {{ .Content }}
</article>
{{ end }}
```

### 3. Add CSS for Posts
Add to `themes/shifty/assets/css/main.css`:
```css
.posts-container {
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background: rgba(255,255,255,0.95);
  border-radius: 10px;
}

.post-preview {
  margin-bottom: 2rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid #ddd;
}

.post-content {
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background: rgba(255,255,255,0.95);
  border-radius: 10px;
  line-height: 1.6;
}
```

## Development Workflow

**Start dev server:**
```bash
hugo serve -D
```

**Build for production:**
```bash
hugo
```

**Create new content:**
```bash
hugo new posts/post-title.md
hugo new posts/post-title.he.md  # Hebrew version
```

## File Organization

```
/workspaces/shift1w/
├── hugo.toml                 # Main config (multilingual settings)
├── content/                  # Your content files (Markdown)
│   └── posts/               # Blog posts
├── themes/shifty/           # Your theme
│   ├── layouts/
│   │   ├── baseof.html      # Base template
│   │   ├── home.html        # Homepage (matches deprecated)
│   │   ├── page.html        # Single page template
│   │   ├── section.html     # List template (e.g., all posts)
│   │   └── _partials/
│   │       ├── head.html
│   │       ├── footer.html  # Language switcher + copyright
│   │       └── head/
│   │           └── css.html
│   ├── assets/css/
│   │   └── main.css         # Your original styles
│   ├── static/assets/       # Images, icons, files
│   └── i18n/
│       ├── en.toml          # English translations
│       └── he.toml          # Hebrew translations
└── public/                  # Generated site (deploy this)
```

## Key Features Implemented

✅ Homepage matches original design exactly
✅ Multilingual support (English/Hebrew)
✅ Language switcher with flags
✅ Background images per language
✅ Profile info box with links
✅ Responsive design (mobile/desktop)
✅ All assets migrated
✅ Hugo theme structure ready for posts

## Resources
- [Hugo Documentation](https://gohugo.io/documentation/)
- [Multilingual Mode](https://gohugo.io/content-management/multilingual/)
- [Content Organization](https://gohugo.io/content-management/organization/)
- [Page Bundles](https://gohugo.io/content-management/page-bundles/)
