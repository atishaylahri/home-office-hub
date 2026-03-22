# Home Office Hub

An automated affiliate blog in the home office tech niche. Claude generates a new SEO-optimized post every Sunday. Zero ongoing effort after setup.

## How It Works

1. `topics.txt` holds a queue of 52 article topics (1 year of posts)
2. Every Sunday, a GitHub Action runs `generate_post.py`
3. The script calls Claude AI (Haiku model) to write a full affiliate blog post
4. The post is committed to the repo — GitHub Pages rebuilds the site automatically

**Monthly cost: ~$1–2** (Claude API only — hosting is free)

---

## One-Time Setup (do this on your Mac Mini)

### 1. Update `hugo.toml`
Replace `YOUR_GITHUB_USERNAME` and `home-office-hub` with your actual GitHub username and repo name:
```toml
baseURL = "https://your-actual-username.github.io/your-repo-name/"
```

### 2. Update `generate_post.py`
After Amazon Associates approval, replace the associate ID:
```python
AMAZON_ASSOCIATE_ID = "your-actual-id-20"
```

### 3. Create GitHub Repository
- Go to github.com → New repository
- Name it `home-office-hub` (or anything you like — match it in `hugo.toml`)
- Set to **Public**
- Do NOT initialize with README (you already have one)

### 4. Push Files
```bash
cd "Desktop/Passive Income"
git init
git add .
git commit -m "Initial site setup"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/home-office-hub.git
git push -u origin main
```

Or use GitHub Desktop app (drag and drop the folder).

### 5. Add API Key Secret
- Go to your repo on GitHub
- Settings → Secrets and variables → Actions → New repository secret
- Name: `ANTHROPIC_API_KEY`
- Value: your Anthropic API key (get one at console.anthropic.com)

### 6. Enable GitHub Pages
- Repo → Settings → Pages
- Source: **GitHub Actions**
- Click Save

Your site will be live at `https://YOUR_USERNAME.github.io/home-office-hub/` within 2–3 minutes.

### 7. Apply for Amazon Associates
- Go to affiliate-program.amazon.com
- Apply with your live site URL
- Once approved, update `AMAZON_ASSOCIATE_ID` in `generate_post.py`

---

## Manual Post Generation

To generate a post manually (useful for seeding more content):
```bash
pip install anthropic
export ANTHROPIC_API_KEY=your_key_here
python generate_post.py
```

## File Structure

```
├── hugo.toml              # Site configuration
├── generate_post.py       # AI post generator script
├── topics.txt             # Queue of article topics
├── content/
│   ├── _index.md          # Home page content
│   ├── about.md
│   ├── privacy.md
│   ├── affiliate-disclosure.md
│   └── posts/             # Generated blog posts land here
├── layouts/               # Custom Hugo templates
├── static/css/style.css   # Site styles
└── .github/workflows/     # Automation
    ├── weekly-post.yml    # Generates post every Sunday
    └── deploy.yml         # Builds and deploys to GitHub Pages
```
