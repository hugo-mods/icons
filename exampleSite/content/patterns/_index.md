---
title: "Patterns"
date: 2021-05-22T16:32:06+02:00
draft: false
---

Hey there! 

This page shows different patterns.

From content files, you use the [shortcode pattern](https://github.com/hugo-mods/icons#shortcode-pattern)!

This pattern will use the `defaultLoaderShortcode` which is "svg-inline" for shortcodes by default:

> I {{< icon "fas guitar" >}} [hugo-mods](https://git.io/hugo-mods)!

If you check the HTML source, you'll see that the icon is not referenced. Instead, the SVG is written out completely in the above line.

Nevertheless, you can also reference icons that you're sure already exist on the page by changing the loader:

> I {{< icon "love" "svg-use" >}} [hugo-mods](https://git.io/hugo-mods)!

Again in the HTML source, note how the icon will be referenced via `<svg class="icon"><use xlink:href="#icon-love"/></svg>`