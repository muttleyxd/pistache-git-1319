# Maintainer: Martchus <martchus@gmx.net>

# All my PKGBUILDs are managed at https://github.com/Martchus/PKGBUILDs where
# you also find the URL of a binary repository.

pkgname=pistache-git
_name=${pkgname%-git}
pkgver=1319.a91cb1c
pkgrel=1
arch=('i686' 'x86_64')
pkgdesc='Modern and elegant HTTP and REST framework for C++'
license=('APACHE')
depends=()
makedepends=('cmake' 'git')
checkdepends=('gtest')
provides=("${_name}")
conflicts=("${_name}")
options=(staticlibs)
url="https://github.com/oktal/${_name}"
source=("${_name}::git+https://github.com/oktal/${_name}.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${_name}"
  echo "$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${srcdir}/${_name}"
  git checkout a91cb1c
  patch -p1 <../../patch1.patch
}

build() {
  cd "${srcdir}/${_name}"

  cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DPISTACHE_BUILD_TESTS=true \
    -DPISTACHE_USE_SSL=true \
    .
  make
}

check() {
  cd "${srcdir}/${_name}"
  make test
}

package() {
  cd "${srcdir}/${_name}"
  make DESTDIR="${pkgdir}" install
}
