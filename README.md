## JPEG codec with mods for Lossless, 12-bit lossy (XP)
XP : extended precision

The [libjpeg](https://github.com/externpro/libjpeg.git) repository is a submodule of this repository (jpegxp) 3 times (see [.gitmodules](.gitmodules)),
with modifications to each submodule in a branch to support building a single JPEG codec capable of
1. lossy 8-bit encode and decode [lossy8](https://github.com/externpro/libjpeg/compare/09a4003...lossy8.6b)
1. lossy 12-bit encode and decode [lossy12](https://github.com/externpro/libjpeg/compare/09a4003...lossy12.6b)
1. lossless decode (NOTE: no encode support) [lossless](https://github.com/externpro/libjpeg/compare/eccc424...lossless.6b)

libjpeg https://libjpeg.sourceforge.net is written and distributed by the Independent JPEG Group (IJG) https://www.ijg.org

lossless decode support was derived from a patch provided by Ken Murchison https://en.wikipedia.org/wiki/Lossless_JPEG#cite_note-1

IJG license [see LEGAL ISSUES in README](https://github.com/externpro/libjpeg/blob/upstream/README#L99)
