# Flash Linux packages

Binary packages for [Flash Linux](https://github.com/Isakarbast/flash-linux),
installed with fpm (Flash Package Manager). The packages live in the
[`x86_64` release](https://github.com/Isakarbast/flash-packages/releases/tag/x86_64),
not in the git tree: GitHub's release files can be up to 2 GB, git files only 100 MB.

The index (`index.fpm.zst`) is signed with the Flash ed25519 key, and fpm
checks every package's sha256 against it, so a tampered download is refused.

## Using it

Add this to `/etc/fpm.conf` on a Flash system (installs from the ISO already
have the key at `/etc/fpm/keys/flash-iso.pub`):

```
[repo flash]
url = https://github.com/Isakarbast/flash-packages/releases/download/x86_64
key = /etc/fpm/keys/flash-iso.pub
```

Then:

```
fpm sync
fpm install <package>
```

## Updating (maintainer)

In the build environment:

```
fpm index DIR --sign /etc/fpm/keys/flash-iso.key
gh release upload x86_64 DIR/<new packages> DIR/index.fpm.zst DIR/index.fpm.zst.sig --clobber
```

The release holds only the newest version of each package.
