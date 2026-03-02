# Documentation Index

## 🗂️ Complete Documentation Guide

Welcome! This index helps you navigate all documentation for the Journal Blog website.

---

## 📚 Quick Navigation

| Document | Purpose | For Who |
|----------|---------|---------|
| [QUICKSTART.md](QUICKSTART.md) | Get started fast | **Start here!** |
| [OVERVIEW.md](OVERVIEW.md) | Project overview | Everyone |
| [STRUCTURE.md](STRUCTURE.md) | Visual structure guide | Developers |
| [README.org](README.org) | General information | Everyone |
| [AGENTS.md](AGENTS.md) | AI agent instructions | AI Agents |

---

## 🎯 Find What You Need

### I Want To...

#### ✏️ **Create a New Blog Post**
→ Read [QUICKSTART.md](QUICKSTART.md)
- Step-by-step instructions
- Copy-paste examples
- Quick checklist

#### 🏗️ **Understand the Project Structure**
→ Read [STRUCTURE.md](STRUCTURE.md)
- Visual diagrams
- File relationships
- Component breakdown

#### 📖 **Learn About the Project**
→ Read [OVERVIEW.md](OVERVIEW.md)
- Design philosophy
- Technical details
- Features and roadmap

#### 🎨 **Customize Styling**
→ See [OVERVIEW.md - Design Section](OVERVIEW.md#-design)
- Catppuccin Mocha colors
- CSS class reference
- Styling guidelines

#### 🤖 **Automate or Build Tools**
→ Read [AGENTS.md](AGENTS.md)
- Content processing rules
- Automation workflows
- Quality standards

---

## 📄 Document Summaries

### QUICKSTART.md
**One-page guide to adding posts**
- Simple 4-step process
- Code examples ready to copy
- Common patterns and tips
- Quick reference for colors and classes

**Best for**: Getting your first post published quickly

---

### OVERVIEW.md
**Complete project overview**
- Project structure and file layout
- Design principles and color palette
- Content guidelines and writing style
- Technical stack and deployment
- Future enhancements

**Best for**: Understanding how everything fits together

---

### STRUCTURE.md
**Visual guide to website architecture**
- Directory tree diagrams
- Data flow illustrations
- Navigation patterns
- Component breakdown
- File relationship maps

**Best for**: Visual learners and developers

---

### README.org
**Human-readable project info (Org-mode format)**
- Project description and goals
- Theme information
- Deployment instructions
- Feature list and future improvements

**Best for**: Quick reference and GitHub display

---

### AGENTS.md
**Comprehensive guide for AI agents**
- Source data processing
- Content synthesis strategies
- Styling rules and conventions
- Automation tasks and workflows
- Quality checklist
- Special handling guidelines

**Best for**: AI assistants and automation tools

---

## 🔧 Helper Tools

### new-post.sh
**Bash script to create new posts**

```bash
# Usage
./new-post.sh 2026-03-07

# What it does:
# 1. Copies _template.html to new file
# 2. Calculates date range
# 3. Opens in your editor
# 4. Shows next steps
```

**Location**: `docs/new-post.sh`

---

## 🎯 Common Tasks

### First Time Setup
1. Read [OVERVIEW.md](OVERVIEW.md) - Understand the project
2. Browse `index.html` in browser - See current site
3. Look at `posts/2026-02-28.html` - Example post
4. Read [QUICKSTART.md](QUICKSTART.md) - Learn to create posts

### Creating Your First Post
1. Run `./new-post.sh` or copy `_template.html`
2. Follow [QUICKSTART.md](QUICKSTART.md)
3. Check [STRUCTURE.md](STRUCTURE.md) if confused
4. Reference [AGENTS.md](AGENTS.md) for content tips

### Troubleshooting
1. Check [OVERVIEW.md - Troubleshooting](OVERVIEW.md#-troubleshooting)
2. Verify file structure in [STRUCTURE.md](STRUCTURE.md)
3. Review examples in `posts/2026-02-28.html`

### Learning the Design System
1. Color palette in [OVERVIEW.md](OVERVIEW.md#-design)
2. Component examples in [STRUCTURE.md](STRUCTURE.md)
3. CSS reference in [QUICKSTART.md](QUICKSTART.md)
4. Full styling guide in [AGENTS.md](AGENTS.md)

---

## 📁 File Structure Quick Reference

```
docs/
├── index.html              Landing page
├── posts/
│   ├── _template.html     Template (copy this!)
│   └── YYYY-MM-DD.html    Your blog posts
├── README.org             Project info
├── QUICKSTART.md          Start here!
├── OVERVIEW.md            Full overview
├── STRUCTURE.md           Visual guide
├── AGENTS.md              AI instructions
├── INDEX.md               This file
└── new-post.sh            Helper script
```

---

## 🎨 Design System at a Glance

**Theme**: Catppuccin Mocha (Dark)

| Element | Color | Hex |
|---------|-------|-----|
| Titles | Mauve | `#cba6f7` |
| Headers | Blue | `#89b4fa` |
| Subheads | Teal | `#94e2d5` |
| Highlights | Yellow | `#f9e2af` |
| Code | Peach | `#fab387` |
| Text | Text | `#cdd6f4` |
| Background | Base | `#1e1e2e` |

---

## 🚀 Quick Start Commands

```bash
# Create new post
./new-post.sh 2026-03-07

# View site locally
open index.html

# Deploy to GitHub Pages
git add .
git commit -m "Add post: March 1-7, 2026"
git push
```

---

## 💡 Tips

- **New to the project?** → Start with [QUICKSTART.md](QUICKSTART.md)
- **Need visuals?** → Check [STRUCTURE.md](STRUCTURE.md)
- **Building tools?** → Read [AGENTS.md](AGENTS.md)
- **Quick reference?** → Use this INDEX.md!

---

## 📞 Support

For questions about:
- **Content**: See [AGENTS.md - Content Guidelines](AGENTS.md)
- **Structure**: See [STRUCTURE.md](STRUCTURE.md)
- **Styling**: See [OVERVIEW.md - Design](OVERVIEW.md)
- **Process**: See [QUICKSTART.md](QUICKSTART.md)

---

**Documentation Index v1.0**  
**Last Updated**: 2026-02-28  
**Maintained by**: Arik with AI assistance