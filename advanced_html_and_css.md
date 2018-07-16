Source: [Shay Howe](https://learn.shayhowe.com/advanced-html-css/)

# Advanced HTML & CSS

## Performance & Organization

- organization and architecture of a code base can greatly affect the speed of development, but also the speed at which pages render
- both can be sizeable concerns not only for developers but also users
- taking the time to design the right structure for a code base, and identify how all of the different components will work together, can speed up production and make for a better experience all around
- 20% of the optimizations will speed up roughly 80% of the website.

### Strategy & Structure

#### Style Architecture

- One practice includes separating styles based on intent, which includes creating directories for common base styles, user interface components, and business logic modules.

```
# Base
  – normalize.css
  – layout.css
  – typography.css

# Components
  – buttons.css
  – list.css
  – nav.css

# Modules
  – footer.css
  – header.css
```

- three directories, all with individual groups of styles
- goal is to start thinking of websites as systems rather than individual pages
- notice how there aren’t any page specific styles here

- base directory includes common styles to be used across the entire website
- components directory includes styles for specific user interface elements which are broken down into different component files such as buttons
- modules directory includes styles for different sections of a page, which are determined by business needs.

- component styles are purely interface driven and have nothing to do with the core business logic of the website
- modules then include styles specific to the business logic
- when marking up a module in HTML it is common to use different user interface components within it
- e.g. sidebar of a page may have list and button styles that are defined within component styles while other styles needed for the sidebar are inherited from the module style
- separation of style encourages well thought out presets and the ability for styles to be widely shared and reused

#### Object Oriented CSS

- two principles include Separate structure from skin, Separate content from container

- separating structure from skin: includes abstracting the layout of an element away from the theme of a website. The structure of a module should be transparent, allowing other styles to be inherited and displayed without conflict. Most commonly this requires a solid grid and layout structure, along with well crafted modules.

- separating content from the container: involves removing the dependency of a parent element nesting children elements. A heading should look the same regardless of its parent container. To accomplish this, elements need to inherit default styles, then be extended with multiple classes as necessary.

#### Choosing a Methodology

- Choosing which methodology to use, is completely up to you and what you feel is best for a given website
- BEM, OOCSS or SMACSS works well

### Performance Driven Selectors

#### Keep Selectors Short

- benefits: minimizing specificity, allowing for better inheritance and portability, and improving efficiency
- overall goal with short selectors is to decrease specificity, creating cleaner, more charitable code

```
/* Bad */
header nav ul li a {...}

/* Good */
.primary-link {...}
```

#### Favor Classes

- stay away from ID selectors as they are overly specific and do not allow for any repetition
- using an ID isn’t a whole lot different than using `!important`
- classes are great, they render quickly, allow for styles to be reused, and are already commonly used in building a website
- key selector is the selector unit at the end, furthest to the right
- key selector is crucial as it identifies the first element a browser is going to find
- having a poor key selector can send the browser on a wild goose hunt
- use a class to be more unique simply for the benefit of performance
- do not prefix class selectors with an element, doing so prohibits those styles from easily being applied to a different element and increases the overall specificity of the selector

```
/* Bad */
article.feat-post {...}

/* Good */
.feat-post {...}
```

### Reusable Code

- largest performance drawbacks: bloated file sizes and unnecessary browser rendering
- quick way to cut down on file sizes is to reuse styles as much as possible
- repeating styles or interface patterns should be combined, allowing code to be shared
- if two modules share a background, rounded corners, and a box shadow there is no reason to explicitly state those same styles twice
- they can be combined, within a single class, allowing the styles to be written once and then shared

- reusing code doesn’t have to come at the cost of semantics either
- pair selectors together, separating them with a comma
- bind styles to one class, then using multiple classes on the same element

```
/* Bad */
.news {
  background: #eee;
  border-radius: 5px;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .25);
}
.social {
  background: #eee;
  border-radius: 5px;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .25);
}

/* Good */
.news,
.social {
  background: #eee;
  border-radius: 5px;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .25);
}

/* Even Better */
.modal {
  background: #eee;
  border-radius: 5px;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, .25);
}
```

### Minify & Compress Files

- removing duplicate and unnecessary code is the best way to cut down on file size
- minifying and compressing files, such as HTML, CSS, and JavaScript files
- images may be compressed, removing any unnecessary comments and color profiles

#### gzip Compression

- gzip compression takes common files and identifies similar strings to compress down
- the more matching strings identified, the smaller the file can be compressed
- to gzip files an .htaccess file needs to be added to the root directory of the web server, labeling the specific files to be gzipped
- only works on Apache web servers, which need to have the following modules enabled

`request headers: accept-encoding:` which compressions are supported
`response header: content-encoding:` which compression is actually used

#### Image Compression

- compressing images will greatly help keep the file size under control
- many people steer away from compressing images in fear that compression involves reducing the quality of the image itself
- for the most part this is incorrect, and images can be compressed in a lossless fashion, allowing unnecessary color profiles and comments to be removed from the image without changing the quality of the image at all
- **best tools: ImageOptim for Mac and PNGGauntlet for Windows**
- setting an image’s dimensions in HTML by way of the height and width attributes does help render the page quicker
- but: using a larger image, then scaling it down with the height and width attributes is bad practice as it loads more data than necessary

### Reduce HTTP Requests

- next to file size, the number of HTTP requests a website makes is one of the largest performance pitfalls
- each time a request is made to the server the page load time increases
- some request have to finish before others can start, and too many request can bloat the server

#### Combine Like Files

- the easiest way to reduce the number of HTTP requests is to combine like files
- combine all of the CSS files into one and all of the JavaScript files into one
- combining these files then compressing them creates one, hopefully small, HTTP request

- the CSS should be loaded at the beginning, within the head
- the JS should be loaded at the end, just before the closing body tag
- reason: CSS can be loaded while the rest of the website is being loaded as well
- JS can only render one file at a time, thus prohibiting anything else from loading

#### Image Sprites

- the goal here is to cut down the number of HTTP requests made by using multiple background images
- to create a sprite take a handful of background images, ones that are commonly used, and arrange them into one single image
- then using CSS add the sprite as a background image to an element, and use the background-position property to display the correct background image
- think of the background image sliding around behind elements, only to expose the proper background image on a given element

#### Image Data URI

- instead of spriting images, the encoded data for an image can be included within HTML and CSS directly by way of the data URI, removing the need for a HTTP request all together
- using the image data URI works great for small images, likely to never change, and where the HTML and CSS can be heavily cached
- problems with data URIs. They can be difficult to change and maintain, leading to having to generate another encoding
- if using data URIs helps cut down a few HTTP requests, and the HTML or CSS can be heavily cached, the benefits tend to outweigh the risk

### Cache Common Files

- another way to help cut down HTTP requests, and to serve up pages faster, is to cache common files
- the browser doesn’t have to request the same files again on repeating visits for quite some time
- setting the expires headers for caching files can be set within the .htaccess file.
- images, videos, web fonts, and common media types are often cached for a month
- CSS and JavaScript files are often cached for a year
- the file name will need to be changed, preferably versioned, in order to be loaded
- alternatively, the expires headers can be changed to a smaller period of time.

---

## Detailed Positioning

- ability to float elements side by side provides a nice, clean layout that is receptive to the different elements on a page
- when more strict control is needed, elements may be positioned using relative or absolute positioning
- new: Flexbox and Grid

### Floats

- left out to not being best practice in 2018 => Flexbox and Grid

### Position Property

#### Position Static

- default value ion value of static

#### Position Relative

- relative value is very similar to that of the static value
- primary difference is that the relative value accepts the box offset properties top, right, bottom, and left to shift the element from its default position in any direction
- the element still remains in the normal (= static) flow of the page
- other elements will not impede on where the relatively positioned element was originally placed, the relatively positioned element may overlap or underlap other elements without moving them from their default position

#### Position Absolute

- elements are positioned directly in relation to their containing parent whom is relatively or absolutely positioned
- accept box offset properties, however they are removed from the normal flow of the document
- using an absolutely positioned element and not specifying any box offset property will position the element in the top left of its closest relatively positioned parent.

#### Position Fixed

- fixed works just like that of absolute, however the positioning is relative to the browser viewport, and it does not scroll with the page
- elements will always be present no matter where a user stands on a page
- box offset properties with fixed positioning will produce the same behaviors as an absolutely positioned element

#### Fixed Header or Footer

- one of the most common uses of fixed positioning is to build a fixed header or footer, that always stays within the viewport for users to interact with

#### Z-Index Property

- to change the order of how these elements are stacked, also known as the z-axis, the z-index property is to be used
- elements are positioned upon the z-axis as they appear within the DOM
- elements coming at the top of the DOM are positioned behind elements coming after them
- the element with the highest z-index value will appear on the top regardless of its placement in the DOM
- to apply the z-index property to an element, you must first apply a position value of relative, absolute, or fixed
-

In the example below, without the z-index property each box will be positioned precisely, starting with box two sitting on top of box one, then box three sitting on top of box two, and so forth. Reordering the stacking with the z-index property now positions box two on top of every other box, followed by box three underneath it, and box four underneath box three.

---

## Complex Selectors

- selectors are one of the most important parts of CSS
- they shape the cascade and determine how styles are to be applied to elements on a page

### Common Selectors

- most common selectors: type (`h1`), class (`.box`), and ID (`#intro`)
- type: based on its type in HTML
- class: based on its class attribute value, may be reused on multiple elements
- ID: based on its ID attribute value, is unique and should only be used once per page

### Child Selectors

- child selectors provide a way to select elements that fall within one another
- can be made two different ways, using either descendant or direct child selectors

#### Descendant Selector

- most common child selector, which matches every element that follows an identified ancestor
- selects an element that resides anywhere within an identified ancestor element
- does not have to come directly after the ancestor element inside the document tree
- created by spacing apart elements within a selector
- `article h2`: no matter where a h2 element lives, so long as it is within the article element, it will always be selected

#### Direct Child Selector

- at times only the direct children of a parent element need to be selected, not every instance of the element nested deeply inside of an ancestor
- selects an element that resides immediately inside an identified parent element
- `article > p`: is a direct child selector only identifying p elements that fall directly within an article element

### Sibling Selectors

- elements that share a common parent
- two ways: general sibling and adjacent sibling selectors

#### General Sibling Selector

- selects an element that follows anywhere after the prior element, in which both elements share the same parent
- tilde character `~` between two elements within a selector
- the first element identifies what the second element shall be a sibling with and both of which must share the same parent
- `h2 ~ p`: looks for p elements that follow and share the same parent of any h2 elements. In order for a p element to be selected it must come after any h2 element

#### Adjacent Sibling Selector

- selects an element that follows directly after the prior element, in which both elements share the same parent
- plus character `+` between the two elements
- the first element identifies what the second element shall directly follow after and be a sibling with, and both of which must share the same parent
- `h2 + p`: only p elements directly following after h2 elements will be selected, both of which must also share the same parent element

### Attribute Selectors

#### Attribute Present Selector

- selects an element if the given attribute is present, regardless of any actual value
- include the attribute name in square brackets, []
- `a[target] {...}` => `<a href="#" target="_blank">...</a>`

#### Attribute Equals Selector

- selects an element if the given attribute value exactly matches the value stated
- inside of the square brackets following the attribute name include the desired matching value
- `a[href="http://google.com/"] {...}` => `<a href="http://google.com/">...</a>`

#### Attribute Contains Selector

- selects an element if the given attribute value contains at least once instance of the value stated
- the asterisk character `*` may be used within the square brackets of a selector
- denotes that the value to follow only needs to appear or be contained within the attribute value
- `a[href*="login"] {...}` => `<a href="/login.php">...</a>`

#### Attribute Begins With Selector

- selects an element if the given attribute value begins with the value stated
- use the circumflex accent `^`
- `a[href^="https://"] {...}` => `<a href="https://chase.com/">...</a>`

#### Attribute Ends With Selector

- selects an element if the given attribute value ends with the value stated
- use the dollar sign `$`
- `a[href$=".pdf"] {...}` => `<a href="/docs/menu.pdf">...</a>`

#### Attribute Spaced Selector

- selects an element if the given attribute value is whitespace-separated with one word being exactly as stated
- use the tilde character `~`
- `a[rel~="tag"] {...}` => `<a href="#" rel="tag nofollow">...</a>`

#### Attribute Hyphenated Selector

- selects an element if the given attribute value is hyphen-separated and begins with the word stated
- uses the vertical line character `|`
- `a[lang|="en"] {...}` => `<a href="#" lang="en-US">...</a>`

### Pseudo-classes

- are similar to regular classes in HTML however they are not directly stated within the markup, instead they are dynamically populated as a result of users’ actions or the document structure

#### Link Pseudo Class

- `:link`: selects a link that has not been visited by a user
- `:visited`: selects a link that has been visited by a user

#### Action Pseudo Class

- `:hover`: selects an element when a user has hovered their cursor over it
- `:active`: selects an element when a user has engaged it
- `:focus`: selects an element when a user has made it their focus point

#### State Pseudo Class

- `:enabled`: selects an element in the default enabled state
- `:disabled`: selects an element in the disabled state
- `:checked`: selects a checkbox or radio button that has been checked
- `:indeterminate`: selects a checkbox or radio button that neither been checked or unchecked, leaving it in an indeterminate state

#### Structural Pseudo Class

- `li:first-child`: selects an element that is the first within a parent
- `li:last-child`: selects an element that is the last within a parent
- `div:only-child`: selects an element that is the only element within a parent
- `p:first-of-type`: selects an element that is the first of its type within a parent
- `p:last-of-type`: selects an element that is the last of its type within a parent
- `img:only-of-type`: selects an element that is the only of its type within a parent
- `li:nth-child(2n+3)`: selects an element that matches the given number or expression, counting all elements from the beginning of the document tree
- `li:nth-last-child(3n+2)`: selects an element that matches the given number or expression, counting all elements from the end of the document tree
- `p:nth-of-type(3n)`: selects an element that matches the given number or expression, counting only elements of its type from the beginning of the document tree
- `p:nth-last-of-type(2n+1)`: selects an element that matches the given number or expression, counting only elements of its type from the end of the document tree

### Pseudo-elements

- dynamic elements that don’t exist in the document tree, and when used within selectors these pseudo-elements allow unique parts of the page to be stylized
- only one pseudo-element may be used within a selector at a given time.

#### Textual Pseudo-elements

- `.alpha:first-letter`: selects the first letter of text within an element
- `.bravo:first-line`: selects the first line of text within an element

#### Generated Content Pseudo-elements

- `div:before`: creates a pseudo-element inside the selected element at the beginning
- `a:after`: creates a pseudo-element inside the selected element at the end

#### Fragment Pseudo-element

- `::selection`: selects the part of a document which has been selected, or highlighted, by a users’ actions

---

## Responsive Web Design

- it is hard to find someone who doesn’t own a mobile device connected to the Internet
- with the growth in mobile Internet usage comes the question of how to build websites suitable for all users
- the industry response to this question has become responsive web design, also known as RWD.

### Responsive Overview

- is the practice of building a website suitable to work on every device and every screen size, no matter how large or small, mobile or desktop
- is focused around providing an intuitive and gratifying experience for everyone

#### Responsive vs. Adaptive vs. Mobile

- Responsive and adaptive web design are closely related, and often transposed as one in the same
- responsive means to react quickly and positively to any change
- adaptive means to be easily modified for a new purpose or situation
- a combination of the two is ideal, providing the perfect formula for functional websites
- mobile means to build a separate website commonly on a new domain solely for mobile users, it normally isn’t a great idea
- mobile websites can be extremely light but they do come with the dependencies of a new code base and browser sniffing, all of which can become an obstacle for both developers and users

- currently the most popular technique lies within RDW, favoring design that dynamically adapts to different browser and device viewports, changing layout and content along the way. This solution has the benefits of being all three, responsive, adaptive, and mobile
- RWD is broken down into three main components: flexible layouts, media queries and flexible media

### Flexible Layouts

- flexible layouts is the practice of building the layout of a website with a flexible grid, capable of dynamically resizing to any width, built using relative length units, most commonly percentages or em units
- do not advocate the use of fixed measurement units, such as pixels or inches
- reason: the viewport height and width continually change from device to device
- website layouts need to adapt to this change and fixed values have too many constraints
- easy formula to help identify the proportions of a flexible layout using relative values: target ÷ parent = relative size
- the formula is based around taking the target width of an element and dividing it by the width of it’s parent element, the result is the relative width of the target element

#### Relative Viewport Lengths

vw: Viewports width
vh: Viewports height
vmin: Minimum of the viewport’s height and width
vmax: Maximum of the viewport’s height and width

#### Flexible Grid

- using the flexible grid formula we can take all of the fixed units of length and turn them into relative units
- no matter how wide the parent container becomes, the section and aside margins and widths scale proportionally
- taking the flexible layout concept and formula and reapplying it to all parts of a grid will create a completely dynamic website, scaling to every viewport size
- for even more control within a flexible layout, you can also leverage the min-width, max-width, min-height, and max-height properties
- at times the width of a browser viewport may be so small that even scaling the the layout proportionally will create columns that are too small to effectively display content
- in this event, media queries can be used to help build a better experience

### Media Queries

- Media queries provide the ability to specify different styles for individual browser and device circumstances, the width of the viewport or device orientation

#### Initializing Media Queries

- couple different ways to use media queries: using the @media rule inside of an existing style sheet, importing a new style sheet using the @import rule, or by linking to a separate style sheet from within the HTML document
- it is recommended to use the @media rule inside of an existing style sheet to avoid any additional HTTP requests

#### Logical Operators in Media Queries

- three logical operators available for use within media queries: `and`, `not`, `only`

```
<!-- The example below selects all media types between 800 and 1024 pixels wide -->
@media all and (min-width: 800px) and (max-width: 1024px) {...}
```

```
<!-- only screens in a portrait orientation that have a user agent capable of rending media queries -->
@media only screen and (orientation: portrait) {...}
```

#### Media Features in Media Queries

- Media features identify what attributes or properties will be targeted within the media query expression

#### Height & Width Media Features

- one of the most common media features revolves around determining a height or width
- most commonly used features include `min-width` and `max-width`
- may be any length unit, relative or absolute.
- `@media all and (min-width: 320px) and (max-width: 780px) {...}`

#### Orientation Media Feature

- determines if a device is in the landscape or portrait orientation
- landscape mode is triggered when the display is wider than taller
- portrait mode is triggered when the display is taller than wider
- `@media all and (orientation: landscape) {...}`

#### Aspect Ratio Media Features

- `aspect-ratio` and `device-aspect-ratio` specifies the width/height pixel ratio of the targeted rendering area or output device
- min and max prefixes are available to use with the different aspect ratio features
- consists of two positive integers separated by a forward slash
- `@media all and (min-device-aspect-ratio: 16/9) {...}`

#### Resolution Media Feature

- specifies the resolution of the output device in pixel density
- also accepts dots per pixel (1.3dppx), dots per centimeter (118dpcm), and other length based resolution values.
- `@media print and (min-resolution: 300dpi) {...}`

#### Identifying Breakpoints

- when building a responsive website it should adjust to an array of different viewport sizes, regardless of the device
- breakpoints should only be introduced when a website starts to break, look weird, or the experience is being hampered.
- your instinct might be to write media query breakpoints around common viewport sizes as determined by different device resolutions, such as 480px, 768px, 1024px etc. This is a bad idea
- new devices and resolutions are being released all of the time, trying to keep up with these changes could be an endless process

### Mobile First

- one popular technique with using media queries is called mobile first
- it includes using styles targeted at smaller viewports as the default styles for a website, then use media queries to add styles as the viewport grows
- the operating belief behind mobile first design is that a user on a mobile device shouldn’t have to load the styles for a desktop computer only to have them over written with mobile styles later, saving mobile data
- the majority of Internet consumption will be done on a mobile device, plan for them accordingly and develop intrinsic mobile experiences

```
/* Default styles first then media queries */
@media screen and (min-width: 400px)  {...}
@media screen and (min-width: 600px)  {...}
@media screen and (min-width: 1000px) {...}
@media screen and (min-width: 1400px) {...}
```

### Viewport

#### Viewport Height & Width

- using the viewport meta tag with either the height or width values will define the height or width of the viewport respectively
- it is recommended that you use the device defaults by applying the device-height and device-width values
- `<meta name="viewport" content="width=device-width">`

#### Viewport Scale

- to control how a website is scaled on a mobile device, and how users can continue to scale a website, use the minimum-scale, maximum-scale, initial-scale, and user-scalable properties
- the `initial-scale` of a website should be set to 1 as this defines the ratio between the device height, while in a portrait orientation, and the viewport size
- `<meta name="viewport" content="initial-scale=1">`
- the minimum-scale and maximum-scale values determine how small and how large a viewport may be scaled
- these values should not be set to the same value as the initial-scale, this would disable any zooming

#### Viewport Resolution

- letting the browser decide how to scale a website based off any viewport scale values usually does the trick

#### Combining Viewport Values

- the viewport meta tag will accept individual values as well as multiple values, allowing multiple viewport properties to be set at once
- one of the recommended viewport values is outlined below, using both the width and initial-scale properties.
- `<meta name="viewport" content="width=device-width, initial-scale=1">`

### Flexible Media

- as viewports begin to change size media doesn’t always follow suit
- images, videos, and other media types need to be scalable, changing their size as the size of the viewport changes
- one quick way to make media scalable is by using the max-width property with a value of 100%, doing so ensures that as the viewport gets smaller any media will scale down according to its containers width

```
img, video, canvas {
  max-width: 100%;
}
```

#### Flexible Embedded Media

- unfortunately the max-width property doesn’t work well for all instances of media, specifically around iframes and embedded media
- when it comes to third party websites, such as YouTube, who use iframes for embedded media this is a huge disappointment
- the embedded element needs to be absolutely positioned within a parent element with a width of 100% and a height of 0

---

## Preprocessors

- writing HTML and CSS may feel a bit taxing, requiring a lot of the same tasks to be completed over and over again
- these different tasks, while commonly small, do add up to quite a bit of inefficiency
- a preprocessor is a program that takes one type of data and converts it to another type of data
- Haml and Sass found many additional ways to empower HTML and CSS, not only by removing the inefficiencies but also in creating ways to make building websites easier and more logical

### Haml (HTML abstraction markup language)

- is a markup language with the single goal of providing the ability to write beautiful markup
- code written in Haml is later processed to HTML
- Haml promotes DRY and well structured markup, providing a pleasing experience for anyone having to write or read it

#### Installation

- requires Ruby to be compiled to HTML
- use gem to install haml
- files written in the Haml markup should be saved with the file extension of .haml

#### Doctype

- the default doctype in Haml is the HTML 1.0 Transitional document type so in order to make this the HTML5 doctype the number five has to be passed in after the exclamation points, `!!! 5`

#### Declaring Elements

- within Haml elements only have one tag, the opening
- elements are initialized with a percent sign `%` and then indented to identify nesting

```
%body
  %header
    %h1 Hello World
  %section
    %p Lorem ipsum dolor sit amet.
```

#### Attributes

- attributes are declared directly after the element in either {} or () (Ruby or HTML)
- `%img{src: "shay.jpg", alt: "Shay Howe"}` or `%img(src="shay.jpg" alt="Shay Howe")`

#### Classes & IDs

- can be identified directly after the element
- class: `.`
- id: `#`
- may be mixed and matched, chaining them together in the appropriate format
- if a class or ID is used on a div the %div may be omitted, and the class or ID value can be used outright

```
%section.feature
%section#hello
%div.awesome => .awesome
```

#### Comments

- code can be commented out with the use of a single forward slash `/`
- blocks of code can be commented out by being nested underneath a forward slash

```
/ Commented line
Actual line
```

#### Silent Comments

- any content within a silent comment is completely removed from the page
- initialized with a dash then the number sign `-#`

```
-# Removed line
Actual line
```

#### Filters

- allowing different types of input to be used inside of Haml
- identified with a colon followed by the name of the filter `:markdown`
- `:css :erb :javascript :markdown :ruby :sass :scss`

### SCSS & Sass

- preprocessing languages which are compiled to CSS
- Sass came first and is a strict indented syntax
- SCSS followed shortly after providing the same firing power of Sass but with a more flexible syntax, including the ability to write plain CSS

#### Installation

- files written in SCSS or Sass need to have the .scss or .sass file extensions
- Sass can watch the file and recompile the CSS every time a change takes place
- single file: `sass --watch styles.sass:styles.css`
- folder: `sass --watch assets/sass:public/css`

#### Syntax

- primary difference between SCSS and Sass is their syntax
- SCSS isn’t much different than regular CSS, standard CSS will run inside of SCSS
- Sass is fairly strict and any indenting will prohibit the styles from compiling
- Sass omits all curly brackets and semicolons, relying on indentation and clear line breaks for formatting

SCSS

```
.new {
  color: #ff7b29;
  span {
    text-transform: uppercase;
  }
}
```

Sass

```
.new
  color: #ff7b29
  span
    text-transform: uppercase
```

#### SCSS vs. Sass

- boils down to personal preference, and is a decision to be made based on what is best for a specific team and project
- Sass requires less characters and provides a cleaner syntax
- Sass will not allow straight CSS input as SCSS does
- Sass has a bit more of a learning curve, however well worth learning

#### Nesting

- nesting quickly outlines identifiable selectors, however it is important not to go overboard
- do not nest selectors for unapparent reasons or go overboard nesting one selector under the prior one
- using specific selectors without raising specificity is important

#### Nesting Properties

- also possible to nest properties

```
div
  font:
    family: Baskerville, Palatino, serif
    style: italic
```

#### Parent Selector

- add styles to a previous selector with the use of the parent selector, implemented by using an ampersand `&`

```
a
  color: #0087cc
  &:hover
    color: #ff7b29
```

#### Parent Key Selector

- parent selector may also be used as the key selector, adding qualifying selectors to make compound selectors

#### Variables

- with Sass you can define variables and then reuse them as necessary
- variables are defined with a dollar sign `$`, followed by the variable name
- `$font-base: 1rem`

#### Variable Interpolation

- interpolation e.g. when being used in a class name, property name, or inside a string of plain text with `#{}`
- `.#{%location}`

#### Calculations

- ability to do calculations in a variety of different manners

#### Number Functions

- handful of built in functions, many of which are used to manipulate number values
- `percentage() round() ceil() floor() abs()`

#### Color

- one of the more popular color features in Sass is the ability to change a hexadecimal color and convert it into an RGBa value.
- `color: rgba(#8ec63f, .25)`

#### Color Alterations

- provide the ability to inverse colors, find complementary colors, mix colors together, or find the grayscale value of a color
- `invert() complement() mix() grayscale()`

#### HSLa Color Alterations

- take things a step further, adding in even more alterations
- `lighten() darken() saturate() desaturate() adjust-hue() fade-in() fade-out()`

#### Extends

- a way to easily share and reuse styles without having to explicitly repeat code or use additional classes, providing a perfect way to keep code modular
- are established by using the `@extend` rule followed by the selector to extend
- the original selector receives and additional selector, that of which is from the selector calling the extend

#### Imports

- one of nicest parts of Sass is its ability to import multiple .scss or .sass files and condense them into one single file
- condensing all of the files into one allows for multiple stylesheets to be used for better organization without the worry of numerous HTTP request
- instead of referencing all of the different stylesheets within an HTML document only reference the one Sass file importing all of the other stylesheets

#### Loops & Conditionals

- Sass supports different control directives

#### If Function

- `@if` tests an expressions then loads the styles beneath that expression should it return anything other than false or null

#### For Loop

- `@for $i from 1 to 3` will output styles up to, but not including, 3
- `@for $i from 1 through 3` will output styles up to, and including, 3.

#### Each Loop

- `@each` returns styles for each item in a list, list may include multiple comma separated items

#### While Loop

- `@while` repeatedly returns styles until the statement becomes false

### Other Preprocessors

- other popular preprocessors including Jade, Slim, LESS, Stylus, and CoffeeScript
- Projects built in Node.js may likely better benefit from Jade and Stylus
- the most important aspect to consider, though, is what your team is accustomed to using, do your research for each project and make the most educated decision

---

## Transforms

- the transform property comes in two different settings: two-dimensional and three-dimensional

### 2D Transforms

#### 2D Rotate

- provides the ability to rotate an element from 0 to 360 degrees
- a positive value will rotate an element clockwise, a negative value counterclockwise
- `transform: rotate(20deg)`

#### 2D Scale

- allows you to change the appeared size of an element
- default value is 1, therefore any value between .99 and .01 makes an element appear smaller while any value greater than or equal to 1.01 makes an element appear larger
- it is possible to scale only the height or width of an element using the scaleX and scaleY values
- `transform: scale(1.25)`
- `transform: scaleX(1.25)`
- `transform: scale(1.1, 1.3)`

#### 2D Translate

- pushs and pulls an element in different directions without interrupting the normal flow of the document
- the distance values used within the translate value may be any general length measurement, most commonly pixels or percentages
- positive values will push an element down and to the right of its default position while negative values will pull an element up and to the left of its default position
- `transform: translateX(-10px);`
- `transform: translateY(25%);`
- `transform: translate(-10px, 25%);`

#### 2D Skew

- is used to distort elements on the axis
- the distance calculation of the skew value is measured in units of degrees
- `transform: skew(5deg, -20deg);`

### Combining Transforms

- multiple transforms can be combined together
- list the transform values within the transform property one after the other without the use of commas
- `transform: rotate(25deg) scale(.75);`

### Transform Origin

- the default transform origin is the dead center of an element, both 50% horizontally and 50% vertically
- the values are treated like that of a background image position, using either a length or keyword value. 0 0 is the same value as top left, and 100% 100% is the same value as bottom right
- `transform-origin: 0 0`
- `transform-origin: 100% 100%`

### Perspective

- in order for three-dimensional transforms to work the elements need a perspective from which to transform
- the perspective for each element can be thought of as a vanishing point, similar to that which can be seen in three-dimensional drawings
- the perspective of an element can be set in two different ways: one way includes using the perspective value within the transform property on individual elements, the other includes using the perspective property on the parent element residing over child elements being transformed
- Using the perspective value within the transform property works great for transforming one element from a single, unique perspective. When you want to transform a group of elements all with the same perspective, or vanishing point, apply the perspective property to their parent element

#### Perspective Depth Value

- can be set as none or a length measurement
- the higher the value, the further away the perspective appears, thus creating a fairly low intensity perspective and a small three-dimensional change
- the lower the value the closer the perspective appears, thus creating a high intensity perspective and a large three-dimensional change
- imagine yourself standing 10 feet away from a 10 foot cube as compared to standing 1,000 feet away from the same cube. At 10 feet, your distance to the cube is the same as the dimensions of the cube, therefore the perspective shift is much greater than it will be at 1,000 feet, where the dimensions of the cube are only one one-hundredth of your distance to the cube. The same thinking applies to perspective depth values

#### Perspective Origin

- the same values used for the transform-origin property may also be used with the perspective-origin property
- the large difference between the two falls where the origin of a transform determines the coordinates used to calculate the change of a transform, while the origin of a perspective identifies the coordinates of the vanishing point of a transform

### 3D Transforms

- working with two-dimensional transforms we are able to alter elements on the horizontal and vertical axes, however there is another axis along which we can transform elements, giving us control of depth as well as length and width

#### 3D Rotate

- using rotateX allows you to rotate an element around the x axis, bent in half horizontally
- using rotateY allows you to rotate an element around the y axis, bent in half vertically
- using rotateZ allows an element to be rotated around the z axis.
- positive values will rotate the element around its dedicated axis clockwise, while negative values will rotate the element counterclockwise

#### 3D Scale

- transforming elements on the z axis isn’t extremely exciting when no other three-dimensional transforms are in place, as there is nothing in particular to scale

#### 3D Translate

- elements may also be translated on the z axis using the translateZ value
- a negative value here will push an element further away on the z axis, resulting in a smaller element
- using a positive value will pull an element closer on the z axis, resulting in a larger element
- while this may appear to be very similar to that of the two-dimensional transform scale value, it is actually quite different: being able to move an element on the z axis does have great benefits, like when building a cube

#### 3D Skew

- Skew is the one two-dimensional transform that cannot be transformed on a three-dimensional scale

#### Shorthand 3D Transforms

- there are also properties to write out shorthand three-dimensional transforms, including rotate3d, scale3d, transition3d and matrix3d
- these properties do require a bit more math, as well as a strong understanding of the matrices behind each transform

### Transform Style

- three-dimensional transforms will be applied on an element that is nested within a parent element which is also being transformed. In this event, the nested, transformed elements will not appear in their own three-dimensional space
- to allow nested elements to transform in their own three-dimensional plane use the transform-style property with the preserve-3d value
- the transform-style property needs to be placed on the parent element, above any nested transforms. The preserve-3d value allows the transformed children elements to appear in their own three-dimensional plane while the flat value forces the transformed children elements to lie flat on the two-dimensional plane

### Backface Visibility

- elements will occasionally be transformed in a way that causes them to face away from the screen. This may be caused by setting the rotateY(180deg) value for example
- set the backface-visibility property to hidden and you will hide the element whenever it is facing away from the screen

---

## Transitions & Animations

- with CSS3 transitions you have the potential to alter the appearance and behavior of an element whenever a state change occurs, such as when it is hovered over, focused on, active, or targeted
- animations within CSS3 allow the appearance and behavior of an element to be altered in multiple keyframes
- transitions provide a change from one state to another, while animations can set multiple points of transition upon different keyframes

### Transitions

- an element must have a change in state, and different styles must be identified for each state
- the easiest way for determining styles for different states is by using the :hover, :focus, :active, and :target pseudo-classes
- there are four transition related properties: transition-property, transition-duration, transition-timing-function, and transition-delay
- not all of these are required to build a transition, with the first three are the most popular

```
.box {
  background: #2db34a;
  transition-property: background;
  transition-duration: 1s;
  transition-timing-function: linear;
}
.box:hover {
  background: #ff7b29;
}
```

#### Transitional Property

- transition-property determines what properties will be altered
- if multiple properties need to be transitioned they may be comma separated within the transition-property value
- not all properties may be transitioned, only properties that have an identifiable halfway point: colors, font sizes, and the alike may be transitioned from one value to another as they have recognizable values in-between one another. The display property, for example, may not be transitioned as it does not have any midpoint

#### Transition Duration

- the duration in which a transition takes place is set using the transition-duration property
- the value of this property can be set using general timing values, including seconds (s) and milliseconds (ms)
- you can set multiple durations, one for each property, using comma separated values
- the order of these values when identifying individual properties and durations does matter

#### Transition Timing

- transition-timing-function is used to set the speed in which a transition will move
- a few of the more popular keyword values: linear, ease-in, ease-out, and ease-in-out
- linear: constant speed
- ease-in: starts slowly and speeds up
- ease-out: starts quickly and slows down
- ease-in-out: starts slowly, speeds up in the middle, then slows down again
- each timing function has a cubic-bezier curve behind it, which can be specifically set using the cubic-bezier(x1, y1, x2, y2) value

#### Transition Delay

- the delay sets a time value, that determines how long a transition should be stalled before executing

### Shorthand Transitions

- declaring every transition property individually can become quite intensive
- `transition` is capable of supporting all of these different properties and values
- you can set every value in the order of property, duration, timing-function and delay
- `transition: background 2s linear;`

### Animations

- transitions do a great job of building out visual interactions from one state to another and are perfect for these kinds of single state changes
- when more control is required, transitions need to have multiple states. this is where animations pick up where transitions leave off

#### Animations Keyframes

- to set multiple points at which an element should undergo a transition, use the @keyframes rule
- the @keyframes rule includes the name, breakpoints, and the properties intended to be animated

```
@keyframes slide {
  0% {
    left: 0;
    top: 0;
  }
  50% {
    left: 244px;
    top: 100px;
  }
  100% {
    left: 488px;
    top: 0;
  }
}
```

- the animation above is named slide
- the different keyframe breakpoints starting at 0% and working to 100% with an intermediate breakpoint at 50%
- the element properties to be animated are listed inside each of the breakpoints, left and top in the example above

#### Animation Name

- once the keyframes for an animation have been declared they need to be assigned to an element
- to do so, the animation-name property is used with the animation name, identified from the @keyframes rule, as the property value
- the animation-name declaration is applied to the element in which the animation is to be applied to

#### Animation Duration, Timing Function, & Delay

- animations need a duration declared using the animation-duration property
- timing function and delay can be declared using the animation-timing-function and animation-delay properties respectively

```
.stage:hover .ball {
  animation-name: slide;
  animation-duration: 2s;
  animation-timing-function: ease-in-out;
  animation-delay: .5s;
}
```

### Customizing Animations

- animations also provide the ability to further customize an element’s behavior, including the ability to declare the number of times an animation runs, as well as the direction in which an animation completes

#### Animation Iteration

- animations run their cycle once from beginning to end and then stop
- to have an animation repeat itself numerous times the animation-iteration-count property may be used
- `animation-iteration-count: infinite`

#### Animation Direction

- you may declare the direction an animation completes using animation-direction
- values include normal, reverse, alternate, and alternate-reverse

#### Animation Play State

- allows an animation to be played or paused using the running and paused keyword values respectively

#### Animation Fill Mode

- identifies how an element should be styled either before, after, or before and after an animation is run
- accepts four keyword values: none, forwards, backwards, and both

### Shorthand Animations

- the order of values within the animation property should be animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode and animation-play-state

---

## Feature Support & Polyfills

- common frustrations arise from trying to get a website to look and perform the same in every browser
- determine what is acceptable for a given website and work from there: if a website receives under a percent of traffic from Internet Explorer 6 it might make sense to drop support for it, if that percent is still contributing to thousands of dollars in sales, support may be mandatory

- when incorporating CSS3 properties, fallbacks are recommend to support older browsers
- other techniques include shivs and polyfills

### HTML5 Shiv

- HTML5 Shiv was created to provide the ability to use HTML5 elements within versions of Internet Explorer 8 and below and also allows them to be properly styled with CSS

### Detecting Browser Features

- referencing the HTML5 Shiv works well with a conditional comment, because the intention is to specifically target browsers that don’t support new HTML5 features and elements
- feature detection provides a way to write conditional CSS and JavaScript based on whether or not a browser supports a specific feature

#### Conditionally Applying CSS Styles

- CSS styles may be conditionally applied based on the features a given browser supports
- Modernizr has detection for the majority of the CSS3 properties and values, all of which can be found in the Modernizr documentation
- when working with CSS3 feature detection it is hard to know what the styles look like in browsers that do not support specific CSS3 features
- there is a bookmarklet called deCSS3 which disables any CSS3 features, doing so allows you to see what a website would look like without CSS3, and if your conditional styles are working

### Conditionally Loading Files

- Modernizr also provides a way to use feature detection in JavaScript. JavaScript polyfills and conditional files may be loaded based on the detection of a given feature with the help of jQuery and the jQuery getScript method

### Cross Browser Testing

- perhaps the most dreaded part of web design and development is cross browser testing
- the largest pitfalls live within Internet Explorer
- there are a handful of services out there that help with cross browser testing
- being able to interact with a browser, rather than seeing a rendered screenshot, is far more helpful for debugging code: one of the best ways to boot up multiple versions of Internet Explorer is by using multiple virtual machines, each with a different version of Internet Explorer
- Greg Thornton has built an automated installer for all of these vms: http://xdissent.github.io/ievms/

---

## Extending Semantics & Accessibility

- knowing how to write semantic and accessible code properly takes an understanding of how semantics and accessibility work, and how users and machines interpret them
- do your best to write the cleanest code possible, don’t use a meaningless element where another element might make more semantic sense, using a div where a h1 would be better fitted for example
- use semantic elements and attributes, as well as microdata and WAI-ARIA to extend the value of your code
- be an advocate for semantics and accessibility, provide reasoning why certain modules of content are marked up in a specific way

### Semantic Motivation

- semantics provide: unambiguous, shared meaning within content, accessibility, search and globalization, interoperability

### Structural Semantics

- structural semantics, specifically using the header, nav, article, section, aside, and footer elements, are used to provide additional background context to the content within them, communicating their core meaning to web browsers and other devices
- this is important, as it provides a better way to outline and structure pages, not to mention a more meaningful solution than divisions

#### Hiding Content

- every now and then you may want to hide a block of content on the page, perhaps showing or hiding an element depending on a user’s state
- most commonly, this is accomplished with the display: none; CSS declaration. While this does work, it is semantically incorrect
- a better option is to use the hidden Boolean attribute, which is a global attribute available to all elements for use. Functionally it performs the same way as the CSS declaration, but semantically it represents an element that should be hidden, or ignored, for the time being. Screen readers and other devices will recognize this, temporarily skipping it, where they may not done so with the CSS declaration
- imagine a blind user attempting to fill out a form and the first piece of content, before even filling out the form, is a success message. This is a poor user experience, and one that can easily be fixed using proper semantics

```
<!-- Good -->
<div hidden>...</div>

<!-- Not good -->
<div style="display: none;">...</div>
```

### Text Level Semantics

- the majority of content on the web lives within text, and we primarily browse the Internet looking for this content, using the proper semantic markup for text makes it easier for users to find what they need

#### Bolding Text

- the two main elements used in this case include strong and b. While these two elements have the same presentation they have completely different semantic meanings
- the strong element outlines text that has a strong importance
- the b element identifies text that is to be stylistically offset, without importance
- the b element should be used solely as a styling hook to change the presentation of an element, where the strong element should be used to identify significantly important text

```
<!-- Strong importance -->
<strong>Caution:</strong> Falling rocks.

<!-- Stylistically offset -->
This recipe calls for <b>bacon</b> and <b>baconnaise</b>.
```

#### Italicizing Text

- the two elements most commonly used are em and i
- the em element places a stressed emphasis on text
- the i element identifies text to be expressed in an alternate voice or tone
- using the em element really drives prominence with an added importance
- the i element is primarily used within dialog or prose, offsetting text without any added emphasis or importance

```
<!-- Stressed emphasis -->
I <em>love</em> Chicago!

<!-- Alternative voice or tone -->
The name <i>Shay</i> means a gift.
```

#### Underlining Text

- the two primary elements used to underline text are ins and u
- the ins element is used to identify text that has been recently added to the document
- the u element simply refers to an unarticulated annotation
- underlining text that is not a hyperlink can confuse users and cause quite a bit of frustration, use underlines with caution

#### Striking Text

- the two properties most commonly used include del and s
- the del element is used to identify text deleted or removed from the document
- the s element identifies text that is no longer accurate or relevant

#### Highlighting Text

- to highlight text for reference purposes the mark element should be used, it provides a clean, semantic way to identify text, specifically for reference purposes without having to use an un-semantic text level element

#### Abbreviations

- abbreviations, the shortened form of a phrase, can be semantically marked up in HTML using the abbr element
- the abbr element should be used along with the title attribute, of which includes the full value of the phrase being abbreviated
- the acronym element was originally used to distinguish acronyms from abbreviations but has since been deprecated, and shouldn’t be used

#### Sub & Superscripts

- subscripts and superscripts may be marked up accordingly using the sub and sup elements respectively
- these elements should be reserved for typographical conventions, not for presentational purposes

```
<!-- Subscript -->
H<sub>2</sub>O

<!-- Superscripts -->
1<sup>st</sup> Place
```

#### Meter & Progress

- to gauge scale or indicate progress the meter and progress elements should be used
- the meter element is used to measure a fixed value, one that does not change over time
- the progress element measures the progress of a increasing measurement

- the meter element may be used with the min, max, low, high, optimum, and value attributes. The min and max attributes set the lower and upper bounds of the range, where the value attribute sets the exact measured value. The low and high attributes identify what is to be considered the lower and higher parts of the range, while the optimum value identifies the most favorable part of the range, of which may be in the lower or higher parts

- the progress element indicates progress rather than a fixed measurement. It specifically represents the completion of a task, either by what is left to be completed or what has been completed thus far. There are two attributes that may be applied to the progress element, value and max. The value attributes indicates where the progress currently stands and the max attribute indicates what progress needs to be reached

#### Time & Address

- the time element may be used with the datetime attribute, depending on how the text within the element is formatted
- if the content is formatted with the correct time stamp then the datetime attribute may be omitted
- if the time is representing the date or time of a publication the pubdate Boolean attribute should be used
- the address element may be used to hold any contact information, including a physical address as well as a website or email address
- it should not include any further information than the contact information, and other content needs to be placed outside of the address element

#### Presenting Code

- presenting code snippets can be accomplished using either the code or pre elements
- the code element is commonly used to represent a fragment of code and is displayed in the default monospace font
- the code element is an inline level element and may be used within paragraphs of text
- for large blocks of code, the pre element can be used in conjunction with the code element. The pre element represent preformatted text and will display text exactly as it is typed, whitespace included. Nesting the code element within the pre element semantically identifies larger samples of code, which include whitepsace, displayed in a block level manner

```
<!-- Inline code samples -->
Use the <code>article</code> element.

<!-- Larger, block level code snippets -->
<pre><code>body {
  color: #666;
}</code></pre>
```

#### Line & Word Breaks

- occasionally you may want to include a line break within a line of text, in which case the br element may be used
- the br element does not have a closing tag
- line breaks are not to be used for thematic grouping of content
- paragraphs or other elements are better suited for thematic grouping
- line breaks are specifically to be used where line breaks exist as part of the content, for example as within addresses and poems
- you may also specify word breaking opportunities with the wbr element. Using the wbr element in the middle of a word ensures that, should the word need to wrap two lines, it does in a legible fashion

#### Side Comments

- the small element preserves the presentation of being displayed at a smaller font size, however it semantically means to be rendered as a side comments or small print, this often includes copyright information or legal print

#### Citations & Quotes

- the cite element refers to a title of work
- the q element identifies dialog or prose
- the blockquote element is used to code longer formed quotes

#### Hyperlink Attributes

##### Download Attribute

- the download attribute tells the browser to prompt a download for a file, rather than the default behavior of navigation to the file
- as an example, if the hyperlink reference attribute, href, is pointing to an image, the browser will prompt a user to download the image instead of opening the image within the browser
- the download attribute can serve as a Boolean attribute, downloading the file as is, or it may contain a value, of which becomes the file name once downloaded. Using a specific value here lets you name the file as you wish on your server while still providing users with a meaningful name

```
<!-- Boolean -->
<a href="twitter-logo.png" download>Twitter Logo</a>

<!-- With a value -->
<a href="twitter-logo.png" download="Logo">Twitter Logo</a>
```

##### Relationship Attribute

- the rel attribute identifies the relationship between the current document and the document being referenced. For example, when linking to a copyright statement the rel attribute value of copyright should be used

### Microdata

- Microdata is HTML extended with nested groups of name-value pairs that allow machines, including browsers and search engines, to pick up additional semantics and information for rich content
- adding microdata to your website is accomplished by using predetermined attributes and values. These attributes and values will then be interpreted, and extended, as intended
- the more popular uses of microdata reside within coding contact information and calendar events, however there are encoding models for products, reviews, and more
- one example of microdata at work is within Google, where microdata is interpreted and used within search results to display more relevant data. Often performing a search for a business location yields the address and sub sequential contact information within the results. Chances are this information is being pulled from microdata written on an existing website

#### Outlining Microdata

- Microdata is identified using three main attributes: itemscope, itemtype and itemprop
- the itemscope Boolean attribute declares the scope of each microdata item. Place this attribute on the parent element where all of the microdata information pertaining to this item should reside
- use the itemtype attribute to identify what microdata vocabulary should be used, some of the more popular microdata item types have been outlined at Schema.org
- once the scope and type of the item have been determined, properties may then be set by different elements which include the itemprop attribute. The value of this attribute determines what property is being referenced, and the content within the element itself most commonly determines the value of the property

#### Person Microdata

- when referring to a person the person microdata library should be used. Below is an example of what a person microdata item might look like. Please notice, the person item type is used, as is the postal address item type within it. Also, please notice the different item properties and their corresponding values

#### Event Microdata

- the event microdata is very similar to that of the person microdata, however it uses the event microdata library instead

### WAI-ARIA

- WAI-ARIA, also know as Web Accessibility Initiative — Accessible Rich Internet Applications, is a specification that helps make web pages and applications more accessible to those with disabilities
- it helps define roles (for what blocks of content do), states (for how blocks of content are configured), and additional properties to support assistive technologies

#### Roles

- setting WAI-ARIA roles is accomplished using the role attribute
- these roles then specify what certain elements and blocks of content do on a page.

`<header role="banner">...</header>`

- roles break down into four different categories: abstract, widget, document structure, and landmark roles
- document structure roles define the organizational structure of content on a page
- landmark roles define the regions of a page
- HTML5 introduced a handful of new structural elements which commonly match up against the document structure and landmark roles

#### States & Properties

- in combination with WAI-ARIA roles there are also states and properties which help inform assistive technologies how content is configured
- like roles, the states and properties are broken into four categories: widget attributes, live region attributes, drag-and-drop attributes, and relationship attributes
- the widget attributes support widget roles and are specific to the user interface and where users take actions
- the live region attributes may be applied to any element and are used to indicate content changes for assistive technologies, on page alerts and notifications for example
- drag-and-drop attributes supply information about drag-and-drop interface elements and provide alternate behaviors to assistive technologies
- relationship attributes outline the relationship between elements when the document structure cannot be determined
