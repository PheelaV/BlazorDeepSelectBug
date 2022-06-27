# Bug description:
With reference to [child component support](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/css-isolation?view=aspnetcore-6.0#child-component-support)

```css
.listing::deep > div {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```
 
generates

```css
.listing::deep > div[b-o1x0imiw0b] {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```

which is the same as if the style was originally defined as
```css
.listing >  div {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```

## Expected Behaviour
Selector generated as:

`.listing[b-{STRING}] > div`

as per the example in the documentation:

> For example, `div::deep > a` is transformed to `div[b-{STRING}] > a` (for example, `div[b-3xxtam6d07] > a`).

## What works
This produces what I wanted to achieve
```css
.listing > ::deep div {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```
generates
```css
.listing[b-o1x0imiw0b] >  div {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```

and the same does 
```css
.listing ::deep > div {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
```
Two options come to my mind:
1) This is a bug.
2) This is a tiny documentation mistake?