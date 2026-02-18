# kenya-realty Deployment Guide

This guide ensures your real estate playground can transition from local to live production.

## 1. Prerequisites
- [Hugo Extended](https://gohugo.io/installation/) version 0.128+ recommended.
- Git installed.

## 2. Local Production Build
Run the following command to generate a minified, optimized version of the site:
```bash
hugo --gc --minify
```
The output will be in the `/public` directory.

## 3. Deployment Options

### GitHub Pages (Automated)
1. Push your code to a GitHub repository.
2. Go to **Settings > Pages**.
3. Select **GitHub Actions** as the source.
4. Use the official "Hugo" workflow template.

### VPS / Traditional Server
1. Build the site locally: `hugo --minify`.
2. Sync the `public/` directory via SCP or Rsync:
   ```bash
   rsync -avz --delete public/ user@your-vps-ip:/var/www/kenya-realty
   ```

## 4. Environment Configuration
To change the base URL for production, either:
- Update `hugo.toml`: `baseURL = "https://yourdomain.com/"`
- Or pass it via CLI: `hugo --baseURL "https://yourdomain.com/"`

## 5. Scaling Content
To add a new property, use the page bundle structure:
```bash
mkdir -p content/properties/houses/new-listing
echo '--- title: "New Home" ... ---' > content/properties/houses/new-listing/index.md
cp your-photos/*.jpg content/properties/houses/new-listing/
```
The system will automatically resize and optimize these images upon build.
