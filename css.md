# Useful CSS snippets. Just in case

### Basic attributes
`width: auto` -- means container takes only amount of space according to content inside; For example, container width is equal to text width inside a block.
`width: 100%` -- means width of the parent container. Applicable for _block_ elements.

`1fr` vs `auto`: _1fr_ is greedy(equal), fraction of the space, so the purpose is to take equal amount of space among elements. _auto_ is shy(adaptive), so it usually takes only content's width.

`margin-inline` -- responsible for _left_ and _right_; `margin-block` -- for _top_ and _bottom_. The purpose is to follow direction convention...

### Flex stuff

* [How `flex` property works](https://ishadeed.com/article/css-flex-property/). In a nutshell, `flex-grow` specifies how much of _available_ space an item will take compare to other items. It's _not_ about equal space distribution between items.
* Default `flex` is `grow: 0, shring: 1, basis: auto`. So elements take only necessary space horizontally (don't span) and will decrease in size if container will be small.
* Default `align-items: stretch`, so it means the items height will be equal to the highest one. An additional value is `baseline`, it means adjust on the content bottom point.
* `grid-ish` or how to create _grid_ similar structure.
```css
.grid-ish {
   display: flex;
   flex-wrap: wrap;
}

.grid-ish > * {
   flex: 1; /* 1 1 auto; it means justify all elements inside a container equally */
}

.grid-ish > * {
   flex: 1 1 33%; /* if there are 5 items, then 3 of them will span on the first line, the last two will be spanned equally on the next line */
   /* flex: 0 1 33%; similar to the previous one, except two items won't be justified along the line */
}
```

`margin-right: auto` it's similar to `flex:1`, but it just *gives* space, not takes it.

### Grid

#### Template columns
   _auto-fit_ -- takes all available in a row, even if two elements are presented. That's will stretch these two elements to fit all empty space.

   _auto-fill_ -- keeps some empty space for potential elements that may be added. Might be suitable for shop items grid.
```css
.grid {
  border: 1px solid red;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  overflow-wrap: break-word; /* optional. Useful for long words */
}
```

#### Justify and Align
In Grid system there are several options:

* ***justify-items*** -- sets how to position each item (horizontally) inside a grid's cell (_start | end | center | space-between |..._).
* ***align-items*** -- sets how to position each item (vertically) inside a grid's cell (_start | end | center | space-between |..._).
* ***justify-content*** -- sets how to position (horizontally) the whole grid _(container's content)_ inside the container (only if the grid size is less than container's one).
* ***align-content*** -- sets how to position (vertically) the whole grid _(container's content)_ inside the container (only if the grid size is less than container's one).


#### Grid Auto

There are two types of grids: _explicit_ and _implicit_.

_Explicit_ applied when it's defined with `grid-template-*`. The settings will be applied to the items inside the area.

_Implicit_, on the other hand, applied when there are items that are not fit in explicit definition. For example, if you defined 2 columns and 2 rows, but there are 5 items. So the structure fits 4 elements only. Therefore, the 5th one will be in the _implicit_ grid, and `grid-auto-*` property will configure such items.

It's also possible to specify how those additional items will be added. By default, it's added like _rows_, but using `grid-auto-flow: column` it will be positioned like additional columns.

Materials:
* [Justify-* and Align-* in Grid](https://www.digitalocean.com/community/tutorials/css-align-justify)
