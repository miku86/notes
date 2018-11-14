# CSS BEM for Beginners

Source: https://www.smashingmagazine.com/2018/06/bem-for-beginners/

## Summary

- BEM makes code reusable
- Reuse the layout
- Move layout fragments around within a project safely
- Move the finished layout between projects
- Create stable, predictable and clear code
- Reduce the project debugging time

---

## Only Use Classes, no other Selectors

- No `ID`: `ID` is unique, so you can't reuse it.
- No `Tag`: HTML page markup is unstable: A new design can change the nesting of the sections, heading levels etc. Any of these changes will break styles that are written for tags. Even if the design doesn’t change, the set of tags is limited.
- No `CSS Reset`: These styles affect all layout nodes, violate the independence of components, and make it harder to reuse them. Resetting and normalization cancel existing styles and replace them with other styles, which you will have to change and update later in any case.
- No Universal Selector `*`: The universal selector indicates that the project features a style that affects all nodes in the layout. This limits reuse of the layout in other. A universal selector can make the project code unpredictable.
- No `Nested Selectors`: Nested selectors increase code coupling and make it difficult to reuse the code. BEM doesn’t prohibit nested selectors, but it recommends not to use them too much.
- No `Combined Selectors`: Combined selectors are more specific than single selectors, which makes it more difficult to redefine blocks.

```
<button class="button button_theme_islands button_active">...</button>

/* No */
.button.button_theme_islands {}
.button.button_active {}

/* Yes */
.button_theme_islands {}
.button_active {}
.button {}
```

- No Combination of `Tag and Class`: Combining a tag and a class in the same selector (for example, `button.button`) makes CSS rules more specific, so it is more difficult to redefine them.
- No `Attribute` Selectors: Attribute selectors are less informative than class selectors.

Summary: `class` is the only selector that allows you to isolate the styles of each component in the project, increase the readability of the code and do not limit the re-use of the layout. CSS styles isolation is the most frequent start point of the BEM journey. But this is the least that BEM can give you.

---

## Basics

### Block and Elements

The interface consists of blocks that can include elements. Blocks are independent components of the page. An element can’t exist outside the block, so keep in mind that each element can belong to one block only.

The block name is always unique. It sets the namespace for elements and provides a visible connection between the block parts. Block names are long but clear in order to show the connection between components and to avoid losing any parts of these components when transferring the layout.

Consider this example with a form. The form is implemented using the form block. The block name is included in the `class` attribute:

`<form class="form" action="/">`

All parts of the form (the `form` block) that don’t make sense on their own are considered its elements. So the search box (`search`) and the button (`submit`) are `elements of the form block`. Classes also indicate that an element belongs to the block:

```html
<form class="form" action="/">
  <input class="form__search" name="s" />
  <input class="form__submit" type="submit" />
</form>
```

The block’s name is separated from the element’s name with two underscores. The important thing is that separators allow you to distinguish blocks from elements and modifiers programmatically.
Selector names make it clear that in order to move the form to another project, you need to copy all of its components:

```css
.form__search {
}
.form__submit {
}
```

Using blocks and elements for class names solves an important problem: It helps us get rid of nested selectors. All selectors in a BEM project have the same weight. That means it is much easier to redefine styles written according to BEM. Now, to use the same form in another project, you can just copy its layout and styles.

The idea of the naming of BEM components is that you can explicitly define the connection between the block and its elements.

### Modifiers and Mixes

Both modifiers and mixes make changes to a block and its elements.

#### Modifiers

A modifier defines the look, state and behavior of a block or an element. Adding modifiers is optional. Modifiers let you combine different block features, as you can use any number of modifiers. But a block or an element can’t be assigned different values of the same modifier.

Imagine the project needs the same search form as in the example above. It should have the same functions but look different (for example, the search forms in the header and in the footer of the page should differ). The first thing you can do to change the appearance of the form is to write additional styles.

In BEM, you can use a modifier to add new styles to the block:
`<form class="form form--original">`

The line indicates that the block was assigned a type modifier with the original value. In a classic scheme, the modifier name is separated from the block or element name with an underscore.

The form can have a unique color, size, type, or design theme. All these parameters can be set with a modifier: `<form class="form form--original form--size-m form--theme_forest">`

Important: A modifier contains only additional styles that change the original block implementation in some way. This allows you to set the appearance of a universal block only once, and add only those features that differ from the original block code into the modifier styles:

```css
.form {
  /* universal block styles */
}
.form--original {
  /* added styles */
}
```

You can use modifiers to apply universal components in very specific cases. The block and element code doesn’t change. The necessary combination of modifiers is created on the DOM node.

#### Mixes

A mix allows you to apply the same formatting to different HTML elements and combine the behavior and styles of several entities while avoiding code duplication. They can replace abstract wrapper blocks.

A mix means that you host several BEM entities (blocks, elements, modifiers) on a single DOM node. Similar to modifiers, mixes are used for changing blocks.

Blocks can differ not only visually but also semantically. For example, a search form, a registration form and a form for ordering cakes are all forms. In the layout, they are implemented with the “form” block but they don’t have any styles in common. It is impossible to handle such differences with a modifier.

Now you can make a search form from the universal form. Create an additional `search` class in the project. This class will be responsible only for the search. To combine the styles and behavior of the `.form` and `.search` classes, place these classes on a single DOM node:

```html
<form class="form search" action="/">
  <input class="form__search" name="s" />
  <input class="form__submit" type="submit" />
</form>
```

In this case, the `.search` class is a separate block that defines behavior. This block can’t have modifiers responsible for the form, themes, and sizes. These modifiers already belong to the universal form. A mix helps to combine the styles and behavior of these blocks.

Let’s take one more example where the component’s semantics is changed:

```html
<nav class="menu">
  <a class="link" href=""></a>
  <a class="link" href=""></a>
</nav>
```

The link functionality is already implemented in the `link` block, but the menu links have to differ visually from the links in the text.

Use a mix of the `link` universal block and the `item` element of the `menu` block:

```html
<nav class="menu">
  <a class="link menu__item" href=""></a>
  <a class="link menu__item" href=""></a>
</nav>
```

With the mix of the two BEM entities, you can now implement the basic link functionality from the `link` block and additional CSS rules from the `menu` block, and avoid code duplication.

#### External Geometry And Positioning: Giving Up Abstract HTML Wrappers

Mixes are used to position a block relative to other blocks or to position elements inside a block. In BEM, styles responsible for geometry and positioning are set in the parent block. Let’s take a universal menu block that has to be placed in the header. In the layout, the block has to have a 20px indent from the parent block.

This task has several solutions:

Write styles with indents for the menu block:

```css
.menu {
  margin-left: 20px;
}
```

In this case, the "menu" block isn’t universal anymore. If you have to place the menu in the page footer, you will have to edit styles because the indents will probably be different.

OR

Create the menu block modifier:

```html
<div>
  <ul class="menu menu_type_header">
    <li class="menu__item"><a href=""></a></li>
    <li class="menu__item"><a href=""></a></li>
  </ul>
</div>
```

In this case, the project will include two kinds of menus, although this is not the case. The menu stays the same.

OR

Use a mix. The information about nested block positioning is included in the parent block elements. Then the parent block element is mixed into the nested block. In this case, the nested block doesn’t specify any indents and can be easily reused in any place.

```html
<div>
  <ul class="menu header__menu">
    <li class="menu__item"><a href=""></a></li>
    <li class="menu__item"><a href=""></a></li>
    <li class="menu__item"><a href=""></a></li>
  </ul>
</div>
```

In this case, external geometry and positioning of the menu block are set through the `header__menu` element. The `menu` block doesn’t specify any indents and can be easily reused.

The parent block element (`header__menu`) performs the task of the wrapper blocks responsible for external positioning of the block.

### Blocks in the file structure

All BEM projects have a similar file structure. The familiar file structure makes it easier for developers to navigate the project, switch between projects, and move blocks from one project to another.

The implementation of each block is stored in a separate project folder. Each technology (CSS, JavaScript, tests, templates, documentation, images) is in a separate file.

For example, if the `input` block appearance is set with CSS, the code is saved in the `input.css` file.

```
project
  common.blocks/
    input/
      input.css # The "input" block implementation with CSS
      input.js  # The "input" block implementation with JavaScript
      input__clear.css    # The "input__clear" element implementation with CSS
      input_theme_sun.css # The "input_theme_sun" modifier implementation
```

The code for modifiers and elements is also stored in separate files of the block. This approach allows you to include in the build only those modifiers and elements that are necessary for the implementation of the block.

Using blocks and storing all block technologies in the same folder makes it easy to move blocks between projects. To move all styles and behavior of the block together with the layout, just copy the block folder to the new project.

---

## Non-Evident Advantages Of The Methodology

### Parallel Development

In BEM, any layout is divided into blocks. Because the blocks are independent, they can be developed in parallel by several developers.
A developer creates a block as a universal component that can be reused in any other project.

An example is the bem-components block library, which contains universal blocks, such as a link, button, and input field. It is easier to create more complex blocks from universal components.
Using blocks in project layout helps you save the time on integrating code written by several developers, guarantees the uniqueness of component names, and lets you test blocks at the development stage.

### Testing

It is problematic to test the functionality of the whole page, especially in a dynamic project connected to a database.

In BEM, each block is covered by tests. Tests are a block implementation technology, like Javascript or CSS. Blocks are tested at the development stage. It is easier to check the correctness of one block and then assemble the project from tested blocks. After that, all you have to do is to make sure that the block wrapper is working correctly.

### Customizable Build

All blocks and technologies in a BEM project are placed in separate folders and files. To combine the source files into a single file (for example, to put all CSS files in project.css, all JS files in project.js, and so on), we use the build process.

The build performs the following tasks: Combines source files that are spread out across the project’s file system; Includes only necessary blocks, elements, and modifiers (BEM entities) in the project; Follows the order for including entities; Processes the source file code during the build (e.g. compiles LESS code to CSS code).

Since BEM blocks are developed independently and placed in separate files in the file system, they don’t ‘know’ anything about each other. To build blocks based on other blocks, specify dependencies. There is a BEM technology responsible for this: the `deps.js` files. Dependency files let the build engine know which additional blocks have to be included in the project.
