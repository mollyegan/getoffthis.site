# getoffthis.site (GitHub Pages)

This repository is published with GitHub Pages and uses the custom domain: `getoffthis.site`.

What I added
- A `CNAME` file (one line: `getoffthis.site`) that tells GitHub Pages to serve the site at your custom domain.
- A `README.md` with NameSilo DNS setup steps and verification/troubleshooting notes.

Step-by-step: connect NameSilo domain to GitHub Pages

1) Add the custom domain to the repository (one of these):
   - GitHub: Repository → Settings → Pages → Custom domain: enter `getoffthis.site` and Save.
   - OR add a file named `CNAME` in the repository root containing exactly:
     getoffthis.site

2) Configure DNS at NameSilo (Domain Manager → Manage → DNS Records / Host Records)
   - For the apex/root domain (`getoffthis.site`) add four A records:
     - Host: @   Type: A  Value: 185.199.108.153
     - Host: @   Type: A  Value: 185.199.109.153
     - Host: @   Type: A  Value: 185.199.110.153
     - Host: @   Type: A  Value: 185.199.111.153
   - For the `www` subdomain (optional, recommended) add:
     - Host: www   Type: CNAME  Value: mollyegan.github.io
   - Do NOT create a CNAME at the apex/root. Remove any conflicting records.

3) Wait for DNS to propagate (minutes to hours). Verify with these commands:
   - dig +short getoffthis.site A
   - dig +short www.getoffthis.site CNAME
   - curl -I https://getoffthis.site

4) Enable HTTPS in GitHub Pages settings:
   - Once DNS is correct GitHub will provision a TLS certificate (Let's Encrypt). In Settings → Pages, enable “Enforce HTTPS” when available.

Notes & troubleshooting
- If you use Cloudflare, set the records to DNS-only (grey cloud). Proxying (orange cloud) prevents GitHub from issuing certificates.
- If HTTPS never issues: double-check DNS records and that there are no proxies; re-enter the custom domain in Pages settings if needed.
- If you see GitHub’s "There isn't a GitHub Pages site here" page, DNS is not pointing to GitHub Pages or the Pages source branch isn't published.

If you'd like, I can also add a redirect for `www` to the apex by setting the Pages custom domain to `getoffthis.site` (GitHub will redirect `www` automatically if `www` points to mollyegan.github.io).