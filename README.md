# kustonaut.github.io — Portfolio

Personal portfolio site for [Akshay Dixit](https://github.com/kustonaut).

## Deploy to GitHub Pages

### Option A: User site (`kustonaut.github.io`)

1. Create a new GitHub repo named **`kustonaut.github.io`**
2. Copy the portfolio files into the repo root:
   ```bash
   git init
   cp /path/to/portfolio/* .
   git add .
   git commit -m "🚀 Launch portfolio"
   git remote add origin https://github.com/kustonaut/kustonaut.github.io.git
   git push -u origin main
   ```
3. GitHub Pages auto-deploys user sites. Visit **https://kustonaut.github.io** within a few minutes.

### Option B: Project site (any repo)

1. In the repo, go to **Settings → Pages**
2. Set Source: **Deploy from a branch**
3. Select branch: `main`, folder: `/ (root)`
4. Push `index.html` to the repo root
5. Site will be available at `https://kustonaut.github.io/<repo-name>/`

### Custom Domain (optional)

1. Add a `CNAME` file with your domain (e.g., `akshaydixit.dev`)
2. Configure DNS:
   - CNAME record: `kustonaut.github.io`
   - Or A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. In repo Settings → Pages → Custom domain, enter your domain
4. Enable **Enforce HTTPS**

## Tech

- Pure HTML/CSS/JS — no build tools, no frameworks
- Google Fonts (Inter + JetBrains Mono)
- Intersection Observer for scroll animations
- Animated counter for metrics
- Typing animation for hero taglines
- Mobile responsive
- Reduced-motion support
- Dark theme

## Structure

```
portfolio/
├── index.html    # Complete portfolio (single file)
└── README.md     # This file
```

## Customization

All styling uses CSS custom properties at the top of `index.html`. Change colors, fonts, or spacing by editing the `:root` block.

---

Built by Akshay Dixit · 2026
