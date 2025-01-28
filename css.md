# Useful CSS snippets. Just in case

### Basic attributes
`width: auto` -- means container takes only amount of space according to content inside; For example, container width is equal to text width inside a block.
`width: 100%` -- means width of the parent container. Applicable for _block_ elements.

`1fr` vs `auto`: _1fr_ is greedy(equal), fraction of the space, so the purpose is to take equal amount of space among elements. _auto_ is shy(adaptive), so it usually takes only content's width.

`margin-inline` -- responsible for _left_ and _right_; `margin-block` -- for _top_ and _bottom_. The purpose is to follow direction convention...

### Grid template columns
   _auto-fit_ -- takes all available in a row, even if two elements are presented. That's will stretch these two elements to fit all empty space.
   _auto-fill_ -- keeps some empty space for potential elements that may be added. Might be suitable for shop items grid.
```css
.grid {
  border: 1px solid red;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  overflow-wrap: break-word; /* optional. Useful for long words */
}
