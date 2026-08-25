# Adams David, portfolio site

A single-page personal portfolio. Everything lives in `index.html`: the markup, the
styles, the JavaScript, and the portrait, which is embedded as a data URI. There is
no build step and no dependencies, so the file you open locally is byte for byte the
file that gets served.

## Deploying to Vercel

Two ways. Pick one.

### Option A, straight from this folder (fastest)

Open a terminal in this folder and run:

```
npx vercel login
npx vercel --prod
```

The first command opens your browser to sign in. The second uploads the folder and
prints your live URL. To publish a change later, run `npx vercel --prod` again.

### Option B, through GitHub (recommended)

Slower to set up once, then every push deploys itself. Create a new empty repository
on GitHub first, then:

```
git init
git add .
git commit -m "Portfolio site"
git branch -M main
git remote add origin https://github.com/DAMMMZZZYYY/<repo-name>.git
git push -u origin main
```

Then go to vercel.com/new, import that repository, and hit Deploy. Leave every build
setting on its default, Vercel serves static files as they are. From then on, any
`git push` redeploys the site automatically.

Note you already have a repo called `cybersecurity-portfolio`. Give this one a
different name, such as `portfolio`, so the two do not get confused.

## What is in here

| File | Purpose |
| --- | --- |
| `index.html` | The entire site |
| `vercel.json` | Security response headers and caching rules |
| `.gitignore` | Keeps `.vercel` and local junk out of the repo |

## About vercel.json

The site ships with a real Content Security Policy rather than a permissive one. The
CSS and JS are inline, which normally forces you into `'unsafe-inline'`, so instead
each block is hashed with SHA-256 and the hashes are named in the policy. The browser
runs those two exact blocks and refuses anything else that gets injected.

That means the hashes must match the file. **If you hand-edit the `<style>` or
`<script>` block in `index.html`, the hashes in `vercel.json` go stale and the page
will load with no styling and no JavaScript.** Recompute them, or ask Claude to
rebuild both files together.

Also set: HSTS, `nosniff`, `frame-ancestors 'none'` so the page cannot be framed,
a locked down `Permissions-Policy`, and `strict-origin-when-cross-origin` referrers.

## Adding your CV

The Download CV button points at `cv.pdf` next to `index.html`. Drop a file with
that exact name into this folder and the button starts working. Until then it
resolves to nothing.

## Custom domain

In the Vercel dashboard, Settings, Domains. You already own `nythen.com`, so
something like `adams.nythen.com` would work, or point a separate domain at it.
