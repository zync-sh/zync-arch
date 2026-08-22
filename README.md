# zync-arch

Official **Arch Linux / pacman** repository for [Zync](https://github.com/zync-sh/zync).

Application source and releases live in **`zync-sh/zync`**.  
This repo only hosts the signed pacman package database and `.pkg.tar.zst` files (GitHub Pages).

Packages are GPG-signed with the same packaging key as the APT repo (`releases@zync.thesudoer.in`).

## Install

```bash
# 1. Import and locally sign the Zync packaging key
curl -fsSL https://arch.zync.thesudoer.in/key.gpg -o /tmp/zync.gpg
sudo pacman-key --add /tmp/zync.gpg
FPR="$(gpg --show-keys --with-colons /tmp/zync.gpg 2>/dev/null | awk -F: '/^fpr:/ { print $10; exit }')"
sudo pacman-key --lsign-key "$FPR"

# 2. Add the repo
sudo tee /etc/pacman.d/zync.conf >/dev/null <<'EOF'
[zync]
SigLevel = Required TrustedOnly
Server = https://arch.zync.thesudoer.in/$arch
EOF

grep -q 'pacman.d/zync.conf' /etc/pacman.conf || \
  echo 'Include = /etc/pacman.d/zync.conf' | sudo tee -a /etc/pacman.conf

# 3. Install
sudo pacman -Syu zync
```

**Upgrade:** `sudo pacman -Syu`  
**Remove:** `sudo pacman -R zync`

Updates go through pacman (not the in-app AppImage updater).

## Pages layout (`gh-pages`)

```text
CNAME                 → arch.zync.thesudoer.in
key.gpg               → public packaging key
x86_64/
  zync-*-x86_64.pkg.tar.zst
  zync-*-x86_64.pkg.tar.zst.sig
  zync.db.tar.zst
  zync.db.tar.zst.sig
  …
```

Published automatically from the `zync` release workflow after each tagged release.

## One-time GitHub setup

See [docs/PAGES.md](./docs/PAGES.md).

## License

MIT — same as Zync. See [zync/LICENSE](https://github.com/zync-sh/zync/blob/main/LICENSE).
