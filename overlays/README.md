You can use these overlays as is, and they will be pulled from the appshots source directory.

The `base.png` files were exported from `base.sketch` which you can edit with [Sketch3 by Bohemian Coding](http://bohemiancoding.com/sketch/).

The `none.png` were generated using the following commands.

    convert -size 1536x2048 xc:white -alpha transparent overlays/iPad97/none.png
    convert -size 2048x2732 xc:white -alpha transparent overlays/iPad129/none.png
    convert -size 1668x2388 xc:white -alpha transparent overlays/iPad110/none.png
    convert -size 1668x2224 xc:white -alpha transparent overlays/iPad105/none.png
    convert -size  640x960  xc:white -alpha transparent overlays/iPhone35/none.png
    convert -size  640x1136 xc:white -alpha transparent overlays/iPhone40/none.png
    convert -size  750x1334 xc:white -alpha transparent overlays/iPhone47/none.png
    convert -size 1242x2208 xc:white -alpha transparent overlays/iPhone55/none.png
    convert -size 1125x2436 xc:white -alpha transparent overlays/iPhone58/none.png
    convert -size 1242x2688 xc:white -alpha transparent overlays/iPhone65/none.png
    convert -size 1920x1080 xc:white -alpha transparent overlays/appleTV/none.png
    convert -size  312x390  xc:white -alpha transparent overlays/appleWatch3/none.png
    convert -size  368x448  xc:white -alpha transparent overlays/appleWatch4/none.png
