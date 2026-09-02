# Deploying protosunsolutions.com

Static site. No build step, no dependencies, no framework. Free to host.

## Files

```
index.html          the entire site
wordmark-light.png  header logo
mark.png            sunburst, navy/gold
mark-light.png      sunburst, white/gold (spare)
favicon.png         browser tab icon
```

Everything is in one folder. `index.html` contains all CSS inline, so there is nothing to
compile and nothing that can break from a missing dependency.

---

## Step 1 — GitHub repository

1. Create a new **public** repository. Name it anything (`protosun-site` is fine).
2. Upload all five files to the repository root — not into a subfolder.
3. Go to **Settings → Pages**.
4. Under *Build and deployment*, set **Source** to `Deploy from a branch`.
5. Set branch to `main` and folder to `/ (root)`. Save.

Within a minute or two GitHub will publish the site at
`https://<your-username>.github.io/<repo-name>/`. Confirm it loads before moving on.

**Note:** the repository must be public for GitHub Pages on a free account.
Nothing in these files is sensitive, so that is fine.

---

## Step 2 — Point the domain at it

You already own `protosunsolutions.com` and use Cloudflare for DNS.

### In GitHub

1. **Settings → Pages → Custom domain**
2. Enter `protosunsolutions.com` and save.
3. This creates a `CNAME` file in your repository. Leave it there.

### In Cloudflare DNS

Add these records. **Set the proxy status to "DNS only" (grey cloud) at first** —
Cloudflare's orange-cloud proxy interferes with GitHub's certificate issuance.

| Type  | Name | Content                    | Proxy    |
|-------|------|----------------------------|----------|
| A     | @    | 185.199.108.153            | DNS only |
| A     | @    | 185.199.109.153            | DNS only |
| A     | @    | 185.199.110.153            | DNS only |
| A     | @    | 185.199.111.153            | DNS only |
| CNAME | www  | `<username>.github.io`     | DNS only |

### Then

1. Wait for DNS to propagate — usually minutes, occasionally an hour.
2. Back in **GitHub → Settings → Pages**, check the box for **Enforce HTTPS**.
   This may be greyed out until GitHub finishes issuing the certificate. Wait and retry.
3. Once HTTPS works, you may switch Cloudflare back to proxied (orange cloud) if you want
   Cloudflare's caching and analytics. Set Cloudflare SSL/TLS mode to **Full** if you do.

---

## Step 3 — Verify

- `https://protosunsolutions.com` loads with a valid certificate
- `https://www.protosunsolutions.com` redirects correctly
- The padlock appears in the browser — no mixed-content warnings

---

## Editing later

Open `index.html`, change the text, commit. GitHub Pages redeploys automatically within
about a minute. There is no build to run.

Common edits:

- **Contact details** — search for `michael.potter@protosunsolutions.com`
- **Headline** — search for `Something`
- **Section text** — each section is marked with an HTML comment
- **Colors** — the `:root` block at the top of the `<style>` section defines every color once

---

## Deliberately not included

- **No contact form.** Forms need a backend and invite spam. A `mailto:` link is
  appropriate for this audience and cannot break.
- **No analytics.** Add later if you want it. Government visitors often block trackers anyway.
- **No technical specifications.** See the note below.

---

## One caution before you add content

Keep the site at capability-statement level: what the company does, what it delivers,
who the team is, how to make contact.

**Do not publish technical specifications, performance data, drawings, or system
architecture detail.** Once the export jurisdiction determination comes back, some of
that material is likely to be controlled technical data, and a public website is a
publication to the world. What is here now is safe. Anything more detailed should wait
for the attorney's opinion.
