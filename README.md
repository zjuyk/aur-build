# aur-build

## build aur and self-host packages

For PKGBUILDs which have no dependencies in AUR:

Using `Ducksoft/build-aur-action`

- Use `sed -i '/E_ROOT/d' /usr/bin/makepkg` to hack makepkg which can not run via root for security reason.
- Git clone packages git repo from AUR and just makepkg

Finally, upload the *.zst to release via `ncipollo/release-action`

For PKGBUILDs which have dependencies in AUR:

Using `edlanglois/pkgbuild-action`

- Add a new user `builder` and give it passwordless sudo access
- Install yay and use it to install dependencies in AUR
- Check packages via namcap

Hint: It will obtain packagelist via `makepkg --packagelist`, so you should make a dir with package name and put PKGBUILD in it.

Finally, upload the *.zst to release via `ncipollo/release-action`

## Download releases via command line
```bash
curl -s https://api.github.com/repos/zjuyk/aur-build/releases/latest | \
        rg browser_download_url | \
        cut -d : -f 2,3 | \
        tr -d \" | \
        xargs -n 1 curl -O -sSL
```

## Download releases via public repo

You can vist my public repo on keybase: [here](https://zjuyk.keybase.pub)
My GPG fingerprint: [B3A9 251F BEA2 1298 B80B  7F9E F84D 36A7 3BF3 9DC8](https://github.com/zjuyk.gpg)
