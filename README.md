I wanted a really simple process to generate app store screenshots for [some of my apps](http://paribuscalc.com). I want to easily generate these from screenshots and configure-once layout.

<blockquote style="text-align:center">
<img valign="center" src="http://www.paribuscalc.com/store/screenshots/iPhone5/screen1.png" width="200">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img valign="center" src="http://www.paribuscalc.com/store/iPhone5_screen1.png" width="200">
</blockquote>

Even though I love [Sketch3](http://bohemiancoding.com/sketch/) and use it for most other assets, replacing screenshots in the sketch file and realigning was way too tedious.

There are several options out there to automate, but this was my attempt--and IMHO much simpler to setup and use.

I welcome any fixes or improvements you want to contribute. Fork away.


## How It Works

These scripts allow you to:

1. Take 5 screenshots in the simulator (simply press `⌘-S`)
2. Run `gather_screenshots screenshots/iPhone6`
3. Run `generate_store_images iPhone6`

The `gather_screenshots` command simply pulls the most recent screenshots from your desktop (with ugly names like `iOS Simulator Screen Shot Aug 27, 2015, 1.17.21 PM.png`). 

The `generate_store_images` processes the `appshots.txt` config file and the `screenshots` folder. The script loops through each device and all the screenshots.

1. Create proper size app store image with background color
1. Resize and composite the screenshot
1. Composite the overlay image (with transparency)
1. Add `blurb1` text
1. Add `blurb2` text
1. Save output file as `<device>_<screen>.png`
1. Output details to `index.html`


## Installation

The primary workhorse of these scripts is `convert` which is part of [ImageMagick](http://www.imagemagick.org/). The easiest way to install that is with [Homebrew](http://brew.sh/). If you already have `convert` installed you can skip this step.

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    
    brew install imagemagick --with-fontconfig --with-ghostscript --with-librsvg

Download or fork this project

    curl -L -O https://github.com/solesby/appshots/archive/master.zip
    
    unzip master

You should be all set up. The scripts should work from whereever you install them. To test, you can run the scripts on the `sample` folder.

    cd appshots/sample
    
    ../gather_screenshots screenshots/iPhone5
    
    ../generate_store_images all preview

Go get coffee, because you just prettied-up 25 screenshots in a few minutes.


## Usage

### Project setup

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

The `appshots.txt` is a tab-delimited config file. You can copy the provided one from the `appshots` project folder and modify it. The coordinates should work as is. The most important thing is to set up your color preferences and "blurbs" that you want to overlay. See below for more [details on appshots.txt](#appshots-txt-format).

The `screenshots` folder is required. It is organized by `screenshots`/`device`/`screen[1-5].png`. Any device/screen combination not present in the `appshots.txt` or the `screenshots` directory tree will be ignored.

You can optionally provide a `overlays` folder. If you don't the script will use the one provide in the projects folder.



### `gather_screenshots` Helper

You can manually populate the `screenshots` folders for each device. This is just a helper script to gather screenshots and organize them.

It assumes that the most recent 5 screen shots are the 5 shots you want for the app store. So the first screenshot you take in the simulator is screen1. This is just a handy way to avoid dealing with renaming/moving all the files on the desktop (with ugly names like `iOS Simulator Screen Shot Aug 27, 2015, 1.17.21 PM.png`).

For whichever device you want to gather, take 5 screenshots (in desired order) in the simulator (for example here we assume iPhone5). Then execute these commands:

    cd store
    
    /path/to/appshots/gather_screenshots screenshots/iPhone5

That will copy the most recent screenshots from the desktop and create:

    screenshots/iPhone5/screen1.png
    screenshots/iPhone5/screen2.png
    screenshots/iPhone5/screen3.png
    screenshots/iPhone5/screen4.png
    screenshots/iPhone5/screen5.png

### `generate_store_images` Image Processor


### `appshots.txt` Format


## About the Author

    TODO: insert bio

* [Linked In](http://www.linkedin.com/in/solesby)
* [Twitter](http://twitter.com/solesby)
* [Github](http://github.com/solesby)


## License

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
