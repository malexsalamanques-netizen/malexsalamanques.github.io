# Publishing malexsalamanques.com

Two HTML files, one GitHub repo, one DNS change at GoDaddy. About 20 minutes of active work, plus 15 minutes to 24 hours of waiting for DNS to propagate.

---

## Part 1 — Upload the site to GitHub

### 1. Create a GitHub account
If you don't already have one, sign up at github.com. Pick a username you don't mind appearing in URLs. Something close to your name is best (e.g. `malexsalamanques`).

### 2. Create the repository
Once signed in, click the green **New** button (top left of the page, next to "Repositories").

Fill in:
- **Repository name:** `yourusername.github.io` (replace `yourusername` with the exact username you chose). This naming matters because GitHub treats a repo with this exact name as your personal site.
- **Public** (must be public for free Pages hosting).
- Tick **Add a README file**.
- Leave everything else as default.

Click **Create repository**.

### 3. Upload both HTML files
On the repository page, click **Add file → Upload files**.

Drag these two files in (from your computer):
- `index.html`
- `signals-in-context.html`

Both must sit at the root of the repo, not in a subfolder. The article page links to `index.html` and the homepage links to `signals-in-context.html`, so they need to be siblings.

Scroll down, type a commit message like "initial site", and click **Commit changes**.

### 4. Turn on GitHub Pages
In the repo, click **Settings** (top nav).

In the left sidebar, click **Pages**.

Under "Build and deployment → Source", set it to **Deploy from a branch**.

Under "Branch", select **main** and **/ (root)**, then click **Save**.

Wait one to three minutes. Your site will go live at `https://yourusername.github.io`. Visit it to confirm it works before connecting your custom domain.

---

## Part 2 — Point malexsalamanques.com at the site

This is where the GoDaddy side comes in. You need to tell GoDaddy "send visitors of malexsalamanques.com to GitHub's servers." It's done by editing DNS records.

### 5. Open your GoDaddy DNS panel
1. Sign in to GoDaddy.
2. Click your name (top right) → **My Products**.
3. Find `malexsalamanques.com` in your domain list and click **DNS** next to it.

You'll see a table of DNS records. GoDaddy will have created a few by default. You're going to edit two of them and add several more.

### 6. Edit the A records (for the apex domain)
The "apex" domain is `malexsalamanques.com` with no `www.` in front. GitHub Pages requires four A records for the apex, pointing to their IP addresses.

In GoDaddy:
1. Find the existing **A record** with **Name: @**. Click the pencil/edit icon next to it.
2. Change its **Value/Points to** to: `185.199.108.153`
3. Save.

Now add three more A records (click **Add New Record** or similar):
- Type: **A**, Name: **@**, Value: `185.199.109.153`
- Type: **A**, Name: **@**, Value: `185.199.110.153`
- Type: **A**, Name: **@**, Value: `185.199.111.153`

You should end up with four A records all named `@`, each pointing to one of those four IPs.

### 7. Edit the www CNAME
Find the existing **CNAME** record with **Name: www**. Click edit.
- Change its **Value/Points to** to: `yourusername.github.io` (use your actual GitHub username, keep the `.github.io` suffix).
- Save.

If no CNAME for `www` exists, add one:
- Type: **CNAME**, Name: **www**, Value: **yourusername.github.io**

### 8. Tell GitHub about the custom domain
Back in your GitHub repo:
1. Go to **Settings → Pages**.
2. Under "Custom domain", type `malexsalamanques.com` and click **Save**.

GitHub will check your DNS. The first check often fails because DNS hasn't propagated yet. Come back in 15 minutes to a few hours and refresh the Pages settings page. When the check passes, a green tick appears.

### 9. Turn on HTTPS
Once GitHub's DNS check passes, the **Enforce HTTPS** checkbox unlocks at the bottom of the Pages settings. Tick it. GitHub will issue a free SSL certificate for `malexsalamanques.com`. Your site is now live at:

**`https://malexsalamanques.com`**

---

## What to do if something breaks

**"DNS check failed" in GitHub Pages settings.**
Wait longer. DNS propagation can take up to 24 hours, though usually it resolves in 1 to 2 hours. Come back later and click "Check again."

**Site loads but shows a 404.**
Make sure `index.html` is at the root of the repo (not inside a folder). Click around your repo to verify.

**Site works at github.io but not at the custom domain.**
Check that you saved all four A records and that the www CNAME points to `yourusername.github.io` (not `yourusername.github.io.com` or similar). GoDaddy sometimes silently appends `.com` if you're not careful.

**HTTPS checkbox is greyed out.**
The DNS check must pass first. Wait, then refresh.

---

## Updating the site later

Two routes:

**In the browser.** Open the file in your repo (e.g. `index.html`), click the pencil icon, edit, scroll to the bottom and commit. The live site updates within a minute.

**Local editing.** Edit the file in any text editor on your computer. Drag the new version back into the repo via **Add file → Upload files → "Replace the existing file"**.

If you want me to make edits, paste the text you want changed and I'll send you back updated files.

---

## A note on costs

GitHub Pages: free, including HTTPS.
GoDaddy domain: whatever you paid (~$15-$20/year for renewals).
Total recurring cost: just the domain.
