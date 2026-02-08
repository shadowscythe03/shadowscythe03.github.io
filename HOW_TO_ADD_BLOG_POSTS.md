# How to Add Blog Posts

Your Hugo Academic site includes a blog section where you can publish articles, tutorials, and updates. Here's how to add new blog posts:

## Quick Start

1. **Navigate to the blog directory**:
   ```
   content/blog/
   ```

2. **Create a new folder** for your post (use kebab-case):
   ```
   content/blog/my-new-post/
   ```

3. **Create `index.md`** inside that folder with the following structure:

```markdown
---
title: 'Your Post Title'
summary: 'Brief summary of your post (1-2 sentences)'
date: 2025-12-02
authors:
  - admin
tags:
  - AI
  - Machine Learning
  - Tutorial
image:
  caption: 'Optional image caption'
  focal_point: ''
  preview_only: false
---

Your post content starts here...

## Section Heading

Write your content using Markdown syntax.

### Code Blocks

\```python
def hello_world():
    print("Hello, World!")
\```

### Math Equations

Use LaTeX for equations:
$$ E = mc^2 $$

### Images

![Alt text](image.png)

### Links

[Link text](https://example.com)
```

## Post Components

### Front Matter (YAML header)

- **title**: The post title (required)
- **summary**: Short description shown in list views
- **date**: Publication date in YYYY-MM-DD format
- **authors**: List of authors (use `admin` for yourself)
- **tags**: Keywords for categorization
- **image**: Optional featured image settings

### Content Sections

You can include:
- Text with Markdown formatting
- Code blocks with syntax highlighting
- Mathematical equations (LaTeX)
- Images and figures
- Tables
- Quotes
- Lists (ordered and unordered)

## Example Post Structure

```
content/blog/my-research-update/
├── index.md          # Main post content
├── featured.jpg      # Optional featured image
└── figure1.png       # Other images referenced in the post
```

## Publishing Workflow

1. **Draft Your Post**: Write content in `index.md`
2. **Add Images**: Place images in the same folder
3. **Preview Locally**: Run `hugo server` to preview
4. **Commit Changes**: Git add, commit, and push
5. **Deploy**: GitHub Pages will auto-deploy

## Tips

- **Keep URLs clean**: Use lowercase and hyphens in folder names
- **Add summaries**: Write clear summaries for better SEO
- **Use tags wisely**: Consistent tags help with discoverability
- **Include images**: Visual content increases engagement
- **Write in Markdown**: It's simple and portable

## Markdown Cheatsheet

```markdown
# H1 Heading
## H2 Heading
### H3 Heading

**Bold text**
*Italic text*
`Inline code`

- Bullet point
- Another point

1. Numbered item
2. Another item

[Link](https://example.com)
![Image](image.png)
```

## Advanced Features

### Series/Multi-part Posts

For multi-part series, use consistent naming:
```
content/blog/series-name-part-1/
content/blog/series-name-part-2/
content/blog/series-name-part-3/
```

### Draft Posts

To keep a post as draft, add to front matter:
```yaml
draft: true
```

### Custom Layouts

You can customize post layouts by modifying:
```
layouts/blog/
```

## Current Blog Posts

Your site currently has these example posts in `content/blog/`:
- `get-started/`
- `data-visualization/`
- `project-management/`
- `second-brain/`
- `teach-courses/`

You can modify or delete these example posts.

## Questions?

- Check the [Hugo Blox Documentation](https://docs.hugoblox.com/)
- See [Markdown Guide](https://www.markdownguide.org/)
- Review example posts in your `content/blog/` directory

Happy blogging! 🚀
