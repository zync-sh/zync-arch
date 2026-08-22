# zync-arch

Official **Arch Linux / pacman** repository for [Zync](https://github.com/zync-sh/zync).

Application source and releases live in **`zync-sh/zync`**.  
This repo only hosts the pacman package database and `.pkg.tar.zst` files (GitHub Pages).

## Install

```bash
sudo tee /etc/pacman.d/zync.conf >/dev/null <<'EOF'
[zync]
SigLevel = Optional TrustAll
Server = https://arch.zync.thesudoer.in/$arch
EOF

grep -q 'pacman.d/zync.conf' /etc/pacman.conf || \
  echo 'Include = /etc/pacman.d/zync.conf' | sudo tee -a /etc/pacman.conf

sudo pacman -Syu zync
```

**Upgrade:** `sudo pacman -Syu`  
**Remove:** `sudo pacman -R zync`

Updates go through pacman (not the in-app AppImage updater).

## Pages layout (`gh-pages`)

```text
CNAME                 → arch.zync.thesudoer.in
x86_64/
  zync-<ver>-1-x86_64.pkg.tar.zst
  zync.db
  zync.db.tar.zst
  zync.files
  zync.files.tar.zst
```

Published automatically from the `zync` release workflow after each tagged release.

## One-time GitHub setup

1. **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: **`gh-pages`** / `/ (root)`
2. **Custom domain:** `arch.zync.thesudoer.in`
3. DNS: `CNAME arch` → `gajendraxdev.github.io` (or your Pages target), Proxied optional
4. Ensure the release PAT (`RELEASE_TOKEN` in `zync`) can push to this repo

## License

MIT — same as Zync. The packaged application is MIT; see [zync/LICENSE](https://github.com/zync-sh/zync/blob/main/LICENSE).
