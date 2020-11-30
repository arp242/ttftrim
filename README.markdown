ttftrim removes glyps from TTF fonts. This is useful if you want to reduce the
size of fonts, for example for webfonts.

This uses the fontforge Python library; usually installing fontforge should
install this as well.

Compress and decompress the TTF fonts to WOFF2 with `woff2_decompress` and
`woff2_compress` from https://github.com/google/woff2 – fontforge includes WOFF2
compression, but it's not very good (giving filesizes more than two times
larger).

---

Usage: `ttftrim input-file output-file [corpus]`

After starting it will load a list of glyphs in `$EDITOR`; remove the lines you
don't want, save, and exit.

If `corpus` is given then it will automatically comment out the glyphs not found
in the the corpus text:

    $ ttftrim in.ttf out.ttf ~/code/arp242.net

This can be a file or directory tree.

For example before reducing the glyphs to those used only on my site:

    total 144K
    -rw-r--r-- 1 martin martin 44K Nov 30 16:36 libre-baskerville-bold.woff2
    -rw-r--r-- 1 martin martin 53K Nov 30 16:36 libre-baskerville-italic.woff2
    -rw-r--r-- 1 martin martin 43K Nov 30 16:36 libre-baskerville.woff2

And after:

    total 88K
    -rw-r--r-- 1 martin martin 26K Nov 30 16:36 libre-baskerville-bold.woff2
    -rw-r--r-- 1 martin martin 29K Nov 30 16:36 libre-baskerville-italic.woff2
    -rw-r--r-- 1 martin martin 26K Nov 30 16:36 libre-baskerville.woff2

---

Note: this tool hasn't been tested too extensively. In fact, it's tested with
just the one font I use on my website (Libre Baskerville) 🙃

Note 2: it doesn't modify lookup tables at the moment, so if you remove a glyph
mentioned in a loopup table you'll get a validation error.
