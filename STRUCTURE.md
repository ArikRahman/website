# Website Structure Guide

## 📂 Complete Directory Layout

```
docs/
│
├── index.html                  # 🏠 Landing page - lists all blog posts
│                               #    Card-based design showing post previews
│
├── posts/                      # 📝 Blog posts directory
│   ├── _template.html         #    📋 Template for new posts (DO NOT MODIFY)
│   ├── 2026-02-28.html        #    📄 Example: Week of Feb 22-28, 2026
│   └── YYYY-MM-DD.html        #    📄 Future posts go here
│
├── README.org                  # 📖 Human-readable overview (Org-mode)
├── AGENTS.md                   # 🤖 Detailed AI agent instructions
├── QUICKSTART.md               # 🚀 Quick guide for adding posts
├── OVERVIEW.md                 # 📋 Project overview and guidelines
├── STRUCTURE.md                # 📁 This file - visual structure guide
│
└── new-post.sh                 # 🔧 Helper script to create new posts
```

## 🔄 Data Flow

```
../journals/                  docs/
│                             │
├── 2026-02-22.org           │
├── 2026-02-23.org           │
├── 2026-02-24.org     ──────┼──> Synthesize into narrative
├── 2026-02-25.org           │
├── 2026-02-28.org           │
│                             │
│                             ├── posts/2026-02-28.html
│                             │   (Blog post with themed content)
│                             │
│                             └── index.html
│                                 (Card linking to post)
```

## 📄 File Relationships

```
┌─────────────────────────────────────────────────────────┐
│ index.html (Landing Page)                               │
│ ┌─────────────────────────────────────────────────────┐ │
│ │ <main class="post-list">                            │ │
│ │                                                      │ │
│ │   ┌──────────────────────────────────────────┐     │ │
│ │   │ Post Card 1 (Most Recent)                │     │ │
│ │   │ href="posts/2026-03-07.html" ────────────┼─┐   │ │
│ │   └──────────────────────────────────────────┘ │   │ │
│ │                                                 │   │ │
│ │   ┌──────────────────────────────────────────┐ │   │ │
│ │   │ Post Card 2                              │ │   │ │
│ │   │ href="posts/2026-02-28.html" ────────────┼─┼─┐ │ │
│ │   └──────────────────────────────────────────┘ │ │ │ │
│ │                                                 │ │ │ │
│ └─────────────────────────────────────────────────┘ │ │ │
└─────────────────────────────────────────────────────┼─┼─┘
                                                      │ │
                ┌─────────────────────────────────────┘ │
                │                                        │
                ▼                                        ▼
  ┌──────────────────────────┐         ┌──────────────────────────┐
  │ posts/2026-03-07.html    │         │ posts/2026-02-28.html    │
  │                          │         │                          │
  │ [Blog Post Content]      │         │ [Blog Post Content]      │
  │                          │         │                          │
  │ ← Back to all posts      │         │ ← Back to all posts      │
  │   (links to index.html)  │         │   (links to index.html)  │
  └──────────────────────────┘         └──────────────────────────┘
```

## 🎨 Style Inheritance

```
All posts inherit from embedded CSS:

┌───────────────────────────┐
│ Catppuccin Mocha Theme    │
│ (CSS Custom Properties)    │
└───────────────────────────┘
            │
            ├──> index.html (Landing page styles)
            │    - .post-card
            │    - .post-list
            │    - header styles
            │
            └──> posts/*.html (Individual post styles)
                 - .blog-post
                 - .highlight-box
                 - .dream-box
                 - nav styles
```

## 🔗 Navigation Flow

```
User Journey:

1. Land on index.html
   │
   ├─> Click post card
   │   │
   │   └─> Read posts/YYYY-MM-DD.html
   │       │
   │       └─> Click "← Back to all posts"
   │           │
   │           └─> Return to index.html
   │
   └─> Click another post card
       └─> (repeat)
```

## 📝 Content Creation Flow

```
Step 1: Create Post File
┌─────────────────────────────────┐
│ ./new-post.sh 2026-03-07        │  OR  │ cp posts/_template.html    │
│                                 │      │    posts/2026-03-07.html   │
└─────────────────────────────────┘      └────────────────────────────┘
                │
                ▼
Step 2: Fill Content
┌─────────────────────────────────┐
│ Edit posts/2026-03-07.html      │
│ - Replace [TITLE]               │
│ - Replace [DATE RANGE]          │
│ - Replace [BLOG POST TITLE]     │
│ - Fill in content sections      │
└─────────────────────────────────┘
                │
                ▼
Step 3: Update Index
┌─────────────────────────────────┐
│ Edit index.html                 │
│ Add new post card at top of     │
│ <main class="post-list">        │
└─────────────────────────────────┘
                │
                ▼
Step 4: Test & Deploy
┌─────────────────────────────────┐
│ Open index.html in browser      │
│ Test navigation                 │
│ git add . && git commit         │
│ git push                        │
└─────────────────────────────────┘
```

## 🎯 Component Breakdown

### index.html Components

```
┌───────────────────────────────────────┐
│ <header>                              │
│   <h1>Journal Blog</h1>               │
│   <p>Weekly reflections...</p>        │
└───────────────────────────────────────┘

┌───────────────────────────────────────┐
│ <main class="post-list">              │
│                                       │
│   ┌─────────────────────────────┐   │
│   │ <a class="post-card">        │   │
│   │   <h2>Title</h2>             │   │
│   │   <span>Date</span>          │   │
│   │   <p>Excerpt</p>             │   │
│   │   <span>Read more</span>     │   │
│   └─────────────────────────────┘   │
│                                       │
│   (More post cards...)                │
└───────────────────────────────────────┘

┌───────────────────────────────────────┐
│ <footer>                              │
│   Links to docs and credits           │
└───────────────────────────────────────┘
```

### Individual Post Components

```
┌───────────────────────────────────────┐
│ <nav>                                 │
│   ← Back to all posts                 │
└───────────────────────────────────────┘

┌───────────────────────────────────────┐
│ <header>                              │
│   <h1>Post Title</h1>                 │
│   <p class="date">Date Range</p>      │
└───────────────────────────────────────┘

┌───────────────────────────────────────┐
│ <article class="blog-post">           │
│                                       │
│   <h2>Section</h2>                    │
│   <p>Content...</p>                   │
│                                       │
│   ┌─────────────────────────────┐   │
│   │ <div class="highlight-box">  │   │
│   │   Key insight               │   │
│   └─────────────────────────────┘   │
│                                       │
│   ┌─────────────────────────────┐   │
│   │ <div class="dream-box">      │   │
│   │   💭 Dream description      │   │
│   └─────────────────────────────┘   │
│                                       │
│   <code>inline code</code>            │
│   <strong>emphasis</strong>           │
│   <ul><li>lists</li></ul>             │
└───────────────────────────────────────┘

┌───────────────────────────────────────┐
│ <footer>                              │
│   Written from journals • Date        │
└───────────────────────────────────────┘
```

## 📦 What Each File Does

| File | Purpose | Modify? |
|------|---------|---------|
| `index.html` | Landing page listing all posts | ✅ Add new post cards |
| `posts/_template.html` | Template for new posts | ❌ Copy, don't modify |
| `posts/YYYY-MM-DD.html` | Individual blog posts | ✅ Fill with content |
| `README.org` | Human documentation | ℹ️ Reference only |
| `AGENTS.md` | AI instructions | ℹ️ Reference only |
| `QUICKSTART.md` | Quick start guide | ℹ️ Reference only |
| `OVERVIEW.md` | Project overview | ℹ️ Reference only |
| `STRUCTURE.md` | This visual guide | ℹ️ Reference only |
| `new-post.sh` | Helper script | 🔧 Run to create posts |

## 🎨 Color Scheme Usage

```
Catppuccin Mocha Palette Application:

┌─────────────┬──────────┬─────────────────────────────┐
│ Element     │ Color    │ Hex Code                   │
├─────────────┼──────────┼─────────────────────────────┤
│ Titles      │ Mauve    │ #cba6f7                    │
│ Headings    │ Blue     │ #89b4fa                    │
│ Subheadings │ Teal     │ #94e2d5                    │
│ Highlights  │ Yellow   │ #f9e2af                    │
│ Code        │ Peach    │ #fab387                    │
│ Text        │ Text     │ #cdd6f4                    │
│ Background  │ Base     │ #1e1e2e                    │
│ Cards       │ Mantle   │ #181825                    │
└─────────────┴──────────┴─────────────────────────────┘
```

## 🚀 Quick Commands

```bash
# Create new post
./new-post.sh 2026-03-07

# View structure
tree docs

# Test locally
open index.html

# Deploy to GitHub Pages
git add .
git commit -m "Add post: March 1-7, 2026"
git push
```

---

**Visual Structure Guide v1.0**  
**Last Updated**: 2026-02-28