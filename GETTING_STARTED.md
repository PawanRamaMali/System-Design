# Getting Started with Your System Design Book

## Quick Start Guide

Your System Design content has been transformed into a professional book format using Quarto!

## 📁 What's Been Created

```
System-Design/
├── _quarto.yml              # Book configuration
├── index.qmd                # Book preface/introduction
├── chapters/                # All 13 chapters (ch01-ch13)
├── images/                  # Directory for diagrams
├── references.bib           # Bibliography
├── theme-light.scss         # Light theme styling
├── theme-dark.scss          # Dark theme styling
├── BOOK_README.md           # Comprehensive book README
├── GETTING_STARTED.md       # This file
└── .gitignore              # Git ignore patterns
```

## 🚀 Next Steps

### 1. Install Quarto

Download and install Quarto from: https://quarto.org/docs/get-started/

**Windows:**
```powershell
# Download installer from https://quarto.org/docs/download/
# Or use winget
winget install Posit.Quarto
```

**Mac:**
```bash
brew install --cask quarto
```

**Linux:**
```bash
# Download from https://quarto.org/docs/download/
```

### 2. Preview Your Book

```bash
# Navigate to your repository
cd C:\Github\System-Design

# Preview the book (opens in browser with live reload)
quarto preview
```

This will:
- Generate the book
- Open it in your default browser
- Auto-reload when you make changes

### 3. Build the Book

```bash
# Build HTML version
quarto render

# Build PDF (requires LaTeX installation)
quarto render --to pdf

# Build EPUB
quarto render --to epub

# Build all formats
quarto render --to all
```

The output will be in the `docs/` directory.

### 4. Customize the Book

Edit `_quarto.yml` to customize:

```yaml
book:
  title: "Your Title Here"
  author: "Your Name"
  # ... other settings
```

### 5. Add Diagrams

Move your existing images to the `images/` directory, or create new diagrams using:
- [Mermaid](https://mermaid.js.org/) (built into Quarto)
- [Graphviz](https://graphviz.org/)
- Export from draw.io, Excalidraw, etc.

Example using Mermaid in a chapter:

````markdown
```{mermaid}
graph LR
    A[Client] --> B[Load Balancer]
    B --> C[Server 1]
    B --> D[Server 2]
    B --> E[Server 3]
```
````

### 6. Publish Your Book

#### GitHub Pages (Free Hosting)

```bash
# Render to docs folder
quarto render

# Commit and push
git add .
git commit -m "Add book content"
git push origin main

# Enable GitHub Pages:
# Go to Settings → Pages → Source: main branch /docs folder
```

Your book will be available at: `https://yourusername.github.io/System-Design/`

#### Quarto Pub (Alternative)

```bash
quarto publish quarto-pub
```

## 📝 Editing Content

### Adding a New Chapter

1. Create new file: `chapters/ch14-new-topic.qmd`
2. Add to `_quarto.yml`:
   ```yaml
   chapters:
     - chapters/ch14-new-topic.qmd
   ```
3. Write content using Markdown

### Markdown Features

Quarto supports rich Markdown features:

````markdown
# Heading 1
## Heading 2

**Bold** and *italic*

- Bullet lists
1. Numbered lists

```python
# Code blocks with syntax highlighting
def hello():
    print("Hello, World!")
```

> Blockquotes

[Links](https://example.com)

![Images](images/diagram.png)

| Tables | Are | Supported |
|--------|-----|-----------|
| Col 1  | Col 2 | Col 3   |
````

### Callouts (Special Boxes)

```markdown
:::{.callout-note}
This is a note
:::

:::{.callout-warning}
This is a warning
:::

:::{.callout-tip}
This is a tip
:::

:::{.callout-important}
This is important
:::
```

### Cross-References

```markdown
See @fig-architecture for the architecture diagram.

![Architecture Overview](images/arch.png){#fig-architecture}
```

## 🎨 Customization

### Themes

Edit `theme-light.scss` and `theme-dark.scss` to customize colors and styling.

### Layout

Edit `_quarto.yml` to change:
- Number of table of contents levels
- Code highlighting theme
- Output formats
- And much more!

## 📖 Resources

- **Quarto Documentation**: https://quarto.org/docs/guide/
- **Quarto Books**: https://quarto.org/docs/books/
- **Markdown Guide**: https://quarto.org/docs/authoring/markdown-basics.html
- **Publishing**: https://quarto.org/docs/publishing/

## 🔧 Troubleshooting

### Preview Not Working?

```bash
# Check Quarto is installed
quarto --version

# Clean and rebuild
quarto clean
quarto preview
```

### PDF Not Rendering?

PDF requires LaTeX. Install:
- **Windows**: MiKTeX or TinyTeX
- **Mac**: MacTeX or TinyTeX
- **Linux**: TeX Live

Or install TinyTeX via Quarto:
```bash
quarto install tinytex
```

## 💡 Tips

1. **Use VS Code** with the Quarto extension for best editing experience
2. **Keep `quarto preview` running** while editing for live updates
3. **Commit often** to track your changes
4. **Use branches** for major revisions
5. **Check the rendered output** frequently to catch formatting issues

## 📧 Need Help?

- Quarto Discussions: https://github.com/quarto-dev/quarto-cli/discussions
- Stack Overflow: Tag with `quarto`

---

**You're all set! Start writing and building your book! 🚀**
