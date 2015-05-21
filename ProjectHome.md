**imageresampler** is a pubic domain (see [unlicense.org](http://unlicense.org/)) C++ class for memory efficient image/bitmap [resampling](http://en.wikipedia.org/wiki/Resampling_(bitmap)) loosely based on a (heavily bugfixed) version of [Dale Schumacher's public domain resampler](http://tog.acm.org/resources/GraphicsGems/gemsiii/filter.c) in [Graphics Gems 3](http://www.amazon.com/Graphics-Gems-III-IBM-Version/dp/0124096735) (1994). It supports a wide range of filter kernels and windowing functions, clamp/wrap/reflect boundary modes, arbitrary source image phase offsets, floating point pixels with any number of components, and can process images much larger than available memory.

A long time ago, this resampler was written originally in C and 16-bit x86 assembly and was used in a printer driver for a DOS image viewer product. Memory was extremely tight in this environment, which is why this class supports streaming resampling. I've also successfully used this class to generate texture [mipmaps](http://en.wikipedia.org/wiki/Mipmap) in the tool chains of various PC and console game projects. This version is written in fairly portable C++.

**Features**

  * Can up/downsample completely independently on each axis.
  * Plenty of [antialiasing](http://en.wikipedia.org/wiki/Antialiasing) filters: box, tent, bell, b-spline, Mitchell, [Lanczos](http://en.wikipedia.org/wiki/Lanczos_resampling) 3/4/6/12, Blackman, Kaiser, Gaussian, etc.
  * Filter kernels can be offset and scaled (shrinking the kernel a bit to sharpen the output is very useful when generating texture mipmaps)
  * Supports clamp, wrap, etc. boundary modes - useful when filtering wrapping textures
  * Chooses the axis resample order that minimizes the total number of ops, like Heckbert's [Zoom](http://www.xmission.com/~legalize/zoom.html).
  * Operates on any number of input channels, floating point input/output
  * Minimal memory/streaming operation: you feed it some input scanlines, and it gives you as many output scanlines as it can. Or if you don't care about RAM you can feed it all your input scanlines, then "pull" all the output scanlines.

The source archive includes Visual C++ 2005 and 2008 solutions, and a Codeblocks 10.05 workspace.

**Release History**
  * v2.21 - June 4, 2012: Added unlicense.org text (instead of just plain public domain), integrated GCC fixes supplied by Peter Nagy <petern@crytek.com>, Anteru at anteru.net, and clay@coge.net, added Codeblocks project (for testing with MinGW and GCC), added VS2008 project files, VS2008 static code analysis pass, added calls to delete at end of test.cpp.
  * v2.20 - Dec. 31, 2008: Released to public domain on Google Code.

**Test Executable Instructions**
  * I've included a precompiled Win32 executable under bin/resampler.exe. Example usage:
```
  resampler source_image.tga dest_image.tga dest_width dest_height
```

> Where dest\_width/dest\_height is the desired destination image's resolution. The destination format is hard coded to TGA, but the source image may be in any format that Sean Barrett's [STB Image](http://nothings.org/) module supports: PNG/BMP/TGA/etc.

**Additional Links**

[Mipmapping, Part 1](http://number-none.com/product/Mipmapping,%20Part%201/index.html)

[Mipmapping, Part 2](http://number-none.com/product/Mipmapping,%20Part%202/index.html)

[Ray Gardener's image resampler](http://www.daylongraphics.com/download/filter_rcg.zip) - Also derived from Schumacher's code. (URL doesn't appear to work anymore.)

[Paul Heckbert's "Zoom"](http://www.xmission.com/~legalize/zoom.html)

[Mitchell, Don P.; Netravali, Arun N. (August 1988). "Reconstruction filters in computer-graphics"](http://www.mentallandscape.com/Papers_siggraph88.pdf)

**Support Contact**

For any questions or problems with this code please contact Rich Geldreich at <richgel99 at gmail.com>. Here's my [twitter page](http://twitter.com/#!/richgel999).