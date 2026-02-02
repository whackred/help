# EyeExp

The architecture for icons and logotypes is called EyeExp.

The `whack.eyexp.*` package contains an `EyeExp` singleton-like instance which is accessed like a `Map` for getting, setting and deleting icons or logotypes. Setting an entry causes Whack to re-render dependent `eyexp()` functions in CSS. An entry consists of an URL and a monochrome boolean.

Monochrome resources are displayed filled with the CSS (?inherited) `color` property. Non-monochrome resources may be displayed with a very discrete shadow whose color is the CSS (?inherited) `color`, but that is an explicit `shadow` attribute that only works on `<w:EyeExp/>` components and not things like CSS `background: eyexp(...);`.

- The `<w:EyeExp/>`'s `shadow` attribute only takes effect on non-monochrome resources.
- The `<w:EyeExp/>` accepts `size` (square), `width` and `height`. The two latter are often most used for logotypes.

The convention is for `EyeExp` entries to have a name based on enum names, such as `light_spark`. `enum` types are not actually used as icons and logotypes have a very dynamic nature.

Some examples:

```
import whack.eyexp.EyeExp;


// EyeExp : EyeExpSingleton


EyeExp.flower = { url: Embed("flower.svg"), monochrome: true };


// e4x

(
    <w:EyeExp name="flower" size={37}/>

    <!-- as a css background -->

    <div s:background="eyexp(flower) noRepeat center / contain"
         s:width={37]
         s:height={37}/>
)
```