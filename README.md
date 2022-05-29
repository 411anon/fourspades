[![GPL](https://img.shields.io/badge/license-GPL--3.0-red.svg)](https://github.com/xtreme8000/BetterSpades/blob/standalone/LICENSE)

![GPL v3](https://www.gnu.org/graphics/gplv3-127x51.png)
## ![](docs/icon_small.png) fourspades

A BetterSpades fork with classic gameplay elements restored.

* Replicate of the great game *Ace of Spades* (classic voxlap)
* A focus on versions of the game from 0.52 and earlier, with 0.75 fixes
* runs on modern systems without resolution problems or mouse issues
* runs on very old systems back to OpenGL 1.1 (OpenGL ES support too)
* shares similar if not even better performance to voxlap
* can run on *"embedded"* systems like a [Steam Link](https://store.steampowered.com/app/353380/Steam_Link/)

#### Why should I use this instead of ...?

* free of any Jagex code, they can't shut it down
* classic HUD, original WW1 aesthetic
* more accurate rifle
* no SMG or shotgun
* no sprinting or autoclimb
* easy to use
* no hidden bugs

### Quick usage guide

You can either:
* use the client temporarily by extracting the downloaded zip into a new directory.
* extract all contents to your current Ace of Spades installation directory (normally found at `C:/Ace of Spades/`), effectively replacing the old voxlap version

## System requirements

| Type    | min. requirement                                     |
| ------- | ---------------------------------------------------- |
| OS      | Windows 98 or Linux                                  |
| CPU     | 1 GHz single core processor                          |
| GPU     | 64MB VRAM, Mobile Intel 945GM or equivalent          |
| RAM     | 256MB                                                |
| Display | 800x600px                                            |
| Others  | Keyboard and mouse<br />Dial up network connection   |


## Build requirements

This project uses the following libraries and files:

| Name         | License         | Usage                  | GitHub                                             |
| ------------ | --------------- | ---------------------- | :------------------------------------------------: |
| GLFW3        | *ZLib*          | OpenGL context         | [Link](https://github.com/glfw/glfw)               |
| OpenAL soft  | *LGPL-2.1*      | 3D sound environment   | [Link](https://github.com/kcat/openal-soft)        |
| inih         | *BSD-3.Clause*  | .INI file parser       | [Link](https://github.com/benhoyt/inih)            |
| stb_truetype | *Public domain* | TrueType font renderer | [Link](https://github.com/nothings/stb)            |
| dr_wav       | *Public domain* | wav support            | [Link](https://github.com/mackron/dr_libs/)        |
| http         | *Public domain* | http client library    | [Link](https://github.com/mattiasgustavsson/libs)  |
| LodePNG      | *MIT*           | png support            | [Link](https://github.com/lvandeve/lodepng)        |
| libdeflate   | *MIT*           | decompression of maps  | [Link](https://github.com/ebiggers/libdeflate)     |
| enet         | *MIT*           | networking library     | [Link](https://github.com/lsalzman/enet)           |
| parson       | *MIT*           | JSON parser            | [Link](https://github.com/kgabis/parson)           |
| log.c        | *MIT*           | logger                 | [Link](https://github.com/xtreme8000/log.c)        |
| GLEW         | *MIT*           | OpenGL extensions      | [Link](https://github.com/nigels-com/glew)         |
| hashtable    | *MIT*           | hashtable              | [Link](https://github.com/goldsborough/hashtable/) |
| libvxl       | *MIT*           | access VXL format      | [Link](https://github.com/xtreme8000/libvxl/)      |
| microui      | *MIT*           | user interface         | [Link](https://github.com/rxi/microui)             |
| cglm         | *MIT*           | fast math              | [Link](https://github.com/recp/cglm)               |
| ccolorconv   | *Apache*        | color conversion       | [Link](https://github.com/411anon/ccolorconv)      |

You will need to compile the following by yourself, or get hold of precompiled binaries:

* GLFW3
* GLEW
* OpenAL soft *(only needed on Windows)*
* libdeflate
* enet

Follow the instructions on their project page, then place produced static libraries in `deps/`.

If you are compiling 32-bit binaries, you need 32-bit static libraries. If you are compiling 64-bit binaries, you need 64-bit static libraries.

All other requirements of the above list (like single file libs) will be downloaded by CMake automatically and **don't** need to be taken care of. Because state of copyright of 0.75 assets is unknown, CMake will also download additional assets from [*here*](http://aos.party/bsresources.zip) which are not part of this repository.

### Windows (MSYS2)

Here's a few tips on getting started building on Windows:

* [How to install GCC & MSYS2](https://github.com/orlp/dev-on-windows/wiki/Installing-GCC--&-MSYS2)
* [How to configure Visual Studio Code for C development](https://code.visualstudio.com/docs/cpp/config-mingw)
* [How to add the MSYS2 terminal to Visual Studio Code](https://stackoverflow.com/questions/45836650/how-do-i-integrate-msys2-shell-into-visual-studio-code-on-window/68253833#68253833) *(change MINGW64 to MINGW32 if building 32-bit binaries)*

If targeting 32-bit and 64-bit Windows, install these packages (recommended):
```
pacman -S --needed base-devel mingw-w64-i686-toolchain mingw-w64-i686-cmake mingw-w64-i686-glfw mingw-w64-i686-mesa mingw-w64-i686-openal mingw-w64-i686-enet mingw-w64-i686-glew mingw-w64-i686-libdeflate
```

If targeting only 64-bit Windows, install these packages:
```
pacman -S --needed base-devel mingw-w64-x86_64-toolchain mingw-w64-x86_64-cmake mingw-w64-x86_64-glfw mingw-w64-x86_64-mesa mingw-w64-x86_64-openal mingw-w64-x86_64-enet mingw-w64-x86_64-glew mingw-w64-x86_64-libdeflate
```

To target Windows XP when using MSYS2, you will need to downgrade `mingw-w64-i686-libwinpthread-git` and `mingw-w64-i686-winpthreads-git` packages to version `7.0.0.5273.3e5acf5d-1` or earlier:
```
wget https://github.com/Marisa-Chan/UA_source_XP_build/raw/main/pkg_cache/mingw-w64-i686-libwinpthread-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz
wget https://github.com/Marisa-Chan/UA_source_XP_build/raw/main/pkg_cache/mingw-w64-i686-winpthreads-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz

pacman -U --noconfirm mingw-w64-i686-libwinpthread-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz mingw-w64-i686-winpthreads-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz

rm mingw-w64-i686-libwinpthread-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz
rm mingw-w64-i686-winpthreads-git-5.0.0.4573.628fdbf-1-any.pkg.tar.xz
```

This project uses CMake to generate all Makefiles automatically. For 32-bit binaries, you can generate the required files by opening the MSYS2 MINGW32 shell in the `build/` directory and typing:
```
cmake -G "MinGW Makefiles" ..
mingw32-make
```

If everything went well, `client.exe` should be in the `build/BetterSpades/` subfolder. `OpenAL32.dll` must be placed in the same directory as `client.exe` for the game to launch.

To connect directly to localhost:
```
client.exe -aos://16777343:32887
```

### Linux (Ubuntu 20.04/WSL2)

Install these packages:
```
sudo apt install build-essential cmake libgl1-mesa-glx libgl1-mesa-dev libopenal1 libopenal-dev libglfw3-dev libenet-dev libglew-dev libdeflate-dev
```

Inside the `build` directory, run these commands to configure the build system and begin compiling:
```
cmake ..
make
```

This command will start the client inside the `build/bin/` directory:
```
./client
```
Or connect directly to localhost:
```
./client -aos://16777343:32887
```
