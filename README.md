* Traffic Lights #

[Demo](https://MERNCraft.github.io/traffic-lights)

Demo of a CSS-only activity for displaying the traffic light sequences for France and the UK.

The lights cycle through a sequence, thanks to changes made to the `z-index` value for the red light, with the help of the `:has()` pseudo-class.

Each light circle is contained in a `<label>` element which also holds a radio button and a `.trigger` span. The `.trigger` span for each circle is positioned absolutely to cover all three circles. A click on the `.trigger` makes the circle associated with it fully opaque, which simulates switching it on.

The radio button for the red light is initially checked. The green light is at the front, the amber light behind the green, and the red light at the back. When a radio button is checked, two things happen:

1. The associated light circle is set to `{ opacity: 1 }`
2. The associated `.trigger` span is set to `{ display: none }`. This ensures that the `.trigger` for the light behind it will be clicked next. 

When the checkbox for the amber light is checked, the `.trigger` for the green light is no longer hidden. In order to ensure that the next click is applied to the input for the red light, the `.trigger` for the red light is moved to the front when `#amber:checked` is true.

However, the `<label>` for the red light is defined in the HTML before the `<label>` for the amber light. It is not possible to use the `~` sibling combinator to refer to an older sibling. The solution is to use (pseudo-code follows)...

```css
parentElement:has(youngerSibling:checked) olderSibling
```

... to select the older sibling.

In the UK, before a red light turns green, both the red and the amber light is shown, to warn drivers to get ready to move forward. A similar (but more complicated technique) is used to bring a different `.ready` trigger forward when the input for the red light is checked _and_ the radio button for the UK switch is checked. When the `.ready` radio button is checked, the opacity of both the red and the amber circles is set to `1`. The `.trigger` for the `.ready` checkbox is set to `{ display: none }`, as for the other light circles, so now the green `.trigger` is ready to be clicked.