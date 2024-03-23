# Flatpak for Citra Emulator

## Local Build Instructions

Docker container for building the flatpak: `podman run --rm --privileged -it --volume=./:/build --name citra_ctr quay.io/fedora/fedora:39 bash`

Inside the container:

```sh
# Install apps
dnf upgrade -y; dnf install -y flatpak-builder git ; \
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
# Clone repo
cd /build
git clone https://github.com/ramesh45345/org.citra_emu.citra
cd org.citra_emu.citra
git submodule update --init --recursive
```

Build flatpak in contanier:

```sh
# Build
flatpak-builder --install-deps-from=flathub --force-clean build-dir org.citra_emu.citra.json
flatpak build-export export build-dir
# Export bundle
flatpak build-bundle export citra.flatpak org.citra_emu.citra --runtime-repo=https://flathub.org/repo/flathub.flatpakrepo
```
