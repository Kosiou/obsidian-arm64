# Obsidian ARM64 Debian Package

This project repackages Obsidian's official AMD64 Debian package with the ARM64 binaries from Obsidian's official ARM64 AppImage. It produces an unofficial `arm64` `.deb` for Debian and Ubuntu systems running on `aarch64`.

Obsidian does not provide an official ARM64 `.deb`. The packages used as inputs are downloaded from the official [Obsidian releases](https://github.com/obsidianmd/obsidian-releases).

## Download and Install

Download the latest package from [GitHub Releases](https://github.com/Kosiou/obsidian-arm64/releases), then install it on an ARM64 Debian-based system:

```bash
sudo dpkg -i obsidian_VERSION_arm64.deb
sudo apt-get install -f
```

Replace `VERSION` with the version in the downloaded filename.

## Automated Builds

GitHub Actions checks the official Obsidian release every Monday. When a version has not already been repackaged, the workflow downloads the AMD64 `.deb` and ARM64 AppImage, builds the ARM64 package, verifies its package architecture, and publishes it as a GitHub Release. A build can also be started manually from the repository's Actions tab.

## Build Locally

Requirements are `dpkg-deb`, `python3`, and `squashfs-tools`.

```bash
VERSION=1.15.1
curl -fL "https://github.com/obsidianmd/obsidian-releases/releases/download/v${VERSION}/obsidian_${VERSION}_amd64.deb" -o "obsidian_${VERSION}_amd64.deb"
curl -fL "https://github.com/obsidianmd/obsidian-releases/releases/download/v${VERSION}/Obsidian-${VERSION}-arm64.AppImage" -o "Obsidian-${VERSION}-arm64.AppImage"
bash repack-arm64.sh "$VERSION"
```

The generated package is `obsidian_${VERSION}_arm64.deb`.

## Acknowledgements

The repackaging approach and the original `repack-arm64.sh` implementation are based on [edyfox/obsidian-deb-arm64](https://github.com/edyfox/obsidian-deb-arm64). Thank you to edyfox for creating and sharing the original project. This repository adapts that work, including block-based copying when extracting the AppImage squashfs, and adds scheduled GitHub Actions builds and releases. The upstream project is licensed under Apache-2.0. See [LICENSE](LICENSE).

This is an unofficial community repackaging project and is not affiliated with or endorsed by Obsidian.
