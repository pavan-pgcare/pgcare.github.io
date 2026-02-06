# How to Add New Blog Posts to PGCare

This guide explains how to add new blog posts to your PGCare website without touching any other files.

## Quick Start

1. **Create a new file** in the `_posts` folder
2. **Name it** using this format: `YYYY-MM-DD-post-title.md`
   - Example: `2026-02-15-monitoring-postgresql-connections.md`
3. **Copy the template** from `_posts/TEMPLATE.md`
4. **Write your content** in Markdown
5. **Commit and push** to GitHub

That's it! GitHub Pages will automatically build and publish your post.

## File Naming Convention

Posts MUST follow this naming pattern:
```
YYYY-MM-DD-post-title.md
```

Examples:
- ✅ `2026-02-15-backup-strategies.md`
- ✅ `2026-03-01-query-optimization-tips.md`
- ❌ `backup-strategies.md` (missing date)
- ❌ `2026-2-15-post.md` (wrong date format)

## Post Front Matter (Required)

Every post must start with front matter between `---` markers:

```yaml
---
layout: post
title: "Your Post Title Here"
date: 2026-02-15
author: PGCare
tags: [postgresql, backups, monitoring]
excerpt: "A brief summary for listings and SEO (under 160 characters)"
---
```

### Front Matter Fields:

- **layout**: Always use `post` (required)
- **title**: Your post title in quotes (required)
- **date**: Publication date in YYYY-MM-DD format (required)
- **author**: Usually "PGCare" (optional)
- **tags**: Array of relevant tags (optional but recommended)
- **excerpt**: Short summary for listings (optional but recommended)

## Writing Your Post

### Basic Markdown Syntax

```markdown
# H1 Heading (don't use - title comes from front matter)
## H2 Heading
### H3 Heading

**Bold text**
*Italic text*

- Bullet point
- Another point

1. Numbered list
2. Second item

[Link text](https://example.com)

![Image alt text](/assets/images/image.png)
```

### Code Blocks

For SQL queries:
````markdown
```sql
SELECT * FROM pg_stat_activity;
```
````

For configuration files:
````markdown
```conf
max_connections = 100
shared_buffers = 256MB
```
````

For shell commands:
````markdown
```bash
pg_dump -U postgres mydb > backup.sql
```
````

### Excerpt Separator

Use `<!--more-->` to mark where the excerpt ends:

```markdown
Your opening paragraph that appears in listings.

<!--more-->

The rest of your post that only appears on the full post page.
```

## Common Tags

Use consistent tags across posts:

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
- `troubleshooting`
- `query-optimization`

## Example Complete Post

```markdown
---
layout: post
title: "5 PostgreSQL Monitoring Metrics You Should Track"
date: 2026-02-15
author: PGCare
tags: [postgresql, monitoring, best-practices]
excerpt: "Essential PostgreSQL metrics for production monitoring and why they matter for database reliability."
---

Monitoring PostgreSQL effectively means tracking the right metrics. Here are the five most critical ones.

<!--more-->

## 1. Connection Count

Track active connections against your `max_connections` setting:

```sql
SELECT count(*) FROM pg_stat_activity;
```

Why it matters: Running out of connections causes application failures.

## 2. Replication Lag

For replicated setups, monitor lag in bytes:

```sql
SELECT 
    client_addr,
    pg_wal_lsn_diff(pg_current_wal_lsn(), replay_lsn) AS lag_bytes
FROM pg_stat_replication;
```

## Conclusion

These five metrics form the foundation of PostgreSQL monitoring. Set up alerts for each one.
```

## Publishing Your Post

1. Save your file in `_posts/` with the correct naming format
2. Commit to git: `git add _posts/your-post.md`
3. Commit: `git commit -m "Add new post about monitoring"`
4. Push: `git push origin main`
5. GitHub Pages will build automatically (takes 1-2 minutes)

## Tips for Great Posts

- ✅ **Be practical**: Share real-world experience
- ✅ **Be specific**: Include actual commands and queries
- ✅ **Be concise**: Respect your reader's time
- ✅ **Test your code**: Make sure examples actually work
- ✅ **Explain why**: Don't just show what, explain why it matters
- ❌ **Avoid theory**: Focus on actionable advice
- ❌ **Don't assume**: Explain PostgreSQL-specific concepts

## Need Help?

- Check existing posts in `_posts/` for examples
- Use `_posts/TEMPLATE.md` as a starting point
- Markdown guide: https://www.markdownguide.org/basic-syntax/

---

**Remember**: You only need to add files to `_posts/`. Everything else is already configured!

