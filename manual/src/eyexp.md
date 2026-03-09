# EyeExp

The architecture for icons and logotypes is called EyeExp.

The `whack.eyexp.*` package contains an `EyeExp` singleton-like instance which is accessed like a `Map` for getting, setting and deleting icons or logotypes. Setting an entry causes Whack to re-render dependent `EyeExp` tags. An entry consists of an URL and a monochrome boolean.

Monochrome resources are displayed filled with the CSS (?inherited) `color` property. Non-monochrome resources may be displayed with a very discrete shadow whose color is the CSS (?inherited) `color`.

- The `<w:EyeExp/>`'s `shadow` attribute only takes effect on non-monochrome resources.
- The `<w:EyeExp/>` accepts `size` (square), `width` and `height`. The two latter are often most used for logotypes.

The convention is for `EyeExp` entries to have a name based on enum names, such as `light_spark`. There is an optional but recommended namespace prefix syntax: `zero::light_spark`, which prevents collision between libraries. Setting an entry will automatically manage namespaces efficiently to avoid internally repeating the prefix string in-memory.

The CSS `eyexpPrefix` property allows setting an inheritable namespace prefix to implicitly use within EyeExp names. It supports fallbacks as well.

Some examples:

```sx
import whack.eyexp.EyeExp;

// EyeExp : EyeExpSingleton

EyeExp["zero::flower"] = { url: Embed("flower.svg"), monochrome: true };

// E4X

final = (
    <div s:eyexpPrefix="'zero'">
        <w:EyeExp name="flower" size={37}/>
    </div>
)
```

The most common is for component libraries to provide an `Application` component that eliminates the general need for explicitly setting the implicit EyeExp prefix.

## Enumeration

Obtain all entries of an EyeExp namespace using:

```sx
EyeExp.entries("zero")
    /*
    Returns something like
    [
        ["flower", { url, monochrome, ... }]
    ]
    */
```