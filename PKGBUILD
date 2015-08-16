# adapted by Eric Schulte from clang-svn         -*- shell-script -*-
#
# Maintainer: Eric Schulte <schulte.eric@gmail.com>
pkgname=llvm-clang-cmake-svn
pkgver=182150
pkgrel=1
pkgdesc="Low Level Virtual Machine with Clang from SVN compiled with cmake"
arch=('i686' 'x86_64')
url="http://llvm.org/"
license=('custom:University of Illinois/NCSA')
depends=('gcc-libs' 'libffi' 'python2' "gcc>=4.7.0")
makedepends=('subversion' 'cmake')
provides=('clang' 'llvm')
conflicts=(llvm llvm-svn llvm-ocaml clang clang-svn clang-analyzer)
source=(svn/llvm::svn+http://llvm.org/svn/llvm-project/llvm/trunk
    svn/llvm/tools/clang::svn+http://llvm.org/svn/llvm-project/cfe/trunk
    svn/llvm/tools/clang/tools/extra::svn+http://llvm.org/svn/llvm-project/clang-tools-extra/trunk
    svn/llvm/projects/compiler-rt::svn+http://llvm.org/svn/llvm-project/compiler-rt/trunk)
md5sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')

_svndir="llvm"
_build="llvm-build"

pkgver() {
  cd "${srcdir}/${_svndir}"
  svnversion | tr -d [A-z]
}

_make_w_python2() {
    ln -sf $(which python2) python
    PATH="./:$PATH" make $@
    rm python
}

build() {
  mkdir -p ${srcdir}/${_build}
  cd ${srcdir}/${_build}
  cmake ../${_svndir}
  _make_w_python2
}

package() {
  cd ${srcdir}/${_build}
  _make_w_python2 DESTDIR=$pkgdir install
  install -Dm644 ../${_svndir}/LICENSE.TXT \
      "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
}
# vim:set ts=2 sw=2 et:
