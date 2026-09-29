# kde-shell

SDDM-free KDE Plasma Wayland session package layer for OpenCharly images.

The `kde-shell` candy installs the shared KDE Plasma Wayland session package set
used by **both** KDE consumers, so the package list is defined once:
`plasma-desktop` (the dependency-pulling top package, which drags
`plasma-workspace` + `kwin_wayland` + `plasmashell` + kf6 + qt6 + breeze) plus
`xorg-xwayland`, the core session components, a curated app set usable in both
venues, and the `kdotool` KWin automation tool (AUR) that backs the `wl:` check
verb on KWin.

The bare-metal KDE desktop (`kde-desktop`) composes this layer and adds SDDM +
workstation-only extras; the headless streamed KDE pod (`kde-selkies`) composes
it without a display manager.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `kde-shell` |
| Requires | `pod-dbus` |
| Packages (arch) | `plasma-desktop`, `xorg-xwayland`, `plasma-pa`, `plasma-nm`, `powerdevil`, `kscreen`, `kde-gtk-config`, `breeze-gtk`, `kdialog`, `kio-admin`, `ark`, `dolphin`, `konsole`, `kate`, `kcalc`, `gwenview`, `spectacle` |
| AUR (arch) | `kdotool` |
| Install files | `charly.yml` (packages only) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-kde:
  candy:
    base: cachyos
    candy:
      - '@github.com/opencharly/layer-kde-shell:v2026.239.1627'
```

The headless consumer runs `startplasma-wayland` nested in pixelflux; the
bare-metal consumer adds `sddm` and `systemctl set-default graphical.target`.

## Layout

- `charly.yml` — the `kde-shell:` candy entity: the `pod-dbus` require, the
  `distro:` package/AUR sections, the `check:` assertions, and the embedded
  `skill:` entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:kde-shell` — the SDDM-free Plasma session leaf
- Bare-metal consumer: `opencharly/pod-kde-desktop` (the `kde-desktop` candy)
- Headless streamed consumer: `/charly-selkies:kde-selkies`
- KWin automation verb: `/charly-check:wl`
- Base: `/charly-distros:cachyos`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
