# AGENTS.md

## Purpose

This document provides instructions for AI agents working on this website. It
defines the structure, conventions, and tasks that should be followed when
maintaining or extending this project.

## Project Overview

A static single-page blog that transforms personal journal entries (Org-mode)
into narrative blog posts. Posts are authored as plain ClojureScript data maps;
[Reagent](https://reagent-project.github.io/) (a React wrapper) renders them
client-side. The site uses the Catppuccin Mocha colour scheme and is deployed
via GitHub Pages.

## Technology Stack

| Layer       | Technology                        |
|-------------|-----------------------------------|
| Language    | ClojureScript                     |
| UI          | Reagent (React wrapper)           |
| Build       | shadow-cljs                       |
| Routing     | Custom hash-based (no extra deps) |
| Styling     | Plain CSS — Catppuccin Mocha      |
| Hosting     | GitHub Pages (`/docs` folder)     |

## File Structure

```
PKM/
├── src/
│   └── blog/
│       ├── core.cljs      # Entry point — mounts Reagent app
│       ├── router.cljs    # Hash-based client-side router
│       ├── views.cljs     # Reagent page components
│       └── data.cljs      # ALL post content (plain Clojure maps)
├── docs/                  # Served by GitHub Pages
│   ├── index.html         # Minimal HTML shell — just loads JS + CSS
│   ├── css/
│   │   └── style.css      # Unified Catppuccin stylesheet
│   ├── js/
│   │   └── main.js        # Compiled output (generated — do NOT hand-edit)
│   └── new-post.sh        # Prints a data.cljs stub for a new post
├── shadow-cljs.edn        # Build configuration
└── package.json           # bun dependencies
```

## Source Data

- **Journal location**: `../journals/`
- **Format**: Org-mode files (`.org`)
- **Naming**: `YYYY-MM-DD.org` or `YYYY_MM_DD.org`
- **Date range**: Process the most recent 7 days

---

## How Posts Work

Posts are **not** separate HTML files. Every post is a Clojure map inside the
`posts` vector in `src/blog/data.cljs`.

### Post Map Shape

```clojure
{:id         "2026-03-07"          ; YYYY-MM-DD — used as the URL fragment key
 :title      "Post Title"
 :date-range "March 1-7, 2026"     ; shown under the header
 :month-year "March 2026"          ; shown in the post footer
 :excerpt    "2-3 sentence blurb shown on the index card."
 :content
 [                                  ; vector of Reagent/hiccup vectors
  [:p "Opening paragraph..."]
  [:h2 "Section"]
  [:p "Body text."]]}
```

### URL Scheme

| URL fragment        | View shown          |
|---------------------|---------------------|
| `#/` (or empty)     | Index (post list)   |
| `#/posts/2026-03-07`| Post with that id   |

### Post Ordering

`data/all-posts` sorts by `:id` (string descending) — newest first.  
You may append new maps **anywhere** in the `posts` vector; ordering is
handled automatically.

---

## Content Processing Guidelines
~clj -M -e "(doseq [f (file-seq (clojure.java.io/file \"src\"))] (when (.endsWith (str f) \".cljs\") (try (read-string (str \"(do \" (slurp f) \")\")) (println \"OK:\" f) (catch Exception e (println \"ERR:\" f \"-\" (.getMessage e))))))"~
* It walks every `.cljs` file under `src/`, tries to `read-string` the whole thing, and prints `OK` or `ERR` with the message. From now on I'll run this after every edit before handing things back to you.

### 1. Reading Journal Entries

- Identify the current date; find all journal files from the past 7 days.
- Parse Org-mode syntax:
  - `* TODO` / `* DONE` / `* WAIT` — task items
  - `[[id:...][Dreams]]` or `Dreams` tag — dream entries
  - Regular `*` bullets — general notes and reflections

### 2. Synthesis Strategy

- **Group by theme**, not chronologically.
- Typical sections: Career/Professional, Technical Projects,
  Personal Growth, Dreams, World Events.
- Write in **first person**, conversational but thoughtful.
- Provide brief context for tools and technical references.
- Keep the authentic, self-aware voice.
- Surface key insights in `highlight-box` elements.

### 3. Content Balance

- ~40% Technical / Career
- ~30% Personal reflections
- ~20% Project planning
- ~10% Dreams / philosophy / world events

---

## Hiccup Authoring Reference

`:content` is a vector of [Reagent hiccup](https://github.com/reagent-project/reagent)
vectors that are spliced directly into `<article class="blog-post">`.

### Available Elements

| Hiccup                              | Renders as                          |
|-------------------------------------|-------------------------------------|
| `[:p "..."]`                        | Body paragraph                      |
| `[:h2 "..."]`                       | Blue section header                 |
| `[:h3 "..."]`                       | Teal subsection header              |
| `[:ul [:li "..."] ...]`             | Bulleted list (mauve markers)       |
| `[:ol [:li "..."] ...]`             | Numbered list                       |
| `[:code "..."]`                     | Inline peach monospace              |
| `[:strong "..."]`                   | Peach bold emphasis                 |
| `[:em "..."]`                       | Lavender italic                     |
| `[:div.highlight-box [:p ...]]`     | Yellow left-border insight box      |
| `[:div.dream-box [:p ...]]`         | Mauve left-border dream box         |
| `[:a {:href "..."} "..."]`          | Inline link (blue, hover→mauve)     |

### Mixed Inline Content

To mix text and inline elements inside a paragraph, use a vector of strings
and child vectors:

```clojure
[:p "Planning to use " [:code "kanata"] " for the layout transition."]
```

```clojure
[:p "The concept of " [:strong "\"locality of behavior\""]
    " changed how I think about code structure."]
```

### Highlight Box

```clojure
[:div.highlight-box
 [:p [:strong "Key insight:"] " Never regret conversation."]]
```

### Dream Box

```clojure
[:div.dream-box
 [:p "I was in a prison but realised the constraint itself gave life meaning."]]
```

The `::before` pseudo-element adds the 💭 emoji automatically via CSS.

### Special Characters in Strings

Use Unicode escape sequences or literal characters — **not** HTML entities:

| Character | Use in ClojureScript strings |
|-----------|------------------------------|
| `—`       | `\u2014` or paste literal    |
| `"`       | `\"`  (escaped double-quote) |
| `'`       | `'`   (no escaping needed)   |

---

## Creating a New Post — Step by Step

### Step 1 — Run the scaffold script

```bash
cd docs
./new-post.sh 2026-03-07
```

Copy the printed map stub.

### Step 2 — Add to data.cljs

Open `src/blog/data.cljs` and paste the map as the last element of the
`posts` vector (before the closing `]`):

```clojure
(def posts
  [;; ... existing posts ...
   {:id         "2026-03-07"
    :title      "[Your Title]"
    ;; ...
    :content [...]}])
```

### Step 3 — Fill in content

Replace every `[bracketed]` placeholder. Write `:content` as a vector of
hiccup vectors following the authoring reference above.

### Step 4 — Build

```bash
# Development (hot-reload at http://localhost:3000)
bun run dev

# Production release
bun run build
```

### Step 5 — Commit

```bash
git add src/blog/data.cljs docs/js/main.js
git commit -m "Add post: March 1-7, 2026"
git push
```

---

## Editing an Existing Post

1. Open `src/blog/data.cljs`.
2. Find the map by `:id`.
3. Edit `:title`, `:excerpt`, or `:content` as needed.
4. Rebuild: `bun run build`.
5. Commit both `data.cljs` and `docs/js/main.js`.

---

## Styling Guidelines

### Colour Scheme (Catppuccin Mocha)

All tokens are defined in `docs/css/style.css` as CSS custom properties:

```
--ctp-mauve:   #cba6f7   Primary accent (titles, dream borders)
--ctp-blue:    #89b4fa   Section headers, links, nav
--ctp-teal:    #94e2d5   Subsections, read-more arrow
--ctp-yellow:  #f9e2af   Highlight box border
--ctp-peach:   #fab387   Code, <strong>
--ctp-lavender:#b4befe   <em>
--ctp-text:    #cdd6f4   Primary body text
--ctp-base:    #1e1e2e   Page background
--ctp-mantle:  #181825   Card / article background
```

### Do NOT

- Add inline `style=` attributes to hiccup.
- Create per-post CSS overrides.
- Modify `docs/js/main.js` by hand.
- Add new CSS classes without updating `docs/css/style.css`.

---

## Quality Checklist

Before finalising a new post, verify:

- [ ] `:id` matches `YYYY-MM-DD` format and is unique
- [ ] All `[bracketed]` placeholders replaced
- [ ] `:excerpt` is 2-3 sentences (shown on the index card)
- [ ] `:content` begins with a `[:p ...]` opening paragraph
- [ ] At least one `[:h2 ...]` section break
- [ ] `highlight-box` used for at least one key insight
- [ ] `dream-box` used if there are dream entries (with authentic voice)
- [ ] Technical terms wrapped in `[:code ...]`
- [ ] No HTML entities in strings (use Unicode escapes or literals)
- [ ] `bun run build` completes without errors
- [ ] Site renders correctly at `http://localhost:3000` with `bun run dev`
- [ ] Mobile layout looks right at 768 px width

---

## Writing Style Guidelines

### Tone
- Conversational yet thoughtful
- Self-aware and reflective
- Technically precise but accessible
- Honest about struggles and challenges

### Voice
- First person perspective
- Present tense for current events; past tense for reflections
- Mix of technical and personal content

### Sensitive Content
- Use initials or vague references for third parties
- Frame personal challenges constructively
- Keep professional boundaries in career content

### Dream Entries
- Always use `[:div.dream-box ...]`
- Keep the authentic, stream-of-consciousness quality
- The CSS adds the 💭 prefix automatically — do not add it in content

---

## Architecture Notes

### Router (`src/blog/router.cljs`)

- Single Reagent atom `current-route` drives the whole UI.
- `init!` must be called once at startup to parse the initial hash and
  attach the `hashchange` listener.
- Navigation helpers: `navigate-to-index!`, `navigate-to-post!`.

### Views (`src/blog/views.cljs`)

- `index-page` — renders the post-card list from `data/all-posts`.
- `post-page [id]` — looks up the post with `data/get-post`; shows a
  "not found" state if `nil`.
- `into [:article.blog-post] (:content post)` splices the hiccup vector
  directly — no extra wrapper needed.

### Data (`src/blog/data.cljs`)

- `posts` — the source-of-truth `def`. All content lives here.
- `all-posts` — returns posts sorted newest-first.
- `get-post` — `O(n)` linear scan; fine for a personal blog.

---

## Quick Reference

### Commands

| Task                      | Command                              |
|---------------------------|--------------------------------------|
| Install deps              | `bun install`                        |
| Dev server (hot-reload)   | `bun run dev`                        |
| Production build          | `bun run build`                      |
| New post scaffold         | `cd docs && ./new-post.sh YYYY-MM-DD`|

### Key Files

| File                      | Purpose                              |
|---------------------------|--------------------------------------|
| `src/blog/data.cljs`      | ✏️  Edit to add / change posts        |
| `docs/css/style.css`      | ✏️  Edit to change styles             |
| `src/blog/views.cljs`     | ✏️  Edit to change page components    |
| `docs/index.html`         | 🚫 Do not edit (just a shell)        |
| `docs/js/main.js`         | 🚫 Do not edit (compiled output)     |

---

**Last Updated**: 2026-02-28
**Version**: 3.0 — ClojureScript / Reagent
**Maintained by**: AI Agents working with Arik
