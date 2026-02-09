# yokaihex.com

Personal site and blog. Built with Jekyll, hosted on GitHub Pages, domain via Cloudflare.

## Deployment: Step by Step

### Step 1: Create the GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Repository name: **`yokaihex.github.io`** (this exact name is required for GitHub Pages)
3. Set to **Public**
4. Do NOT initialize with README (we're pushing our own files)
5. Click "Create repository"

### Step 2: Push This Site to GitHub

Open a terminal on your local machine:

```bash
# Clone/download these files to a local folder, then:
cd yokaihex-site

# Initialize git
git init
git branch -M main

# Add the remote (replace with your actual repo URL)
git remote add origin https://github.com/yokaihex/yokaihex.github.io.git

# Add all files
git add .

# Commit
git commit -m "Initial site launch"

# Push
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repo: `github.com/yokaihex/yokaihex.github.io`
2. Click **Settings** → **Pages** (in left sidebar)
3. Under "Source", select **Deploy from a branch**
4. Branch: **main**, folder: **/ (root)**
5. Click **Save**
6. Wait 1-2 minutes, then visit `https://yokaihex.github.io` — your site should be live

### Step 4: Connect Your Custom Domain (Cloudflare DNS)

**In GitHub:**
1. Repo Settings → Pages → Custom domain
2. Enter: `yokaihex.com`
3. Click Save (this also creates/updates the CNAME file)

**In Cloudflare Dashboard:**
1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Select `yokaihex.com`
3. Go to **DNS** → **Records**
4. Add these records:

| Type   | Name | Content             | Proxy Status |
|--------|------|---------------------|-------------|
| A      | @    | 185.199.108.153     | DNS only ⚪ |
| A      | @    | 185.199.109.153     | DNS only ⚪ |
| A      | @    | 185.199.110.153     | DNS only ⚪ |
| A      | @    | 185.199.111.153     | DNS only ⚪ |
| CNAME  | www  | yokaihex.github.io  | DNS only ⚪ |

> **IMPORTANT:** Set proxy status to **DNS only** (gray cloud), NOT Proxied (orange cloud).
> GitHub needs direct access to provision your free HTTPS certificate.

### Step 5: Wait for DNS + HTTPS

- DNS propagation: 5 minutes to 24 hours (usually under 30 minutes)
- HTTPS certificate: GitHub auto-provisions via Let's Encrypt after DNS resolves
- Check progress: Repo Settings → Pages → should show a green checkmark

**Verify DNS is working:**
```bash
dig yokaihex.com +short
# Should return GitHub's IPs: 185.199.108.153, etc.
```

### Step 6: Enforce HTTPS

Once the certificate is provisioned:
1. Repo Settings → Pages → Check **"Enforce HTTPS"**

### Step 7: Cloudflare SSL Settings

In Cloudflare dashboard → SSL/TLS:
- Set encryption mode to **Full** (not Full Strict, not Flexible)
- This ensures Cloudflare respects GitHub's certificate

---

## Adding Blog Posts

Create a new Markdown file in `_posts/`:

```
_posts/2026-03-15-my-first-advisory.md
```

With this front matter:

```yaml
---
layout: post
title: "Advisory Title Here"
date: 2026-03-15
tags: [vulnerability-research, synology]
---

Your content in Markdown here...
```

Push to GitHub and it auto-deploys in ~1 minute.

## File Structure

```
yokaihex.github.io/
├── _config.yml          # Jekyll configuration
├── _layouts/
│   └── post.html        # Blog post template
├── _posts/
│   └── 2026-02-08-hello-world.md  # Example post (delete when ready)
├── index.html           # Landing page
├── 404.html             # Custom 404 page
├── CNAME                # Custom domain config
├── Gemfile              # Ruby dependencies (for local dev)
├── .gitignore
└── README.md
```

## Local Development (Optional)

If you want to preview changes locally before pushing:

```bash
# Install Ruby and Bundler (if not already installed)
# On macOS: brew install ruby
# Then: gem install bundler

# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000
```

## Customization Notes

- **Update your real name**: The site currently uses "yokaihex" as the display identity. If you want your real name visible, edit `index.html`.
- **Add more research**: Copy an existing `research-card` block in `index.html` and update the link, title, and description.
- **Bluesky domain verification**: Once the site is live, follow the Bluesky domain handle process to become `@yokaihex.com`.
- **Email setup**: Set up Cloudflare Email Routing to forward `contact@yokaihex.com` → `yokaihex@protonmail.com`.
