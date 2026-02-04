# EyeExp

The architecture for icons and logotypes is called EyeExp.

The `whack.eyexp.*` package contains an `EyeExp` singleton-like instance which is accessed like a `Map` for getting, setting and deleting icons or logotypes. Setting an entry causes Whack to re-render dependent `eyexp()` functions in CSS. An entry consists of an URL and a monochrome boolean.

Monochrome resources are displayed filled with the CSS (?inherited) `color` property. Non-monochrome resources may be displayed with a very discrete shadow whose color is the CSS (?inherited) `color`, but that is an explicit `shadow` attribute that only works on `<w:EyeExp/>` components and not things like CSS `background: eyexp(...);`.

- The `<w:EyeExp/>`'s `shadow` attribute only takes effect on non-monochrome resources.
- The `<w:EyeExp/>` accepts `size` (square), `width` and `height`. The two latter are often most used for logotypes.

The convention is for `EyeExp` entries to have a name based on enum names, such as `light_spark`. There is an optional but recommended namespace prefix syntax: `com.nothing.fw::light_spark`, which prevents collision between libraries. Setting an entry will automatically manage namespaces efficiently to avoid internally repeating the prefix string in-memory.

The CSS `eyexpPrefix` property allows setting an inheritable namespace prefix to implicitly use within EyeExp names.

Some examples:

```
import whack.eyexp.EyeExp;

// EyeExp : EyeExpSingleton

EyeExp["com.nothing.fw::flower"] = { url: Embed("flower.svg"), monochrome: true };

// e4x
<w:Group s:eyexpPrefix="com.nothing.fw">
    <w:EyeExp name="flower" size={37}/>
    <!-- as a css background. -->
    <w:Group s:background="eyexp(flower) noRepeat center / contain"
             s:width={37]
             s:height={37}/>
</w:Group>
```

