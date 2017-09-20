Title: ASTC texture format
Date: 2016-07-07 21:32
Tags: texture, tools

Tools
---------------------------------

### AMD Compressonator

* version 2.3.2953
* Could not open RGB32f TIF, EXR OK
* Didn't want to compress to ASTC ("incompatible")
* Didn't even want to output as uncompressed RGBA32f DDS (Memory Error(2): Destination image must be compatible with source)
* OK pour RGB8 TIF, ASTC output pretty fast without mipmaps (`CompressonatorCLI.exe xxx.TIF xxx.KTX -fd ASTC -Quality 0.8000`)
* Problem with mipmaps ? `Error(0): KTX Plugin ID(1) saving file = xxx.KTX`, `Error: saving image or format is unsupported`
* No sRGB support 

### Mali Texture Compression Tool

* version 4.3.0
* Could not open RGB32f TIF, EXR OK
* Can't choose output container with GUI, KTX ?
* `astcenc.exe` stops after a little while, "15%" shown on the progress bar - tested twice with different options

### PVRTexTool

* version 4.16.0
* won't open any RGB32f file ? TIF, HDR, EXR
* won't open RGB8 TIF
* wants to use `astc.exe` which is not provided

### Other (untested)

* the famous `astcenc.exe`, https://github.com/ARM-software/astc-encoder
* https://software.intel.com/en-us/articles/fast-ispc-texture-compressor-update, lib
