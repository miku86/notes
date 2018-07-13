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

### Reusable Code#reusable-code

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

## Responsive Web Design

## Preprocessors

## jQuery

## Transforms

## Transitions & Animations

## Feature Support & Polyfills

## Extending Semantics & Accessibility

## Start Learning Advanced HTML & CSS
