# AliceDocs

TLDR; __It doesn't require you to learn Markdown coupled with a very low barrier to setup, topped with the collaborative editing benefits from Google.__

A simplified framework and structure for using Google Docs editor to write, mange, and publish content to the web in a quick and friendly manner with minimal setup and configuration.

## Sandbox & Local Development
```
mkdir ~/project
cd  ~/project
git clone git@github.com:donohoe/alice-docs.git
cd alice-docs/public
php -S localhost:2340
```

Then open this [link](http://localhost:2340/) in the browser of your choice: http://localhost:2340/

## Usage

Once a document has been set as the content source (See _Setting up a Google Document_ below), changes are published by Google every 5 minutes.

_AliceDocs_ supports many formatting features found in a Google Document. In using these features, style information is captured and included within the published page. 

This includes:

* Styles
  * "Normal Text", 
  * "Title", "Subtitle", and 
  * "Heading 1" through "Heading 6"
* Text Styles
  * Bold, Italic, Underline, color, highlight colors
* Tables
* Images
  * Embedded images are then hosted on Googles servers though I don't recommend using Google as your de facto image host.

Beyond that, support is ad-hoc and might vary as Google makes changes to their service. In general we've found that a lot of styles naturally comes through to _AliceDocs_.

## Syntax

Example:

`key: value`

The key is not case-sensitive. Its okay to have trailing spaces before or after the colon separator.

These are equivalent:
* `key:value`
* `Key:value`
* `KEY: value`

The current supported keys are:

* `title: <text>`
  * Provides a tile for the web page.
* `page: <page-name>`
  * Define the beginning of content for a new page. 
  * If you follow this with another _title_ key, you can define the specific title for that page.
  * There is no hard-limit to the number of pages you can have by using more _page_ keys.
* `image: <url>`
  * Embed an external image (GIF, PNG, JPG only).
* `video: <url>`
  * Embed an external video (MP4 only).
* `quote: <text>`
  * Used primarily to allow this to document the _key:value_ pairs on _AliceDoc_ pages.
* `embed: <url>`
  * Embed an external media item.
  * Supported media items include:
    * YouTube
      * Example: `Embed: https://www.youtube.com/watch?v=y2bX2UkQpRI`
    * Vimeo
      * Example: `embed:https://vimeo.com/244506823`
    * Giphy
      * Example: `embed: https://giphy.com/embed/9H8dz7341cJIQ`
    * Twitter
      * Example: `embed: https://twitter.com/BarackObama/status/932685522820042754`
    * Instagram
      * Example: `embed: https://www.instagram.com/p/BcnHp6tFM5_/`
    * SoundCloud
      * Example: `embed: https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/34019569&amp;color=0066cc`
    * Spotify
      * Example: `embed: https://embed.spotify.com/?uri=spotify%3Auser%3Asfchronicle%3Aplaylist%3A4zxPdQDo2VKvl6GFc7dBDF`
    * Planned:
      * DocumentCloud
      * Google Maps


## Setting up a Google Document:

### Creating a new document

1. Create a new Google Document by visiting this link:
https://docs.google.com/document/create
2. Copy/Paste this sample text into the document:
```
Hello World
Title: Hello
This is simple single page example. It really doesn't get more basic than this.
Google only allows updates to go through every 5 minutes so this isn't going to be any good for live-blogging. In addition, the code has local file caching set to 5 minutes so it could be anywhere between 5 and 10 minutes for changes to take affect.
Optimus Prime, known in Japan as Convoy, is a fictional character from the Transformers franchise. He is the leader of the Autobots, a fictional group of sentient robots that can transform into other forms (e.g: cars and other objects). He is the most iconic of the Transformers, being frequently featured in popular culture.
image: https://en.wikipedia.org/wiki/Optimus_Prime#/media/File:Optimus_Prime_patent.png
```
3. Go to: `File > Publish` to the web...
4. Click `Publish`
5. When asked to confirm, choose `OK`
6. Copy the URL that appears in as the new link
7. Click the "X" in top-right corner to close.

### Getting the document ID

Now that you have the URL you need to get the ID from it. This is relatively easy.

The URL will look like this:

`docs.google.com/document/d/e/2PACX-1vQ76OboMhN5zvMZ43LMsu3SvnGts7m8eM3k0VAB5rL22KNjOISNNpN4xCMNyA0dwkf15pxjZ7z1C48i/pub`

and you're interested in this part:

`docs.google.com/document/d/e/`__`2PACX-1vQ76OboMhN5zvMZ43LMsu3SvnGts7m8eM3k0VAB5rL22KNjOISNNpN4xCMNyA0dwkf15pxjZ7z1C48i`__`/pub`

### Modifying the code

8. Open up public/index.php
9. Update the line to reflect the ID of your document:
  * `$response = $document->Run( "YOUR-DOCUMENT-ID" );`

### Here's one I made earlier... 

There are a number of Google Documents already Published to the web that demonstrates styles and functionality. They include:

__1. Hello World__
  * Very basic example.
  * [Document URL](https://docs.google.com/document/d/1k0-Pg1pqUh31gdSw4QxKSfAFsFsktkSfQbqq2nDUmTw/)
  * [Web Publish URL](https://docs.google.com/document/d/e/2PACX-1vQ76OboMhN5zvMZ43LMsu3SvnGts7m8eM3k0VAB5rL22KNjOISNNpN4xCMNyA0dwkf15pxjZ7z1C48i/pub)
    * Google ID is: _2PACX-1vQ76OboMhN5zvMZ43LMsu3SvnGts7m8eM3k0VAB5rL22KNjOISNNpN4xCMNyA0dwkf15pxjZ7z1C48i_

__2. Styles and Elements__
  * Various supported text styling, fonts, headers and usag eof tables, images, css etc.
  * [Document URL](https://docs.google.com/document/d/1KKPrL3MCtA0V8K6UIzMzeCdDG54NFDrEDhS5Y6IW6QE/)
  * [Web Publish URL](https://docs.google.com/document/d/e/2PACX-1vTXpFXuIQJimIJ6rsD13XC-MHJnpDlarlWiYsBoL0cYBkYyyT0l9LJ7RNfRreod7QLwqCCTdaixJZhe/pub)
    * Google ID is: _2PACX-1vTXpFXuIQJimIJ6rsD13XC-MHJnpDlarlWiYsBoL0cYBkYyyT0l9LJ7RNfRreod7QLwqCCTdaixJZhe_

__3. Pages__
  * An example of using one document to manage 3 web pages
  * [Document URL](https://docs.google.com/document/d/1naguPdhgtenA3y_tRtNQU91QlK92zch40YYpa14yoJA/)
  * [Web Publish URL](https://docs.google.com/document/d/e/2PACX-1vR-pd40hZJdD073n53Ejt5OMqADdFYDUYj1JJuA1mbuppCqcWCZ3C9WG6xRMpDYXpGo_ZOt0gShfwMK/pub)
    * Google ID is: _2PACX-1vR-pd40hZJdD073n53Ejt5OMqADdFYDUYj1JJuA1mbuppCqcWCZ3C9WG6xRMpDYXpGo_ZOt0gShfwMK_

## To Do

* Question: Remove phpQuery as a dependency?
* Lazy-load embeds and images by default via standardized JS
* Syntax for indicating group of images to be treated as a Slideshow
* ~~New round of documentation on usage (multi-page, title, etc)~~
* Embeds
  * ~~Embed external media and elements.~~
  * Example: ~~Twitter, Instagram, YouTube,~~ Google Forms, etc.
* ~~Quote or escape things so I can show code snippets~~

## Dependencies

* [phpQuery](https://github.com/punkave/phpQuery)
  * [Documentation](https://code.google.com/archive/p/phpquery/wikis/Manual.wiki)
  * Example: [Manipulating DOM Documents with phpQuery](https://codingexplained.com/coding/php/manipulating-dom-documents-with-phpquery)

## Problems, Questions, Typos?

_Pull Requests_ are welcome or create a [new Issue](https://github.com/donohoe/alice-docs/issues/new) plz.
