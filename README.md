Flatpak manifest for HP's Zcentral Remote Boost Receiver (RGR)

Which seems to be a replacement for HP's RG receiver.

## Why

I got tired of it breaking all the time when installing it using
[AUR](https://github.com/plattfot/rb-rgr-aur) (it does not play nice with wayland). Hopefully this will be
more stable as a flatpak.

## Install

### Download and setup

Download tarball from [hp.com](https://www8.hp.com/us/en/workstations/zcentral-remote-boost.html). Generate a file called `bios`
containing the UUID for the bios using `dmidecode`

```sh
    sudo dmidecode -t 1 > bios
```
See hp issue [6133726](https://h30434.www3.hp.com/t5/Software-Archive-Read-Only/Authorization-fails-on-Linux-after-kernel-4-5-rgsmbiosreader/td-p/6133726), for more info.

Both of these files should be placed in the same directory as
`io.github.plattfot.hp-rgreceiver.yaml`

### Install dependencies

Install the `org.kde.Platform` and `org.kde.Sdk`

```sh
    flatpak install org.kde.Platform org.kde.Sdk
```

Pick the version matching `runtime-version` in
`io.github.plattfot.hp-rgreceiver.yaml`.

You need to install `flatpak-builder`, some package managers bundle
this with flatpak some do not. If you are running guix,
`flatpak-builder` is not in the main channel (yet). I currently have
it in my [channel](https://git.sr.ht/~plattfot/plt/tree/d8ad5f4a41fb607bfd0d890fcaf89990ed1a95ef/item/plt/packages/package-management.scm#L40), but it is in a rough shape.

### Build

When everything is setup and dependencies are installed you can build
the package with `flatpak-builder` and install it to your user:

```sh
    flatpak-builder --user --install --force-clean build io.github.plattfot.hp-rgreceiver.yaml
```
