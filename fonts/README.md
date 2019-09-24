# Fonts Usage

### IMPORTANT

The default font in the `generate_store_images` script is: `SF-Pro-Display-Light`.

The following files are provided for example only. The files in this folder are copyright their original authors.

Download Apple provided San Francisco fonts here: <https://developer.apple.com/fonts/>

Download script to generate `type.xml` here: <https://imagemagick.org/Usage/scripts/imagick_type_gen>

Generate the `type.xml`:

`./imagick_type_gen *.otf > type.xml`

Export the font directory environment variable:

`export MAGICK_FONT_PATH=<path to>/appshots/fonts`

