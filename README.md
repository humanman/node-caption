node-caption- with modified font in generate.js
============

I added a -font arg, and changed some of the settings to deliver a more readable meme in the genereate.js of this library.  (I wish there was a greater variety of fonts to use. I thought it was restricted to those listed in Ghostscript ~9.1, but even most of those would not be recognized.) Thanks to Jesse Ditson for doing the heavy lifting on this one.

=======================
Node utility for captioning images via imageMagick

To use node-caption, the system it's running on must have imageMagick installed. Here are some ways to do that:

  OSX: `brew install imagemagick`
  
  Ubuntu: `apt-get install imagemagick`
  
  RedHat and other yummy systems `yum install imagemagick`

additionally, you can install it from a binary, as described here [http://www.imagemagick.org/script/binary-releases.php](http://www.imagemagick.org/script/binary-releases.php)

or build from source: [http://www.imagemagick.org/script/install-source.php](http://www.imagemagick.org/script/install-source.php)

##### Usage:

To use caption in a node project, just require it:

`var caption = require('caption')`

There are only two methods in caption, `path`, and `url`

To caption an existing image file, do this:

    caption.path("path/to/file.jpg",options,function(err,captionedImage){
      // err will contain an Error object if there was an error
      // otherwise, captionedImage will be a path to a file.
    })

To download the image first, use `caption.url`:

    caption.path("http://www.someImageHost.com/path/to/image.jpg",options,function(err,captionedImage){
      // err will contain an Error object if there was an error
      // otherwise, captionedImage will be a path to a file.
    })

the `options` object is always the same, and has the following options:

- caption : A string containing the text you would like to caption the image with
- bottomCaption : A string containing the bottom caption, for a meme style caption
- outputFile : if specified, caption will put the new image in this file. If not, it'll return an image in the /tmp directory.
- minHeight : minimum height of the image. (defaults to 100)
- minWidth : minimum width of the image. (defaults to 500)

##### Command line

You can also use caption from the command line.

First, install caption:

`npm install -g caption`

then you can start generating images to your hearts content. Calling caption with no arguments will output the usage options:

    Usage: 
    For a caption on the bottom of the image:
      caption <path to image or image url> "caption text" [ouput file]
    For top and bottom captions (meme style):
      caption <path to image or image url> "top caption" "bottom caption" [ouput file]

You can use a url or a path, caption will try to download the url if it doesn't exist on your local fs.

To specify a minimum height or width from the command line, you can set the `CAPTION_MIN_WIDTH` and `CAPTION_MIN_HEIGHT` environment variables.

##### Examples:

    caption http://simonbisleygallery.com/art/biz00157.jpg "I AM THE LAW" dredd.jpg

  or

    caption.url("http://simonbisleygallery.com/art/biz00157.jpg",{
      caption : "I AM THE LAW",
      outputFile : "dredd.jpg"
    },function(err,filename){
      // do stuff
    })

![I AM THE LAW](http://oi46.tinypic.com/2ylpx6d.jpg)

    caption http://i.imgur.com/AtLeN.png "You are mistaken." "This is my bowl." cat.jpg

  or
  
    caption.url("http://i.imgur.com/AtLeN.png",{
      caption : "You are mistaken.",
      bottomCaption : "This is my bowl.",
      outputFile : "cat.jpg"
    },function(err,filename){
      // do stuff
    })

![This is my bowl.](http://oi47.tinypic.com/2vltytk.jpg)

##### Notes

Currently caption always uses white text with a 2px black stroke. It will automatically make the text as big as possible given the image.

In the future, I may add support for specifying certain imagemagick options for more versatility.

If you find issues, please let me know! The preferred method is to use the [github issue tracker](https://github.com/jesseditson/node-caption/issues)

Credit to [Zach Holman's Fuck Yeah](https://github.com/holman/fuck-yeah) for inspiration.

Feel free to talk to me on [Twitter - @jesseditson](https://www.twitter.com/jesseditson)
