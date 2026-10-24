platform_detect
===============

Project is providing simple C library, that can be loaded to test if system can handle specific platform, library was build for with a `cross-compiler`.

The idea is to try looping over different shared libraries trying to load it.

Why
======

Initially, created for Python, as the end user of this project.

Python can be modified, or the system can report false-positive to an arch requests. For that reason we explicitly try to load a library and see if Python and the system can run it.

How to use
==========

For Python, clone repository to the library folder and call `detect_platform`:
```python

from platform_detect.python.platform import detect_platform

print(detect_platform()) # Would show 'linux-x64', for example

```

Supported platforms
===================

`detect_platform()` returns one of: `android-arm64`, `android-arm`, `android-x64`, `android-x86`,
`linux-arm64`, `linux-armv7`, `linux-armv7_softfp`, `linux-armv6`, `linux-x64`, `linux-x86`,
`windows-x64`, `windows-x86`, `darwin-arm64`, `darwin-x64` (or `None` if no library can be loaded).

Higher architectures are tried first. For example, native Kodi on Apple Silicon detects `darwin-arm64`,
while an x86_64 Kodi running under Rosetta can only load the x64 library and detects `darwin-x64`.
The darwin libraries require macOS 13 or newer.

Compile
=======

For compiling libraries <https://github.com/ElementumOrg/cross-compiler> Docker images are used.

To compile images just run make:
```sh

$ make all

```

Contributions
=============

Any contributions are welcome.

Few ideas for contributions:
- There are more platforms to detect.
- Move Docker images to musl-based.
- Make modules for other programming languages.
