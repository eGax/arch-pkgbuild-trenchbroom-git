The purpose of this is to enable Arch users to build the last official release of TrenchBroom 2023.1. since the current AUR version is broke, missing depends, etc.

To build TB in your Arch distro of choice from a terminal :

`git clone https://github.com/eGax/arch-pkgbuild-trenchbroom.git`<br>
`cd arch-pkgbuild-trenchbroom`<br>
`makepkg -si`<br>


That will clone it, enter it, build it, create a symlink from `/usr/lib/libtinyxml2.so.10.0.0` to `/usr/lib/libtinyxml2.so.9`, then installs the package into your system.<br>
<br>
<br>
If you want to use a more current build of TrenchBroom that will be the next 2024 release, highly recommend using my AUR trenchbroom-git https://aur.archlinux.org/packages/trenchbroom-git 
