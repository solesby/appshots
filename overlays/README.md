You can use these overlays as is, and they will be pulled from the appshots source directory.

The `base.png` files were exported from `base.sketch` which you can edit with [Sketch3 by Bohemian Coding](http://bohemiancoding.com/sketch/).

The `none.png` were generated using the following commands.

```
convert -size 1x1 xc:white -alpha transparent overlays/iPad/none.png
convert -size 1x1 xc:white -alpha transparent overlays/iPhone4/none.png
convert -size 1x1 xc:white -alpha transparent overlays/iPhone5/none.png
convert -size 1x1 xc:white -alpha transparent overlays/iPhone6/none.png
convert -size 1x1 xc:white -alpha transparent overlays/iPhone6plus/none.png
```

```
convert -size 1536x2048 xc:white -alpha transparent overlays/iPad/none.png
convert -size 1536x2048 xc:white -alpha transparent overlays/iPad/none.png
convert -size  640x960  xc:white -alpha transparent overlays/iPhone4/none.png
convert -size  640x1136 xc:white -alpha transparent overlays/iPhone5/none.png
convert -size  750x1334 xc:white -alpha transparent overlays/iPhone6/none.png
convert -size 1242x2208 xc:white -alpha transparent overlays/iPhone6plus/none.png
```
