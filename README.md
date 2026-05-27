# keskos-calamares-branding

`keskos-calamares-branding` packages the KeskOS Calamares theme, installer configuration, and post-install helper scripts.

## What this is

This repository builds the package that makes Calamares look and behave like the KeskOS installer, including branding assets, module configuration, desktop launchers, package manifests, and post-install hooks.

## Role in KeskOS

Installer package.

## Package name

```txt
Package: keskos-calamares-branding
Repo: [keskos]
Architecture: any
```

## What it installs or provides

- Installs branding under `/usr/share/calamares/branding/keskos`.
- Installs Calamares configuration under `/etc/calamares/settings.conf` and `/etc/calamares/modules/*.conf`.
- Installs the custom module at `/usr/lib/calamares/modules/keskoschoices/`.
- Installs helper scripts `/usr/lib/keskos-installer/apply-install-choices.sh`, `/usr/local/bin/keskos-open-installer`, `/usr/local/bin/keskos-postinstall-root`, and `/usr/local/bin/keskos-prepare-target-root`.
- Installs launchers `install-keskos.desktop` and `Install KeskOS.desktop`, plus `/usr/share/keskos/installer/package-manifest.json`.

## Commands and launchers

- `keskos-open-installer` launches Calamares with KeskOS logging and failure handling.
- `keskos-postinstall-root` applies post-install repo, user-default, and package-choice logic inside the target system.
- `keskos-prepare-target-root` stages target-root configuration before final install steps.
- GUI launcher installed: `install-keskos.desktop`.

## Config, logs, and state

- Calamares settings and module files live under `/etc/calamares/` after install.
- Installer session logs are written to `${XDG_CACHE_HOME:-$HOME/.cache}/keskos/calamares-installer.log` by `keskos-open-installer`.
- The install flow can record service presets for `bluetooth.service`, `cups.service`, and `docker.service`, and the Calamares `services-systemd` module enables core units such as `NetworkManager.service` and `sddm.service` on the target system.

## Dependencies

- Runtime dependencies: `calamares`, `jq`, `kdialog`, `konsole`, `python`, `rsync`, `sudo`, and `xdg-utils`.
- The package relies on Calamares module loading and the package manifest it ships under `/usr/share/keskos/installer/`.
- Build with `makepkg -s --noconfirm` in this repo.

## Build

```bash
makepkg -s --noconfirm
```

## Packaging notes

- This repo owns installer behavior only; it should not become the source of unrelated desktop or app functionality.
- Package-choice logic should stay aligned with the rest of the KeskOS package repos and first-boot flows.

## Troubleshooting

- If Calamares fails to launch or exits early, inspect `${XDG_CACHE_HOME:-$HOME/.cache}/keskos/calamares-installer.log`.
- If post-install package/application choices were not applied, inspect the packaged manifest and `apply-install-choices.sh` on the installed target system.
- If a service is not enabled after install, check both the Calamares `services-systemd` configuration and any generated system preset snippets.

## Docs website export notes

- Good website split: installer overview, helper-command reference, package-choice flow, and troubleshooting/log paths.
- Keep launcher names and helper paths stable so website docs can reference them directly.
