# Maintainer: ebriouscoding <ebriouscoding at gmail dot com>
pkgname=pebble-tool
pkgver=5.0.35
pkgrel=1
pkgdesc="Pebble SDK CLI tool (pebble-tool) managed with uv"
arch=('any')
url="https://developer.repebble.com/sdk/"
license=('MIT')
depends=('python' 'uv' 'nodejs' 'npm' 'sdl2' 'glib2' 'pixman' 'zlib')
options=('!strip')

package() {
  local target_dir="${pkgdir}/usr/share/pebble-sdk"
  local target_bin="${pkgdir}/usr/bin"
  
  mkdir -p "${target_dir}"
  mkdir -p "${target_bin}"

  # 1. Create an isolated virtual environment using Python 3.13 inside the package directory
  msg2 "Creating isolated Python 3.13 environment..."
  uv venv "${target_dir}/venv" --python 3.13

  # 2. Install pebble-tool directly into this virtual environment
  msg2 "Installing pebble-tool..."
  uv pip install --python "${target_dir}/venv/bin/python" pebble-tool

  # 3. Fix the hardcoded build-directory paths inside the venv scripts
  msg2 "Fixing environment paths..."
  find "${target_dir}/venv/bin" -type f -exec sed -i "s|${pkgdir}||g" {} +

  # 4. Create a symlink in /usr/bin so 'pebble' is available globally
  ln -s "/usr/share/pebble-sdk/venv/bin/pebble" "${target_bin}/pebble"
}
