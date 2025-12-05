# shift1w.com

Personal website built with Hugo and deployed via GitHub Actions.

## Deployment Workflow

This site uses a three-branch deployment strategy for safety:

1. **Development**: Work on the `develop` branch (push freely without triggering deployment)
2. **Staging**: Merge `develop` into `stage` when ready to deploy
3. **Build**: Push to `stage` triggers GitHub Actions to build Hugo site
4. **Commit**: The workflow pushes the built `public` folder to the `master` branch
5. **Deploy**: Cloudflare Pages automatically deploys from the `master` branch to shift1w.com

## Local Development

```bash
# Install Hugo (if not already installed)
# On macOS: brew install hugo
# On Linux: apt-get install hugo
# Or download from https://gohugo.io/installation/

# Start the Hugo development server
hugo server -D

# Build the site
hugo
```

## Deployment

### Daily Development
Work on the `develop` branch without triggering deployments:

```bash
git add .
git commit -m "Your changes"
git push origin develop
```

### Deploy to Production
When ready to deploy, merge to `stage`:

```bash
git checkout stage
git merge develop
git push origin stage
```

The GitHub Actions workflow will automatically:
- Build your Hugo site with `hugo --minify`
- Push the generated `public` folder to the `master` branch

Cloudflare Pages will then automatically deploy the changes from `master`.

## Cloudflare Pages Configuration

Your Cloudflare Pages should be configured to:
- Connect to the `jacobwiseberg/shift1w` GitHub repository
- Deploy from the `master` branch
- Production branch: `master`
- Build configuration: None (pre-built by GitHub Actions)
- Build output directory: `/` (root, since `master` contains only built files)

## Site Structure

- `content/` - Markdown content files
- `layouts/` - HTML templates
- `static/` - Static assets
- `i18n/` - Internationalization files (English & Hebrew)
- `hugo.toml` - Hugo configuration
