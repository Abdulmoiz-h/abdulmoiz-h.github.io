# Homework 2 Reflection

## 1. flex-direction: row vs. flex-direction: column

`flex-direction` sets the main axis of a flex container. With `row`, which is the default, the
items go side by side from left to right. With `column`, they stack on top of each other from top
to bottom.

Changing the direction also changes what `justify-content` and `align-items` do. In a row,
`justify-content` spaces items horizontally and `align-items` lines them up vertically. In a
column it's the other way around.

I used both in my navbar. On desktop the links are in a row next to each other. In my 768px media
query I changed `.nav-links` to `flex-direction: column` so the links stack on mobile, without
changing any of the HTML.

## 2. Why use relative units instead of px?

Pixels are a fixed size, so something like `width: 1100px` looks fine on a laptop but makes a
phone scroll sideways. Percentages, `fr`, `vw` and `vh` are based on the size of the screen or the
parent element, so the layout shrinks and grows with the device. For example, my grid columns are
`1fr` each, so they always split the space that's available.

`rem` is based on the root font size, so if someone makes their browser text bigger, everything
sized in `rem` gets bigger too. It also made the mobile layout easier: I changed the root font
size once in the media query instead of editing every font size by hand.

I still used px for small things like 1px borders, where it doesn't matter.

## AI Attribution

I used Claude (Anthropic) to help with this assignment. I gave it the homework instructions and
asked it to guid me in building the site.
