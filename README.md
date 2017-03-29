## Atomic.css


1. Get it: `npm i atomic.css --save`
2. Import it: `import 'atomic.css'`


## Background

__Prior Art__
[Tachyons](tachyons.io), [Basscss](basscss.com), and other like-minded *CSS systems* have led the way in creating a new approach to doing CSS, where selectors are shallow, immutable, and atomic. In this sense, when reading a list of classes on an element, WYSIWYG. This approach spares teams from the dreadful monolistic `main.css`.

__Why bother?__
Writing your own version of an atomic css stylesheet is tedious. `Atomic.css` uses a combination of *scales* and *SASS functions* to alleviate this tedium.

__How do you even do that?__
`SASS maps`, `@each`, `@if`, and `@mixin/@include`. Black magic can be found at `@_utilities.scss`.

E.g.: hey, create a series of margin selectors derived from a golden-ratio scale.

Here's your scale:
```scss
$scale: (
    'ma0': 1rem,
    'ma1': 1.618rem,
    'ma2': 2.618rem,
);
```


Here's your mapper:
```scss
@each $selector, $property-value in $scale {
  .#{$selector} {
    margin: $property-value;
  }
}
```

Here's your output:
```css
.ma0 { margin: 1rem; }
.ma1 { margin: 1.618rem; }
.ma2 { margin: 2.618rem; }
```

## Selectors & Properties


#### Derivative Properties
*These are derived from `SASS maps` in `_variables.scss` and module files*

Given that these account for the majority of the `LOC` in `atomic.css`, refer to the `_variables.scss` and the files in the `/modules` directory.

__Example__: where `n` is the step and `i` is the associated value in the scale.
```
  .wx { width: i rem; }
  .wx-ns { @media #{$vars-from-map} { width: i rem; } }
```

__Scales used__
- `margin` & `padding`: steps (`n`) from `-5` to `5`: perfect fourth `1 / (1.25 ^ n)` > 0 > Golden ratio `1.618 ^ n`
- `width`, `height`, & `max-width`: 9 steps `[0, 9]`: `2 ^ n`
- `font-size`: `[-1, 5]`: approximately adjusted perfect fourth from `1 + 1.25 * n`

#### Static Properties
*These are not dependent on scales or media queries, and are therefore implemented as is.*

__Positions__
```
  'relative': (position: relative),
  'absolute': (position: absolute),
  'fixed': (position: fixed),
```

__Borders__
```
  'br0': (border-radius: 0),
  'br1': (border-radius: 0.125rem),
  'br2': (border-radius: 0.25rem),
  'br3': (border-radius: 0.5rem),
  'br4': (border-radius: 1rem),
  'br-100': (border-radius: 100%),
  'br-pill': (border-radius: 9999px),
  'br--bottom': (border-top-left-radius: 0, border-top-right-radius: 0),
  'br--top': (border-bottom-left-radius: 0, border-bottom-right-radius: 0),
  'br--right': (border-top-left-radius: 0, border-bottom-left-radius: 0),
  'br--left': (border-top-right-radius: 0, border-bottom-right-radius: 0),
  'ba': (border-style: solid, border-width: 1px),
  'bt': (border-top-style: solid, border-top-width: 1px),
  'br': (border-right-style: solid, border-right-width: 1px),
  'bb': (border-bottom-style: solid, border-bottom-width: 1px),
  'bl': (border-left-style: solid, border-left-width: 1px),
  'bn': (border-style: none, border-width: 0),
  'bw0': (border-width: 0),
  'bw1': (border-width: 0.125rem),
  'bw2': (border-width: 0.5rem),
  'bw3': (border-width: 1rem),
  'bt-0': (border-top-width: 0),
  'br-0': (border-right-width: 0),
  'bb-0': (border-bottom-width: 0),
  'bl-0': (border-left-width: 0),
```

__Box Shadows__
```
  'shadow-1': (box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.5)),
  'shadow-2': (box-shadow: 0 0 4px 2px rgba(0, 0, 0, 0.2)),
  'shadow-3': (box-shadow: 2px 2px 4px 2px rgba(0, 0, 0, 0.2)),
  'shadow-4': (box-shadow: 2px 2px 8px 0 rgba(0, 0, 0, 0.2)),
  'shadow-5': (box-shadow: 4px 4px 8px 0 rgba(0, 0, 0, 0.2)),
```

__Text__
```
  // font-style, transforms, variants, shadows
  'ttc': (text-transform: capitalize),
  'ttl': (text-transform: lowercase),
  'ttu': (text-transform: uppercase),
  'ttn': (text-transform: none),
  'strike': (text-decoration: line-through),
  'underline': (text-decoration: underline),
  'no-underline': (text-decoration: none),
  'i': (font-style: italic),
  'fs-normal': (font-style: normal),
  'small-caps': (font-variant: small-caps),
  'text-shadow-1': (text-shadow: 0 1px 4px rgba(0, 0, 0, 0.5)),
  'text-shadow-2': (text-shadow: 0 2px 4px rgba(0, 0, 0, 0.7)),
  // font-weight
  'normal': (font-weight: normal),
  'b': (font-weight: bold),
  'fw3': (font-weight: 300),
  'fw4': (font-weight: 400),
  'fw5': (font-weight: 500),
  'fw7': (font-weight: 700),
  'fw9': (font-weight: 900),
  // letter-spacing
  'tracked': (letter-spacing: 0.1em),
  'tracked-tight': (letter-spacing: -0.05em),
  'tracked-mega': (letter-spacing: 0.25em),
  // line-height
  'lh-solid': (line-height: 1),
  'lh-title': (line-height: 1.25),
  'lh-copy': (line-height: 1.5),
```

__Opacities__
```
  // opacities
  'o-100': (opacity: 1),
  'o-90': (opacity: 0.9),
  'o-80': (opacity: 0.8),
  'o-70': (opacity: 0.7),
  'o-60': (opacity: 0.6),
  'o-50': (opacity: 0.5),
  'o-40': (opacity: 0.4),
  'o-30': (opacity: 0.3),
  'o-20': (opacity: 0.2),
  'o-10': (opacity: 0.1),
  'o-05': (opacity: 0.05),
  'o-025': (opacity: 0.025),
  'o-0': (opacity: 0),
```

__Others__
```
  // overflows
  'overflow-visible': (overflow: visible),
  'overflow-hidden': (overflow: hidden),
  'overflow-scroll': (overflow: scroll),
  'overflow-auto': (overflow: auto),
  // z-index
  'z-0': (z-index: 0),
  'z-1': (z-index: 1),
  'z-2': (z-index: 2),
  'z-3': (z-index: 3),
  'z-max': (z-index: 2147483647),
  'z-inherit': (z-index: inherit),
  'z-initial': (z-index: initial),
  'z-unset': (z-index: unset),
  // utilities
  'center': (margin-right: auto, margin-left: auto),
  'list': (list-style-type: none),
  'pointer': (cursor: pointer),
  'pointer:hover': (cursor: pointer),
  'flex-center': (display: flex, justify-content: center, align-items: center)
```
