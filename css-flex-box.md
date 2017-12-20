# CSS Flexbox Basics

CSS offers many ways for defining the overall appearance of a web page.

Flexbox gives us complete control over the alignment, direction, order, and size of our boxes.

Flexbox is easy to learn.

If you want to dive in, I recommend [Flexbox Zombies](https://geddski.teachable.com/p/flexbox-zombies).  
The course is free and a lot of fun.

```css
display: flex; /* start flexbox */

/* direction of the flexbox */
/* left to right? top to bottom? */
flex-direction: row;             /* direction from left to right */
flex-direction: row-reverse;     /*  direction from right to left */
flex-direction: column;          /*  direction from top to bottom */
flex-direction: column-reverse;  /*  direction from bottom to top */

/* position of the items */
/* at the start? at the end? */
justify-content: flex-start;     /* start of the line */
justify-content: flex-end;       /* end of the line */
justify-content: center;         /* center of the line */
justify-content: space-between;  /* separate blocks evenly */
justify-content: space-around;   /* separate blocks evenly AND space before the first and after the last block */

/* alignment of the items */
/* all aligned to the top? to the bottom? */
align-items: flex-start;  /*  aligned to top when left-right/right-left, aligned to left when top-bottom/bottom-top */
align-items: flex-end;    /*  aligned to bottom when l-r/r-l, aligned to right when t-b/b-t */
align-items: stretch;     /*  stretched to whole area */
align-items: center;      /*  centered to whole area */

```
