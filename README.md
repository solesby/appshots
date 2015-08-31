I wanted a really simple process to generate app store screenshots for [some of my apps](http://paribuscalc.com). I want to easily generate these from screenshots and configure-once layout.

<blockquote style="text-align:center">
<img valign="center" src="http://www.paribuscalc.com/store/screenshots/iPhone5/screen1.png" width="200">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img valign="center" src="http://www.paribuscalc.com/store/iPhone5_screen1.png" width="200">
</blockquote>

Even though I love [Sketch3](http://bohemiancoding.com/sketch/) and use it for most other assets, replacing screenshots in the sketch file and realigning was way too tedious.

There are several options out there to automate, but this was my attempt--and IMHO much simpler to setup and use.

I welcome any fixes or improvements you want to contribute. Fork away.


# How It Works

These scripts allow you to:

1. Take 5 screenshots in the simulator (simply press `⌘-S`)
2. Run `gather_screenshots screenshots/iPhone6`
3. Run `generate_store_images iPhone6`

The `gather_screenshots` is optional and simply pulls the most recent screenshots from your desktop (with ugly names like `iOS Simulator Screen Shot Aug 27, 2015, 1.17.21 PM.png`). 

The `generate_store_images` processes the `appshots.txt` config file and the `screenshots` folder. The script loops through each device and all the screenshots.

1. Create proper size app store image with background color
1. Resize and composite the screenshot
1. Composite the overlay image (with transparency)
1. Add `blurb1` text
1. Add `blurb2` text
1. Save output file as `<device>_<screen>.png`
1. Output details to `index.html`


# Installation

The primary workhorse of these scripts is `convert` which is part of [ImageMagick](http://www.imagemagick.org/). The easiest way to install that is with [Homebrew](http://brew.sh/). If you already have `convert` installed you can skip this step.

    ## Install Homebrew (as of this writing -- you should check their website for latest)
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    
    ## Install ImageMagick via brew
    brew install imagemagick --with-fontconfig --with-ghostscript --with-librsvg

Download or fork this project

    curl -L -O https://github.com/solesby/appshots/archive/master.zip
    
    unzip master.zip && mv appshots-master appshots

You should be all set up. The scripts should work from whereever you install them. To test, you can run the scripts on the `sample` folder.

    cd appshots/sample
    
    ../gather_screenshots  screenshots/iPhone5
    
    ../generate_store_images  all  preview

Go get coffee, because you just prettied-up 25 screenshots in a few minutes.


# Usage

## Project setup

I keep a `store` folder in my source repo where I generate store screenshots and other marketing material. It helps to version that along with the app.

Create folder and set up the configuration. You will need a layout that looks something like this:

    store/screenshots/appshots.txt
    
    store/screenshots/iPhone4
    store/screenshots/iPhone4/screen1.png
    store/screenshots/iPhone4/screen2.png
    store/screenshots/iPhone4/screen3.png
    store/screenshots/iPhone4/screen4.png
    store/screenshots/iPhone4/screen5.png
    store/screenshots/iPhone5
    store/screenshots/iPhone5/screen1.png
    store/screenshots/iPhone5/screen2.png
    ...
    store/screenshots/iPhone6
    store/screenshots/iPhone6/screen1.png
    ...
    store/screenshots/iPhone6plus
    store/screenshots/iPhone6plus/screen1.png
    ...
    store/screenshots/iPad
    store/screenshots/iPad/screen1.png
    ...

The `appshots.txt` is a tab-delimited config file. You can copy the provided one from the `appshots` project folder and modify it. The coordinates should work as is. The most important thing is to set up your color preferences and "blurbs" that you want to overlay. See below for more [details on appshots.txt](#configuration-format-appshotstxt).

The `screenshots` folder is required. It is organized by `screenshots`/`device`/`screen[1-5].png`. Any device/screen combination not present in the `appshots.txt` or the `screenshots` directory tree will be ignored.

You can optionally provide a `overlays` folder. If you don't the script will use the one provide in the projects folder.



## Image Processor:  `generate_store_images` 


When your directory is set up with `screenshots` and `appshots.txt` config you are ready to generate your App Store images. Simply execute using the full path to the image processor script. You do not need to keep the `appshots` scripts with your project.

    /path/to/generate_store_images [all|device] [preview|debug]

This will process each entry in `appshots.txt` and generate an output file in the current directory.

The script takes two optional command line parameters. The first parameter tells the script which files to overwrite. *By default it will not clobber any existing generated images.* The script will always generate images that don't exist. You can specify any single device name, e.g. `iPhone6`, or you can specify `all` to regenerate all devices in the config file.

The second parameter are two options helpful in designing and debugging you config.

`preview` -- this will open up the `Preview` app and show you all the generated images. It will only open the device (or all) specified in the first parameter.

`debug` -- this will override the blurb background colors with semi-transparent red, green, or blue. This helps you see your text easier regions without changing your colors in the config.

The first time you run `generate_store_images` it will output an HTML file with the detailsindex.html

##  Helper:  `gather_screenshots`

You can manually populate the `screenshots` folders for each device. This is just a helper script to gather screenshots and organize them.

It assumes that the most recent 5 screen shots are the 5 shots you want for the app store. So the first screenshot you take in the simulator is screen1. This is just a handy way to avoid dealing with renaming/moving all the files on the desktop (with ugly names like `iOS Simulator Screen Shot Aug 27, 2015, 1.17.21 PM.png`).

For whichever device you want to gather, take 5 screenshots (in desired order) in the simulator (for example here we assume iPhone5). Then execute these commands:

    cd store
    
    /path/to/appshots/gather_screenshots   screenshots/iPhone5

That will move the most recent screenshots from the desktop and name them:

    screenshots/iPhone5/screen1.png
    screenshots/iPhone5/screen2.png
    screenshots/iPhone5/screen3.png
    screenshots/iPhone5/screen4.png
    screenshots/iPhone5/screen5.png

## Configuration Format: `appshots.txt`

The `appshots.txt` config file is a simple tab-delimited format. The order of the columns don't matter and many have defaults so could be ommitted. If you put a value of `-` it is treated as if empty or unspecified.

Note since, for some reason, I thought this would be good to write in Bash, the parser is not very robust. So if the script breaks, you probably added something in the config file that confuses it :)

    lang        This is the language for the generated image (current unimplemented) [default: en ]
    device      The device name: iPhone4, iPhone5, iPhone6, iPhone6plus, iPad
    screen      The screen name: screen1, screen2, screen3, screen4, screen5
    width       The width of the output image
    height      The height of the output image
    background  The background color of the overall image [default:#CCCCCC]
    screenPos   The size and location (WxH+x+y) where to resize and place the screenshot
    overlay     The name of the overlay image:  base, none
    b1          The text for blurb1
    b2          The text for blurb2
    b3          The text for blurb3
    b1pos       The size and location (WxH+x+y) where to 
    b1size      The font point size used for the blurb text [default: 45]
    b1bg        The background color of the blurb containing box
    b1color     The text color used for the blurb text
    b1font      The font used for the blurb text [defualt: Helvetica ]
    b1grav      Alignment of the blurb text: northwest, north, northeast, center, 
                    southwest, south, southeast [default: center]

All the config options like `b1color` are repeated for `b2` and `b3` as well.

Most of these just pass through to `convert`, so you might want to check out [the documentation](http://www.imagemagick.org/script/command-line-options.php) for more info.

# About the Author

[LinkedIn](http://www.linkedin.com/in/solesby) &ndash; 
[Twitter](http://twitter.com/solesby) &ndash; 
[Github](http://github.com/solesby)


# License

```
The MIT License (MIT)

Copyright (c) 2015 Adam Solesby

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
