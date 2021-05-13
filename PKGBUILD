# Based on mimalloc-git AUR by Ranieri Althoff <ranisalt+aur at gmail dot com>
# Maintainer: <r1nlx0 at gmail dot com>

_pkgname=mimalloc
pkgname=${_pkgname}-git
pkgver=r1435.10ce883
pkgrel=1
pkgdesc='General-purpose allocator with excellent performance characteristics'
arch=('x86_64')
license=('MIT')
url='https://github.com/microsoft/mimalloc'
depends=('glibc')
makedepends=('cmake')
provides=('libmimalloc.so=1.0')
_branch=master
source=("${_pkgname}::git+https://github.com/microsoft/${_pkgname}.git#branch=dev-slice")
sha256sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "$_pkgname"
  cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_CFLAGS="-march=native -O3 -pipe -fno-plt -Xclang -load -Xclang /usr/lib/LLVMPolly.so -Wl -mllvm -threads=1 -mllvm -polly -fuse-ld=lld -flto -fuse-linker-plugin" -DCMAKE_CXX_CFLAGS="-march=native -O3 -pipe -fno-plt -Xclang -load -Xclang /usr/lib/LLVMPolly.so -Wl -mllvm -threads=1 -mllvm -polly -fuse-ld=lld -flto -fuse-linker-plugin" -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_INSTALL_PREFIX=/usr .
  make
}

package() {
  cd "$_pkgname"
  make DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
}
