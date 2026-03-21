# ZeroWire Robotics — Site

Static landing page for [ZeroWire Robotics](https://zerowirerobotics.com) (Yufeng Wu DBA ZeroWire Robotics).

---

## Current state

Minimal "coming soon" page. Search-engine indexing is intentionally disabled via `<meta name="robots" content="noindex, nofollow">` while the site is in soft-launch.

---

## Deployment: GitHub Pages + Squarespace DNS

### 1. Enable GitHub Pages

1. Go to your repo → **Settings → Pages**.
2. Under **Source**, select **Deploy from a branch**.
3. Choose `main` branch, `/ (root)` folder. Save.
4. GitHub will publish the site and show you a `github.io` URL. Ignore it — you'll use your custom domain.

The `CNAME` file in the repo root already contains `zerowirerobotics.com`, so GitHub Pages will automatically associate that domain once DNS is pointed correctly.

### 2. Configure DNS in Squarespace

In **Squarespace Domains → DNS Settings** for `zerowirerobotics.com`, add the following records:

**A records** (apex domain → GitHub Pages IPs):

| Type | Host | Value            |
|------|------|-----------------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |

**CNAME record** (www subdomain):

| Type  | Host | Value                        |
|-------|------|------------------------------|
| CNAME | www  | `<your-github-username>.github.io` |

Replace `<your-github-username>` with your actual GitHub username (e.g. `ericwu17.github.io`).

> DNS propagation typically takes 10–30 minutes, sometimes up to 24 hours.

### 3. Enable HTTPS in GitHub Pages

Once DNS propagates, go back to **Settings → Pages** and check **Enforce HTTPS**. GitHub will auto-provision a Let's Encrypt certificate.

### 4. Verify

Visit `https://zerowirerobotics.com` — you should see the landing page. Confirm the padlock is shown (HTTPS active).

---

## Keeping the site "soft private"

The site is live but intentionally invisible to search engines:

- `<meta name="robots" content="noindex, nofollow">` is set in `index.html` — crawlers that respect this tag will not index the page.
- No social preview tags, no sitemap, no external links.
- The URL is only shared with people you send it to directly.

> This does **not** password-protect the site. If you need that, consider Cloudflare Access (free tier) or a Netlify password page instead of GitHub Pages.

---

## Future product pages

ZeroWire Robotics is planned as a home for multiple projects over time. Anticipated structure:

```
/                          ← this landing page (always up to date)
/products/q8bot-cs/        ← Q8bot Crowd Supply Version
    component-sourcing/
    assembly/
    software-setup/
/products/q9bot-legacy/    ← Q9bot Legacy Version (IROS open-source release)
    ...
```

**Notes for future expansion:**

- **Q8bot Crowd Supply Version** is the first product. It will need: component sourcing guide, PCB assembly instructions, and software setup (firmware flash, ROS2 setup, etc.). Consider whether the Crowd Supply campaign page handles the BOM or whether this site should mirror it.
- **Q9bot Legacy Version** is not a Crowd Supply project — it is the original open-source design published at IROS. Keep it clearly labeled as "legacy / open source" to avoid confusion with the CS campaign. A simple GitHub-link page may be sufficient.
- Future robots that are purely open-source (no crowdfunding) can follow the Q9bot pattern: lightweight doc pages with links to repos, papers, and BOM.
- Consider using a consistent URL convention: `/products/<name>-<variant>/` so the nav scales cleanly.
- When the site gains real content, remove the `noindex` meta tag and set up proper SEO (Open Graph, Twitter card, canonical URLs).
