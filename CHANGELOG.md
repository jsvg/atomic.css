### 0.2.3

__Additions__
- ff1, ff2
- thematic colors
- border radii classes

```
'ff1': (font-family: 'system, -apple-system, BlinkMacSystemFont, "Helvetica Neue", "Lucida Grande", sans-serif'),
'ff2': (font-family: '"Roboto", sans-serif'),

'brtl0': (border-top-left-radius: 0),
'brtr0': (border-top-right-radius: 0),
'brbl0': (border-bottom-left-radius: 0),
'brbr0': (border-bottom-right-radius: 0),
```


### 0.2.2

- Patch `generateFromStaticPropertyMap` reference to `$static-map`

### 0.2.1

- Update `atomic.min.css` build

### 0.2.0

__Additions__
- Change white and black color selectors for [0, 3] to while0, white1, etc

### 0.1.0

__Additions__
- bw1, bw2, bw3

__Removals__
- vertical-alignments
- bw4 bw5
- br5
- fw1, fw2, fw6, fw8
- h-25, h-75, h-v25, h-v50
- media-queries on heights, and max-widths

__Other changes__
*these do not affect the atomic.css output*
- Allow `generateFromStaticPropertyMap` to output media-queries
- Refactor flex module into map
- Move hardcoded file (`_hover.scss`) into its own directory (`/hardcoded`)
