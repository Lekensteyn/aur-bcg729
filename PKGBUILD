# Maintainer: Christian Kohlstedde <christian+arch-pkg@kohlsted.de>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Peter Wu <peter@lekensteyn.nl>

pkgname=bcg729
pkgver=1.0.4
pkgrel=3
pkgdesc="G.729 codec"
arch=('x86_64')
url="https://www.linphone.org/technical-corner/bcg729/overview"
license=('GPL2')
makedepends=('cmake')
depends=('glibc')
source=("https://github.com/BelledonneCommunications/bcg729/archive/${pkgver}/bcg729-${pkgver}.tar.gz"
        "cmake-symbol-visibility.patch::https://github.com/Lekensteyn/bcg729/commit/5e70712297ad2df58a035728da07c440c8ab5fcf.patch"
        "cmake-install-pkgconfig.patch::https://github.com/Lekensteyn/bcg729/commit/58e60cff7fd5829f26fcf6d7b4d80de440b1b151.patch")
sha256sums=('94b3542a06cbd96306efc19f959f9febae62806a22599063f82a8c33e989d48b'
            '6696d6f3a768a6ad1c3f48439ae26a1f7cda170b010095032cd391efe457deff'
            '22292952b6c7db426cec99bcabac87ef8b4b2bc8f4ef3c43924578878f59ce68')

prepare() {
  cd $pkgname-$pkgver
  # CMake build fixes https://github.com/BelledonneCommunications/bcg729/pull/7
  # cmake: fix symbol visibility
  patch -p1 -i "${srcdir}/cmake-symbol-visibility.patch"
  # CMake: install pkg-config files for parity with autotools
  patch -p1 -i "${srcdir}/cmake-install-pkgconfig.patch"
}

build() {
  cd $pkgname-$pkgver
  # Note: -Werror is added by default and cannot be disabled for now.
  cmake . \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_INSTALL_LIBDIR=lib \
      -DENABLE_STATIC=OFF
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir/" install
}
