# PGCare - PostgreSQL Reliability Consulting

A professional Jekyll-based website for PostgreSQL consulting and blog.

## 🚀 Quick Start for Adding Blog Posts

**You only need to work with the `_posts` folder!**

1. Create a new file: `_posts/YYYY-MM-DD-your-title.md`
2. Copy the template from `_posts/TEMPLATE.md`
3. Write your content in Markdown
4. Commit and push to GitHub

See [HOW_TO_ADD_POSTS.md](HOW_TO_ADD_POSTS.md) for detailed instructions.

## 📁 Project Structure

```
pgcare.github.io/
├── _layouts/           # Page templates (don't modify)
│   ├── default.html    # Main layout with header/footer
│   └── post.html       # Blog post layout
├── _posts/             # YOUR BLOG POSTS GO HERE
│   ├── TEMPLATE.md     # Copy this for new posts
│   └── *.md            # Your blog posts
├── assets/
│   ├── css/
│   │   └── main.css    # All styles (don't modify)
│   └── images/         # Add images here if needed
├── _config.yml         # Site configuration (rarely needs changes)
├── index.html          # Homepage
├── blog.html           # Blog listing page
├── services.html       # Services page
├── about.html          # About page
└── HOW_TO_ADD_POSTS.md # Guide for adding posts
```

## 🎨 Features

- ✅ Modern, professional design
- ✅ Fully responsive (mobile, tablet, desktop)
- ✅ Dark mode support (automatic based on system preference)
- ✅ SEO optimized with meta tags
- ✅ Fast loading and performance optimized
- ✅ Clean, readable blog post layout
- ✅ Service pages for consulting offerings
- ✅ Easy to add new posts (just add Markdown files)

## 📝 Adding New Blog Posts

**Simple 3-step process:**

1. **Create file**: `_posts/2026-02-15-my-post-title.md`
2. **Add front matter**:
   ```yaml
   ---
   layout: post
   title: "My Post Title"
   date: 2026-02-15
   tags: [postgresql, backups]
   excerpt: "Brief summary"
   ---
   ```
3. **Write content** in Markdown

That's it! Push to GitHub and it's live.

## 🛠️ Local Development (Optional)

If you want to preview locally before publishing:

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Open browser to http://localhost:4000
```

## 🌐 Deployment

This site is configured for GitHub Pages. Every push to `main` branch automatically deploys.

- **Live URL**: https://pgcare.co.in
- **Build time**: 1-2 minutes after push
- **No manual deployment needed**

## 📋 Content Guidelines

When writing posts:

- ✅ Be practical and specific
- ✅ Include real-world examples
- ✅ Use code blocks for SQL/config
- ✅ Keep it concise and actionable
- ✅ Focus on PostgreSQL reliability topics

## 🎯 Key Pages

- **Homepage** (`index.html`): Hero section, services overview, latest posts
- **Blog** (`blog.html`): All blog posts listing
- **Services** (`services.html`): Consulting services offered
- **About** (`about.html`): About PGCare and philosophy

## 🔧 Configuration

Site settings are in `_config.yml`. You rarely need to change these, but key settings:

- `title`: Site title
- `description`: Site description for SEO
- `url`: Your domain
- `author.email`: Contact email

## 📱 Responsive Design

The site is fully responsive with breakpoints:

- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px

## 🎨 Design System

- **Primary Color**: PostgreSQL Blue (#336791)
- **Font**: Inter (headings & body), JetBrains Mono (code)
- **Max Width**: 1200px
- **Spacing**: Consistent 8px grid system

## 📞 Support

For questions about adding content, see [HOW_TO_ADD_POSTS.md](HOW_TO_ADD_POSTS.md)

---

**Built with Jekyll • Hosted on GitHub Pages • Designed for PostgreSQL Professionals**

