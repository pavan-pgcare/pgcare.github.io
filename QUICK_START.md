# 🚀 Quick Start Guide - PGCare Website

## Adding a New Blog Post (3 Steps)

### Step 1: Create the File
Create a new file in the `_posts` folder with this naming format:
```
_posts/YYYY-MM-DD-your-post-title.md
```

**Example:**
```
_posts/2026-02-15-postgresql-backup-best-practices.md
```

### Step 2: Add Front Matter
Copy this template to the top of your file:

```yaml
---
layout: post
title: "PostgreSQL Backup Best Practices"
date: 2026-02-15
author: PGCare
tags: [postgresql, backups, best-practices]
excerpt: "Essential backup strategies every PostgreSQL DBA should know."
---
```

### Step 3: Write Your Content

```markdown
Your opening paragraph goes here. This hooks the reader.

<!--more-->

## Main Section

Your detailed content here. Use:

- Bullet points
- **Bold** and *italic* text
- Code blocks

### SQL Examples

```sql
SELECT * FROM pg_stat_activity;
```

## Conclusion

Wrap up with key takeaways.
```

### Step 4: Publish
```bash
git add _posts/2026-02-15-your-post.md
git commit -m "Add new post about backups"
git push origin main
```

**Done!** Your post will be live in 1-2 minutes.

---

## 📋 Quick Reference

### File Naming
- ✅ `2026-02-15-backup-strategies.md`
- ❌ `backup-strategies.md` (missing date)
- ❌ `2026-2-15-post.md` (wrong date format)

### Required Front Matter
```yaml
layout: post          # Always "post"
title: "Your Title"   # In quotes
date: 2026-02-15      # YYYY-MM-DD format
```

### Optional Front Matter
```yaml
author: PGCare
tags: [postgresql, monitoring, performance]
excerpt: "Brief summary for listings"
```

### Common Tags
- `postgresql`
- `backups`
- `disaster-recovery`
- `monitoring`
- `performance`
- `replication`
- `high-availability`
- `migrations`
- `security`
- `best-practices`

### Markdown Syntax

```markdown
# H1 (don't use - comes from title)
## H2 Heading
### H3 Heading

**Bold text**
*Italic text*

- Bullet point
- Another point

1. Numbered list
2. Second item

[Link text](https://example.com)

![Image](/assets/images/image.png)

```sql
SELECT * FROM table;
```

```bash
pg_dump database > backup.sql
```
```

---

## 🎯 What You Need to Know

### ✅ Files You WILL Edit
- `_posts/*.md` - Your blog posts (add new files here)

### ⚠️ Files You MIGHT Edit (Rarely)
- `_config.yml` - Site settings (email, description)
- `about.html` - Update your bio
- `services.html` - Adjust service descriptions

### 🚫 Files You DON'T Need to Touch
- `_layouts/` - Page templates
- `assets/css/main.css` - All styles
- `index.html` - Homepage structure
- `blog.html` - Blog listing structure

---

## 📁 Where Things Are

```
_posts/                    ← ADD YOUR BLOG POSTS HERE
├── TEMPLATE.md           ← Copy this for new posts
└── 2026-02-06-*.md       ← Your posts

_layouts/                  ← Don't touch
assets/css/main.css       ← Don't touch
index.html                ← Homepage (rarely edit)
blog.html                 ← Blog page (rarely edit)
services.html             ← Services (maybe edit)
about.html                ← About (maybe edit)
_config.yml               ← Settings (rarely edit)
```

---

## 🆘 Common Questions

**Q: How do I preview locally?**
```bash
bundle install
bundle exec jekyll serve
# Open http://localhost:4000
```

**Q: How long until my post is live?**
A: 1-2 minutes after pushing to GitHub.

**Q: Can I schedule posts for the future?**
A: Yes! Use a future date. Jekyll won't publish until that date.

**Q: How do I add images?**
A: 
1. Add image to `assets/images/`
2. Reference in post: `![Alt text](/assets/images/your-image.png)`

**Q: How do I delete a post?**
A: Delete the file from `_posts/` and push.

**Q: Can I edit a published post?**
A: Yes! Edit the file and push. Updates in 1-2 minutes.

---

## 📚 Full Documentation

- **Detailed Guide**: See `HOW_TO_ADD_POSTS.md`
- **Complete Overview**: See `WEBSITE_OVERVIEW.md`
- **Project Info**: See `README.md`

---

## ✨ That's It!

You now have a professional website. Just add Markdown files to `_posts/` and push to GitHub. Everything else is automatic!

**Happy blogging! 🎉**

