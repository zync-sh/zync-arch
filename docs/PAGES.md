# Enabling GitHub Pages for zync-arch

## First-time bootstrap

If `gh-pages` does not exist yet, create it once:

```bash
git checkout --orphan gh-pages
git rm -rf .
mkdir -p x86_64
echo 'arch.zync.thesudoer.in' > CNAME
echo 'Zync Arch repo — packages appear here after the next zync release.' > index.html
touch x86_64/.gitkeep
git add CNAME index.html x86_64/.gitkeep
git commit -m "chore: bootstrap gh-pages for Arch pacman repo"
git push -u origin gh-pages
git checkout main
```

Then in GitHub → **Settings → Pages**:

- Branch: `gh-pages`
- Custom domain: `arch.zync.thesudoer.in`
- Enforce HTTPS when available

## DNS

| Type | Name | Target |
|------|------|--------|
| CNAME | `arch` | `gajendraxdev.github.io` |

No Cloudflare path/Host rewrite is required when this repo owns the `arch` domain.
