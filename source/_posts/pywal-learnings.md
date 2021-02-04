---
title: Pywal Learnings
---

# Generate a theme from an image using pywal
wal -i /path/my_cool_img.jpg

pywal will attempt to set the x background to the image and apply the theme to running terminals.

pywal will create a theme based on the colours in the image placed in ``.cache/wal/schemes/``

The theme will have a file name ending in .json resembling the image path/name:
    _path_my_cool_img_jpg_dark....json

~/.cache/wal will also now contain many more files which are different representations of the colour to suit different applications.
