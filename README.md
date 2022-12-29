# Web Browser

Initial discovery to answer questions like:

- What is a Web browser? 
- What does it do? 

![](./Image.png)

# Elements

## Overview

## Major Components

![](./Image_1.png)
![](./Image_2.png)
![](./Image_3.png)

- https://joshondesign.com/2020/03/10/rust_minibrowser
- https://joshondesign.com/2020/04/15/next-steps
- https://limpet.net/mbrubeck/2014/08/08/toy-layout-engine-1.html

- https://www.youtube.com/watch?v=xNu6U5XCMMQ&list=PLJbE2Yu2zumDD5vy2BuSHvFZU0a6RDmgb&index=14

### Example Implementation

- https://github.com/stevus/rust_browser_6_final

## HTML / XML Lexer / Parser

This is necessary to create a DOM (Document Object Model).

The module must be able to handle different content types based on MIME type.

A Node Traversal Engine to separate divs by sections and to numerically number divs with alphanumeric names.

| Library  | Browser  |
| - | - |
| Flex  |   |
| Lex  |   |
| Yacc  |   |
|  Bison |   |
|   |   |

- https://joshondesign.com/2020/03/14/rust_browser_parser 
- https://joshondesign.com/2020/03/21/browser_long_slog
- https://limpet.net/mbrubeck/2014/08/11/toy-layout-engine-2.html

- https://www.youtube.com/watch?v=brhuVn91EdY

### Example Implementation

- https://github.com/stevus/rust_browser_part_1

## CSS Lexer / Parser

This module handles all of the complexity of interpreting and understanding how the properties, units of measure, and the different ways values associated with the W3C visual model can be specified (eg "border: 1px solid black" vs the separate border-width, etc properties).

Nested Associative Array’s to store all CSS class and id tag’s by name and their CSS Rules for the rendering engine Parse or Loop.

| Library  | Browser  |
| - | - |
|   |   |

- https://limpet.net/mbrubeck/2014/08/13/toy-layout-engine-3-css.html
- https://limpet.net/mbrubeck/2014/08/23/toy-layout-engine-4-style.html
- https://limpet.net/mbrubeck/2014/09/08/toy-layout-engine-5-boxes.html
- https://limpet.net/mbrubeck/2014/09/17/toy-layout-engine-6-block.html

- https://www.youtube.com/watch?v=dnrEto7adg0&list=PLJbE2Yu2zumDD5vy2BuSHvFZU0a6RDmgb&index=9

### Example Implementation

- https://github.com/stevus/rust_browser_part_2
- https://github.com/stevus/rust_browser_part_3

## Networking

This module handles all of complexity / subtlety of the HTTP protocol eg data transfer, expires headers, different versions, TLS etc.

Url Request Methods
Url Multi IO Threaded Request Methods for CSS, Images, Media and JS files, these have to be live to be fast and efficient.

Other things to consider:
- How many concurrent connections to use?
- Error reporting to the user
- Proxies
- User options

| Library  | Browser  |
| - | - |
| Necko  | Firefox  |
|   |   |

## Rendering Engine

This module handles how to interpret the parsed HTML and creating a plan to displaying it on the screen. Man years have gone into development of different versions of this module.

A Regular Expression Engine to pre find all required HTML, CSS, JS objects and methods and counts to pre set the rendering engine before the rendering loop begins.

Things like the id, tags with their widets and CSS Nested Rules need to be combined in each render loop, with some examples below:
- A set of both Horizontal and Vertical that will handle the Cells below as box Frames for div 1 sections→
- A Canvas or Frame that allows painting or drawing widgets and shapes as box Frames for div 1 to div 6 sections→
- A combo of a rectangle, a label or text widget stacked for block level elements —the cells background, spacing's and colored border
- A combo of a rectangle a label or text widget for Hyperlink Elements
- A combo of a rectangle, a button widget for button widgets with added background borders provided by the extra drawn rectangle on the canvas.
- A combo for every other widget the same such as entry, text entry, combo box, scroll box, radio buttons, check boxes, dividers for hr tags etc.

All of this above requires massive libraries in pairs for either CSS float or display to handle Horizontal and Vertical and to store all their tag or id names by counts and sections to allow JS to do after render methods.

The cell allows margins and borders between the rectangle object and the label or widget objects.

Margins and padding are easily added into the widgets as integers using math and by their own names which some may require minor Tokenizing from the CSS Tokenizer earlier: Regular Expressions do not like background-color or text-width where they are confused bgy width and color after a delimiter “-color”or”-width” so minor tokenizing is required for such.

```
width=parent_width+margin_left # The Frame Notice the Regular Expression Tokenized “-” to ”_” in margin_left
width=parent_width+padding_left etc. # The Cell
```

![](./main-qimg-b3a478b767b23d9452241a513bdbb4c3.webp)
A Pic of Chrome beside Tk testing HTML Cell Rendering to adjust border and spacing properties.

It does require math within the Cell Methods also. 

CSS can be transferred without allot of Tokenizing simply by assigning the CSS value directly to the widgets value variables. Such as background=background-color etc. 

Width and height have to be carried and returned for each new widtget combo in the stack also.

Nothing will fully match between Webkit, Firefox and Edge spacing because of NCSA Mosaic Widgets and they also do not fully match in many ways because of differences between Spyglass and Netscape Navigator’s having a different CSS Engine while both were developed by both Sun Micro Systems and Microsoft to render CSS differently.

| Library  | Browser  |
| - | - |
| Trident  | Internet Explorer  |
| Gecko  | Firefox  |
| Webkit  | Safari and Chrome 0-27  |
| KHTML  |  KDE desktop environment. Webkit forked from KHTML some years ago |
|  Elektra |  Opera 4-6 |
|  Presto |  Opera 7-12  |
| Blink  |  Chrome 28+, Opera 15+, webkit fork |

- https://joshondesign.com/2020/03/24/type_madness
- https://joshondesign.com/2020/04/08/rust5_tree
- https://joshondesign.com/2020/04/11/rust_layout
- https://joshondesign.com/2020/04/13/browser_render
- https://limpet.net/mbrubeck/2014/11/05/toy-layout-engine-7-painting.html

- https://www.youtube.com/watch?v=8e37RsyiGSE&list=PLJbE2Yu2zumDD5vy2BuSHvFZU0a6RDmgb&index=11
- https://www.youtube.com/watch?v=GuzZqrlc52s&list=PLJbE2Yu2zumDD5vy2BuSHvFZU0a6RDmgb&index=12
- https://www.youtube.com/watch?v=rszgtm7i0n8&list=PLJbE2Yu2zumDD5vy2BuSHvFZU0a6RDmgb&index=13
- 

### Example Implementation

- https://github.com/stevus/rust_browser_part_3
- https://github.com/stevus/rust_browser_part_4
- https://github.com/stevus/rust_browser_part_5

## Javascript Engine

A Javascript engine consists of a Lexer and a Parser.

Several of these tend to be tied to a particular rendering engine.

| Library  | Browser  |
| - | - |
| SpiderMonkey  | Gecko/Firefox  |
| TraceMonkey  |  SpiderMonkey in Firefox 3.1 and introduces JIT (just-in-time) compilation |
| KJS  | Konqueror, tied to KHTML  |
|  JScript | Trident, Internet Explorer  |
| JavascriptCore  | Webkit by the Safari browser  |
| SquirrelFish  |  Webkit and adds JIT like TraceMonkey |
| V8  | Google's Javascript engine used in Chrome and Opera  |
|   |   |

## GUI Toolkit

This is the module that draws the elements created by the rendering engine to the screen .

| Library  | Browser  |
| - | - |
| wxWidgets  |   |
| Qt  |   |
| Tcl/Tk  |   |
| GTK  |   |
|   |   |

## User Interface

This module handles displaying the UI for operations such as:
- Navigation between pages
- Page history
- Clearing temporary files
- Typing in a URL
- Autocompleting URLs

| Library  | Browser  |
| - | - |
| skia  | chrome  |
|   |   |

## Web Browser Projects

- https://joshondesign.com/tags/rust
- https://github.com/tensor-programming/
  - https://github.com/tensor-programming/rust_browser_6_final
- https://github.com/joshmarinacci/rust-minibrowser
- https://limpet.net/mbrubeck/2014/08/08/toy-layout-engine-1.html
  - https://github.com/mbrubeck/robinson
- https://github.com/plateaukao/einkbro
- https://github.com/twilco/kosmonaut
- https://news.ycombinator.com/item?id=19553941

## Open Source Web Browsers

- https://librewolf.net/
- https://www.waterfox.net/
- https://arc.net/
- https://www.brow.sh/
  - https://news.ycombinator.com/item?id=17487552
- https://servo.org/
  - https://github.com/rockxcn/book-1/blob/master/Develop%20the%20Servo%20Web%20Browser%20Engine%20using%20Rust.pdf
- https://awesomekling.github.io/Ladybird-a-new-cross-platform-browser-project/
- https://news.ycombinator.com/item?id=32809126
- https://news.ycombinator.com/item?id=24170201

## How Web Browsers Work

- https://developer.chrome.com/blog/inside-browser-part1/
- https://hacks.mozilla.org/2017/10/the-whole-web-at-maximum-fps-how-webrender-gets-rid-of-jank/
- https://www.peteresnyder.com/static/papers/speedreader-www-2019.pdf

## Libraries related to Web Browsers

- https://github.com/cixtor/readability
- https://kas-gui.github.io/blog/state-of-GUI-2022.html

## Ad Block for Web Browsers

- https://github.com/brave/adblock-rust
- https://www.cs.ucr.edu/~zhiyunq/pub/pets17_anti_adblocker.pdf
