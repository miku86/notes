# CSS Grid

Sources:

* https://scrimba.com/g/gR8PTE

## Why

* very easy to create 2-dimensional layout
* simple to use (no `row`s and `col-xs-8`s)
* styling in css-file, not html-file
* no frameworks like bootstrap needed
* browser support at 77% (2017 Dec)
* Grid is made for two dimensional layouts and Flexbox is made for one dimensional layouts

## How

Setup:

* container for the whole grid `display: grid`

Width:

* set fix width for items `grid-template-columns: 100px auto 100px;` // 3 item with absolute width

* set auto width for items `grid-template-columns: 1fr 2fr 1fr;` // 3 item with relative width

* shortcut for auto width for items `grid-template-columns: repeat(3, 1fr);` // 3 items - every one fraction of whole width

Height:

* set height of the items `grid-template-rows: 30px;` // first row 30px

Shortcut Height and Width:

* shortcut for columns and rows together: `grid-template: repeat(2, 30px) / repeat(3, 1fr);`

Gaps:

* for gaps between items `grid-gap: 2px`

Specific Item Width or Height:

* giving specific item width/height: `grid-[column/row]: 1 / 3` // from line 1 to line 3
* giving specific item width/height: `grid-[column/row]: 1 / -1` // from line 1 to last line
* giving specific item width/height: `grid-[column/row]: span 2` // two lines wide/high

Templates:

* defining template: `grid-template-area`
* using `grid-area: var` in the specific div (`.` instead of `var` for blank cells)

Automatic Fit:

* `grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));` // screen gets filled with as many as possible 100px items, but scaling every item up to fill entire screen
*  `grid-auto-rows: 100px;` // for sizing all rows with 100px
* `grid-auto-flow: dense` // fills holes in the grid

Center Content in Grid

* `justify-content: center`
* `align-content: center`
