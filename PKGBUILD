# Maintainer : kilso <asderuiner@gmail.com> 

_pkgname=efa2
pkgname=${_pkgname}-bin
pkgver=240
arch=(any)
_url_base="http://efa.nmichael.de"
url="$_url_base/efa.html.en"
license=("GPL-2.0-or-later")
provides=('efa2')
conflicts=('efa2')
pkgrel=1
epoch=1
depends=(
    'sh'
    'java-runtime>7'
)
makedepends=('unzip')
pkgdesc="Electronic Logbook for Rowing and Canoeing"
_src_name="efa$pkgver.zip"
source=(
    "$_url_base/download/$_src_name"
)
sha256sums=(
    '589afa0ec3c4bc0e9e15b82299b52b5a297539bfdfb8db3c62966683b86cca6c'
)
_install_dir="/usr/share/${_pkgname}"


build() {
    cat >efa2-base <<EOL
#!/bin/sh
cd ${_install_dir} && sh ./efaBase.sh
EOL
    cat >efa2-boathouse <<EOL
#!/bin/sh
cd ${_install_dir} && sh ./efaBths.sh
EOL
    cat >efa2-cli <<EOL
#!/bin/sh
cd ${_install_dir} && sh ./efaCLI.sh
EOL
    desktop_file_fmt=$(cat <<EOL
[Desktop Entry]
Type=Application
Exec=%s
#Icon=efa
Categories=Office;ProjectManagement;

Name=efa2 %s
Comment=${pkgdesc}
StartupNotify=true
StartupWMClass=EFA2

EOL
)
    printf "${desktop_file_fmt}" efa2-base "for private use" > efa2-base.desktop
    printf "${desktop_file_fmt}" efa2-boathouse "for boathouse use" > efa2-boathouse.desktop
}

package() {
    unzip -o ./$_src_name -d efa

    install -Dm 644 efa2-base.desktop -t "${pkgdir}/usr/share/applications"
    install -Dm 644 efa2-boathouse.desktop -t "${pkgdir}/usr/share/applications"

    install -Dm 755 efa2-base -t "${pkgdir}/usr/bin"
    install -Dm 755 efa2-boathouse -t "${pkgdir}/usr/bin"
    install -Dm 755 efa2-cli -t "${pkgdir}/usr/bin"

    install -Dm 644 efa/efa.ico -t "${pkgdir}/usr/share/icons/${_pkgname}"
    install -Dm 644 efa/efa.ico -t "${pkgdir}${_install_dir}"

    install -Dm 755 efa/runefa.sh -t "${pkgdir}${_install_dir}"
    install -Dm 755 efa/efaBase.sh -t "${pkgdir}${_install_dir}"
    install -Dm 755 efa/efaBths.sh -t "${pkgdir}${_install_dir}"
    install -Dm 755 efa/efaCLI.sh -t "${pkgdir}${_install_dir}"
    install -Dm 755 efa/emil.sh -t "${pkgdir}${_install_dir}"

    mv efa/cfg "${pkgdir}${_install_dir}"
    mv efa/doc "${pkgdir}${_install_dir}"
    mv efa/program "${pkgdir}${_install_dir}"

    install -Dm 644 efa/COPYING.TXT -t "${pkgdir}/usr/share/licenses/${_pkgname}"
}
