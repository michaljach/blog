# Minimal Text Blog

A simple, text-only static blog generator. Write your posts in Markdown and automatically deploy to GitHub Pages with GitHub Actions.

## Features

- Minimal and fast
- Pure static HTML generated at build time
- Markdown support with frontmatter
- Automated deployment via GitHub Actions
- No JavaScript required on the client
- Responsive design
- Clean typography focused on readability
- Each post has its own clean URL path

## Project Structure

```
blog/
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions workflow
├── posts/                  # Markdown blog posts
│   ├── welcome.md
│   └── markdown-guide.md
├── templates/              # HTML templates
│   ├── base.html
│   ├── index.html
│   └── post.html
├── build.js                # Static site generator
├── package.json
├── style.css
└── README.md
```

## Adding a New Post

1. Create a new Markdown file in the `posts/` directory:

```bash
touch posts/2026-01-10-my-new-post.md
```

2. Add frontmatter and write your post content in Markdown:

```markdown
---
title: My New Post
date: 2026-01-10
---

# My New Post

This is my new blog post content...
```

Note: The frontmatter is optional. If omitted:
- Title will be extracted from the first `#` heading or filename
- Date will be extracted from filename (YYYY-MM-DD prefix) or file creation date

3. Commit and push your changes. GitHub Actions will automatically build and deploy.

## Local Development

To test the build locally:

```bash
# Install dependencies
npm install

# Build the site
npm run build

# Serve the dist folder
cd dist
python3 -m http.server 8000
# or
npx http-server
```

Then visit `http://localhost:8000` in your browser.

The generated site will be in the `dist/` directory with this structure:
```
dist/
├── index.html              # Post listing page
├── style.css               # Styles
├── welcome/
│   └── index.html          # Individual post
└── markdown-guide/
    └── index.html          # Individual post
```

Each post is accessible at its own URL path, e.g., `/welcome/` or `/markdown-guide/`.

## Deploying to GitHub Pages

### Automatic Deployment (Recommended)

The blog includes a GitHub Actions workflow that automatically builds and deploys when you push to the main branch.

1. Create a new repository on GitHub

2. Push your blog:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/your-repo-name.git
git push -u origin main
```

3. Enable GitHub Pages with GitHub Actions:
   - Go to your repository Settings
   - Navigate to "Pages" in the sidebar
   - Under "Source", select "GitHub Actions"
   - The workflow will automatically run on the next push

4. Your blog will be available at `https://yourusername.github.io/your-repo-name/`

The workflow will:
- Install Node.js dependencies
- Build the static site from markdown
- Deploy to GitHub Pages

Every time you push new posts to the main branch, the site will automatically rebuild and redeploy.

## Customization

### Change Blog Title and Subtitle

Edit `templates/base.html`:

```html
<header>
    <h1><a href="{{ROOT}}index.html">Your Blog Name</a></h1>
    <p class="subtitle">Your subtitle here</p>
</header>
```

### Modify Styles

Edit `style.css` to change colors, fonts, spacing, etc.

### Customize Templates

The blog uses three templates in the `templates/` directory:
- `base.html` - Main layout wrapper
- `index.html` - Post listing page template
- `post.html` - Individual post page template

You can modify these to change the structure or add additional elements.

### Add More Features

The blog is intentionally minimal, but the build script (`build.js`) can be extended to add:
- Tags/categories
- RSS feed generation
- Pagination
- Related posts
- Custom metadata

## License

Public domain. Use however you like.
