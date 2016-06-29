+++
date = "2016-06-29T21:32:50+02:00"
draft = true
title = "ETC texture format"
tags = [ "texture", "tools" ]

+++

As of 2016, comes in two flavors :

* ETC1, the original, RGB only (2005)
* ETC2, more quality + sRGB + RGBA
    * mandatory in OpenGL ES 3.0 and OpenGL 4.3

More info on [wikipedia](https://en.wikipedia.org/wiki/Ericsson_Texture_Compression).

Platform support
--------------------
### ETC1
* Android: 2.2+

### ETC2
* Android: 4.3+, Nexus 4+, Galaxy S5
* iOS: iOS 7+, iPhone 5s+ 

Tools (ETC1)
--------------------

Globally found nothing good, to build [KTX]({{< relref "KTX-texture-container.md" >}}) files, from bad to worse :

### PVRTexTool

* No `TIF` support as input
* Awfully slow with default settings, use `-q pvrtcfast`

### Mali GPU Texture compression tool

* http://malideveloper.arm.com/resources/tools/mali-gpu-texture-compression-tool ?
* uses `etcpack.exe` through command line, along with `ImageMagick`
* awfully slow

### AMD Compress

* open source, fast
* crashes when generating mipmaps (at the last 1x1 pixel level)

### etcpack

Only supports `PPM` files as input

### Untested

* https://developer.qualcomm.com/software/adreno-gpu-sdk/faq


Libs
--------------------
### rg-etc1

* https://code.google.com/archive/p/rg-etc1/, by Rich Geidrich
* According to this benchmark, https://bitbucket.org/wolfpld/etcpak/wiki/Home, quite fast

### others

* https://github.com/paulvortex/RwgTex
* https://github.com/GameTechDev/ISPCTextureCompressor, promising
