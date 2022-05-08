<a href="https://git.io/🪅"><img alt="Logo" align="right" width="200" src="https://raw.githubusercontent.com/hugo-mods/icons/main/.github/logo.png"></a>

# hugo-mods: icons
## A Hugo Icon Module that scales.

- [SVG symbol icon system](https://css-tricks.com/svg-symbol-good-choice-icons/): High performance with great browser support 
- Currently [supports Font Awesome](#icons), but aims to be icon-family agnostic in future 
- User-friendly API with support for [various usage patterns](#usage), including custom icon name support
- [Carefully implemented](https://kdevo.medium.com/-7c0acb90eeec#341e) and structured [partials](./layouts/partials)
- Smart and comfortable [icon search function](https://kdevo.medium.com/-7c0acb90eeec#341e) 
- Auto-enabled [accessibility](https://css-tricks.com/svg-symbol-good-choice-icons/#why-symbol-is-better-for-icons) by considering icon’s metadata

## Go get it

Initialize [Hugo's mod system](https://gohugo.io/hugo-modules/) on your site:

`hugo mod init github.com/<username>/<your-repo>`

Add module to site's config (e.g. `config.yaml`):

```yaml
module:
  imports:
  - path: github.com/hugo-mods/icons
```

Get the module (also upgrades existing one):

`hugo mod get -u`

This might take some time, as it will fetch all potentially usable icons.

## Icons

| Icon Family                        | Identifier Prefix        |
|:-----------------------------------|:------------------------:|
| [Font Awesome Solid][fas]          | `fas`                    |
| [Font Awesome Regular][far]        | `far`                    |
| [Font Awesome Brands][fab]         | `fab`                    |

Please also have a look at the [recommended CSS](assets/mod-icons/style.css) for styling.

## Usage 

hugo-mod-icons can be used in various ways that depend on your preferences and context.

To master this mod, it is advisable to read through every pattern and then decide which one works best for you.

### Context Pass Pattern

This pattern is especially useful for smaller sites/prototypes where you can easily pass around the page's context.

Reference icons with:

```html
<body>
    <!-- [...] -->
    <h1>I {{ partial "icon" (dict "context" . "name" "fas heart") }} hugo-mod-icons!</h1>
    <!-- [...] -->
</body>
```

Finally, place the actual data (non-visible) at the very end of the body:

```html
<body>
    <!-- [...] -->
    {{ partial "icon-data" . }}
</body>
```

It's important that the context is the same as the one passed to the first `partial "icon"`, 
which is sometimes a bit tricky, hence the next pattern has been invented.

> :bulb: The module will automatically keep track of all your referenced icons and only add the ones that are actually needed ONCE. No matter how many times you reference one and the same icon.

### Data Pattern

This pattern is more advanced and especially suitable for larger sites or themes. It requires maintaining all the icons you want to use in a separate `icons.yaml` file in the data folder, e.g.:

```yaml
fas heart:
```

You can omit the part after `:` if you just want to add the icon without renaming it,
but if you'd like to use `heart` instead of `fas heart`, you can do the following:

```yaml
heart: fas heart
```

The bonus you get is that you can easily exchange `fas heart` with another :heart:-like icon at a later time!
Next, you reference the icon like:

```html
<body>
    <!-- [...] -->
    <h1>I {{ partial "icon" "heart" }} icons!</h1>
    <!-- [...] -->
</body>
```

Finally, place the actual data (non-visible) at the very end of the body just as in the first pattern:

```html
<body>
    <!-- [...] -->
    {{ partial "icon-data" . }}
</body>
```

> :bulb: What makes this pattern awesome is that it scales well and that it does not need context for referencing icons. The only downside is that you need to additionally maintain the data file.


### Shortcode Pattern

You can also use this mod from within your content files with the `icon` shortcode:

```markdown
---
title: "My post"
---

Lorem ipsum and so on...

> tldr: `hugo-mods` rock {{< icon "guitar" >}}
```

### Advanced

To be continued. Documentation about mixing patterns and icon loaders will follow here.
Please also check out the [exampleSite](./exampleSite) which you can examine and e.g.
launch via `hugo serve exampleSite`.

[fab]: https://github.com/FortAwesome/Font-Awesome/tree/5.15.3/svgs/brands
[fas]: https://github.com/FortAwesome/Font-Awesome/tree/5.15.3/svgs/solid
[far]: https://github.com/FortAwesome/Font-Awesome/tree/5.15.3/svgs/regular
