# Maintainer:  jyantis <yantis@yantis.net>

pkgname=python-python-amazon-simple-product-api-git
pkgver=2.0.0.r152.f7348fd
pkgrel=2
pkgdesc='A simple Python 3 wrapper for the Amazon.com Product Advertising API'
arch=('any')
url='https://github.com/yoavaviram/python-amazon-simple-product-api'
license=('APACHE')
depends=('python' 'python-bottlenose-git' 'python-lxml' 'python-dateutil')
source=('git+https://github.com/yoavaviram/python-amazon-simple-product-api.git')
sha256sums=('SKIP')
makedepends=('git' 'python-setuptools')
provides=('python-python-amazon-simple-product-api')
conflicts=('python-python-amazon-simple-product-api')

pkgver() {
  cd python-amazon-simple-product-api
  set -o pipefail
  _gitversion=$(printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)" )

  # If there is a setup.py then pull the version tag from the file
  if [ -f "setup.py" ]; then
    if grep --quiet "version = " setup.py; then
      printf "%s.%s" "$(grep -R "version = " setup.py | awk -F\' '{print $2}')" $_gitversion | sed 's/-/./g'
    elif grep --quiet "version=" setup.py; then
      printf "%s.%s" "$(grep -R "version=" setup.py | awk -F\' '{print $2}')" $_gitversion | sed 's/-/./g'
    else
      printf "%s" $_gitversion
    fi
  else
    printf "%s" $_gitversion
  fi
}

build() {
  cd python-amazon-simple-product-api
  python setup.py build
}

check() {
  cd python-amazon-simple-product-api
  python setup.py test --verbose
}

package() {
  cd python-amazon-simple-product-api

  # We don't need anything related to git in the package
  rm -rf .git*

  python setup.py install --root="${pkgdir}" --optimize=1

  # Install License
  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  # Install Documentation
  install -D -m644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}

# vim:set ts=2 sw=2 et:
