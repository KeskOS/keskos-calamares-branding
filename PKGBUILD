pkgname=keskos-calamares-branding
pkgver=0.1.0
pkgrel=1
pkgdesc="KeskOS Calamares branding, installer configs, and post-install helpers"
arch=(any)
url="https://github.com/memegeko/keskos"
license=(GPL-3.0-or-later)
depends=(
  calamares
  jq
  kdialog
  konsole
  python
  rsync
  sudo
  xdg-utils
)
backup=(
  etc/calamares/settings.conf
  etc/calamares/modules/bootloader.conf
  etc/calamares/modules/displaymanager.conf
  etc/calamares/modules/finished.conf
  etc/calamares/modules/keskos-review.conf
  etc/calamares/modules/keskoschoices.conf
  etc/calamares/modules/keyboard.conf
  etc/calamares/modules/locale.conf
  etc/calamares/modules/mount.conf
  etc/calamares/modules/packages.conf
  etc/calamares/modules/partition.conf
  etc/calamares/modules/postinstall.conf
  etc/calamares/modules/prepare-target.conf
  etc/calamares/modules/services-systemd.conf
  etc/calamares/modules/unpackfs.conf
  etc/calamares/modules/users.conf
)
source=()
sha256sums=()

package() {
  local srcroot="${startdir}/files"

  install -d "${pkgdir}/usr/share/calamares/branding"
  cp -a "${srcroot}/calamares/branding/keskos" "${pkgdir}/usr/share/calamares/branding/"

  install -D -m 644 "${srcroot}/calamares/settings.conf" "${pkgdir}/etc/calamares/settings.conf"
  while IFS= read -r module_file; do
    install -D -m 644 "${module_file}" "${pkgdir}/etc/calamares/modules/$(basename "${module_file}")"
  done < <(find "${srcroot}/calamares/modules" -maxdepth 1 -type f -name '*.conf' | sort)

  install -D -m 644 "${srcroot}/airootfs/usr/lib/calamares/modules/keskoschoices/module.desc" "${pkgdir}/usr/lib/calamares/modules/keskoschoices/module.desc"
  install -D -m 755 "${srcroot}/airootfs/usr/lib/calamares/modules/keskoschoices/main.py" "${pkgdir}/usr/lib/calamares/modules/keskoschoices/main.py"
  install -D -m 755 "${srcroot}/airootfs/usr/lib/keskos-installer/apply-install-choices.sh" "${pkgdir}/usr/lib/keskos-installer/apply-install-choices.sh"

  install -D -m 755 "${srcroot}/airootfs/usr/local/bin/keskos-open-installer" "${pkgdir}/usr/local/bin/keskos-open-installer"
  install -D -m 755 "${srcroot}/airootfs/usr/local/bin/keskos-postinstall-root" "${pkgdir}/usr/local/bin/keskos-postinstall-root"
  install -D -m 755 "${srcroot}/airootfs/usr/local/bin/keskos-prepare-target-root" "${pkgdir}/usr/local/bin/keskos-prepare-target-root"

  install -D -m 644 "${srcroot}/airootfs/usr/share/keskos/installer/package-manifest.json" "${pkgdir}/usr/share/keskos/installer/package-manifest.json"
  install -D -m 644 "${srcroot}/airootfs/usr/share/applications/install-keskos.desktop" "${pkgdir}/usr/share/applications/install-keskos.desktop"
  install -D -m 644 "${srcroot}/airootfs/etc/skel/Desktop/Install KeskOS.desktop" "${pkgdir}/etc/skel/Desktop/Install KeskOS.desktop"
}
