# Deploying i4one.com on GitHub Pages

Step-by-step to take this static site live at the apex domain **i4one.com** with
free HTTPS. Nothing here requires a secret or a `.env` — a static site has none.

---

## 0. Prerequisites
- A GitHub account (note your **username** — call it `<USER>`).
- Access to the **DNS panel** for `i4one.com` (your domain registrar).

---

## 1. Create the public repo on GitHub
Create a new **public** repo named `i4one-site` (any name works; the custom
domain is what visitors see). Do **not** add a README/license on creation — this
folder already has them.

## 2. Push this folder
This folder is already a git repo with an initial commit. Add the remote and push:

```bash
cd I:/GitHub/i4one-site
git remote add origin https://github.com/<USER>/i4one-site.git
git branch -M main
git push -u origin main
```

## 3. Enable GitHub Pages
Repo → **Settings → Pages**:
- **Source:** "Deploy from a branch"
- **Branch:** `main`, folder `/ (root)` → **Save**

GitHub publishes at `https://<USER>.github.io/i4one-site/` within a minute.

## 4. Bind the custom domain (apex)
Still in **Settings → Pages → Custom domain**, enter `i4one.com` → **Save**.
(The `CNAME` file in this repo already contains `i4one.com`, so this should
auto-populate.)

## 5. Add DNS records at your registrar
Create these records for `i4one.com`:

**A records** (host `@` / apex):
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**AAAA records** (host `@` / apex — IPv6, recommended):
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**CNAME record** (host `www`) → `<USER>.github.io`
GitHub will redirect `www.i4one.com` → `i4one.com` automatically.

> DNS can take from minutes to a few hours to propagate. Check with:
> `nslookup i4one.com` (should return the four GitHub IPs).

## 6. Enforce HTTPS
Back in **Settings → Pages**, once GitHub finishes provisioning the certificate
(may take up to ~24h after DNS resolves), tick **Enforce HTTPS**. You now have
`https://i4one.com` with a valid padlock.

## 7. Verify the domain with Google (for credits + OAuth)
- Go to **Google Search Console** → add property `i4one.com` (Domain property).
- Add the **TXT record** it gives you to your DNS, then click Verify.
- This verified domain is what Google's OAuth verification and credit programs
  reference. Your privacy policy URL will be `https://i4one.com/privacy.html`.

---

## Going-live checklist
- [ ] `https://i4one.com` loads with a valid TLS padlock
- [ ] `https://www.i4one.com` redirects to the apex
- [ ] "Enforce HTTPS" is enabled
- [ ] Privacy + Terms reachable from the footer (reviewers click these)
- [ ] Privacy policy placeholders replaced with **accurate** OAuth scopes/storage
- [ ] Domain verified in Google Search Console

## Updating the site later
Edit files, then:
```bash
git add -A && git commit -m "update site" && git push
```
GitHub Pages redeploys automatically on push to `main`.
