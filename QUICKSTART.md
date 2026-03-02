# Quick Start Guide

## Adding a New Blog Post

### 1. Quick Method (Copy & Edit)

```bash
# Copy the template
cp posts/_template.html posts/2026-03-07.html

# Edit the new file
# Replace all [BRACKETED] placeholders with your content
```

### 2. What to Replace

In your new `posts/YYYY-MM-DD.html` file:

- `[TITLE]` → Your blog post title (in `<title>` tag)
- `[DATE RANGE]` → Date range like "March 1-7, 2026"
- `[BLOG POST TITLE]` → Title in the header
- `[...]` sections → Your actual content

### 3. Update the Index Page

Add your post to `index.html` by inserting this at the TOP of `<main class="post-list">`:

```html
<a href="posts/2026-03-07.html" class="post-card">
    <h2>Your Blog Post Title</h2>
    <span class="post-date">March 1-7, 2026</span>
    <p class="post-excerpt">
        Copy the first paragraph or write a 2-3 sentence summary here.
    </p>
    <span class="read-more">Read more</span>
</a>
```

### 4. File Naming

- Name posts by the **last day** of the week: `2026-03-07.html` for week ending March 7
- Keep posts in reverse chronological order (newest first)

## Content Structure

### Typical Blog Post Sections

1. **Introduction** - Set the tone, summarize the week
2. **Career/Professional** - Job hunting, meetings, work stuff
3. **Technical Projects** - Development, tools, configuration
4. **Dreams & Philosophy** - Personal reflections, insights
5. **Conclusion** - Forward-looking wrap-up

### Special Elements

#### Highlight Box (Key Insights)
```html
<div class="highlight-box">
    <p><strong>Key insight:</strong> Your important takeaway here.</p>
</div>
```

#### Dream Box
```html
<div class="dream-box">
    <p>Your dream description here. Keep the stream-of-consciousness style.</p>
</div>
```

#### Code References
```html
Use <code>inline code</code> for commands, tools, and technical terms.
```

## From Journal to Blog Post

### 1. Find Your Journals

Journal files are in `../journals/` with names like:
- `2026-03-07.org`
- `2026_03_07.org`

### 2. Read the Past Week

Identify all journal files from the past 7 days.

### 3. Synthesize Content

**Don't** just list entries day by day.

**Do** group by theme:
- All career stuff together
- All technical projects together
- Dreams and reflections together

### 4. Write Naturally

- First person, conversational tone
- Provide context for technical details
- Connect ideas across days
- Show authentic voice and struggles

## Quick Checklist

Before publishing:

- [ ] All `[BRACKETS]` replaced
- [ ] Title matches content
- [ ] Date range is correct
- [ ] Post added to index.html
- [ ] Links work (test the back button)
- [ ] No Lorem Ipsum or placeholder text
- [ ] Code wrapped in `<code>` tags
- [ ] Sections flow naturally

## Example Workflow

```bash
# 1. Create new post from template
cp posts/_template.html posts/2026-03-07.html

# 2. Edit the post
vim posts/2026-03-07.html

# 3. Update index
vim index.html

# 4. Test locally
open index.html  # or your browser command

# 5. Commit
git add .
git commit -m "Add post: March 1-7, 2026"
git push
```

## Need Help?

- **Styling issues**: Check `_template.html` for correct CSS classes
- **Structure questions**: Read `AGENTS.md` for detailed guidelines
- **Content tips**: See "Content Synthesis" section in `AGENTS.md`
- **Theme colors**: All Catppuccin Mocha variables are in the `:root` CSS

## Color Reference (Catppuccin Mocha)

Quick reference for custom content:

- **Mauve** `#cba6f7` - Primary accent (titles, links)
- **Blue** `#89b4fa` - Section headers
- **Teal** `#94e2d5` - Subsection headers
- **Yellow** `#f9e2af` - Highlight boxes
- **Peach** `#fab387` - Code, emphasis
- **Text** `#cdd6f4` - Main text color
- **Base** `#1e1e2e` - Background

---

That's it! Copy, edit, update index, done. 🚀