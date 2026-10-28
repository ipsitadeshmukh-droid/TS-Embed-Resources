# ThoughtSpot Embedding Resources

A small collection of ready-to-use resources for anyone embedding ThoughtSpot with the [Visual Embed SDK](https://developers.thoughtspot.com/docs/). Grab what you need, drop it into your embed config, and customize from there.

## What's inside

```
.
├── iconSprite/      # SVG icon sprites for overriding ThoughtSpot's built-in icons
└── Style Guides/    # Sample style guide for theming embedded ThoughtSpot
```

---

## iconSprite

This folder contains SVG icon sprites you can use to replace ThoughtSpot's default icons (for example, the Spotter icon) in your embedded app.

### What is an icon sprite?

An icon sprite is an SVG file that holds one or more `<symbol>` elements inside `<defs>`. Each symbol's `id` matches the ID of the ThoughtSpot icon it replaces.

```xml
<svg xmlns="http://www.w3.org/2000/svg">
  <defs>
    <symbol id="rd-icon-spotter" viewBox="0 0 18 18">
      <!-- icon artwork -->
    </symbol>
  </defs>
</svg>
```

> **Tip:** A sprite file looks blank when opened in a browser, because symbols aren't rendered until they're referenced. If a folder includes `-preview` files, open those to see what the icon looks like.

### How to use

1. Host the sprite file at a public URL. If this repo is public on GitHub, jsDelivr works well:
   `https://cdn.jsdelivr.net/gh/<org>/<repo>@main/iconSprite/<file>.svg`
2. Add the sprite's domain to your ThoughtSpot CSP allowlist (**Develop → Security Settings**).
3. Reference it in your embed config:

```js
import { init, AuthType } from "@thoughtspot/visual-embed-sdk";

init({
  thoughtSpotHost: "https://your-instance.thoughtspot.cloud",
  authType: AuthType.None,
  customizations: {
    iconSpriteUrl: "https://cdn.jsdelivr.net/gh/<org>/<repo>@main/iconSprite/<file>.svg",
  },
});
```

### Making your own

Copy an existing sprite, replace the artwork inside the `<symbol>`, and keep the `id` the same as the icon you want to override. Keep the `viewBox` consistent with the original icon (usually `0 0 18 18`) so it sizes correctly.

---

## Style Guides

This folder contains a sample style guide showing how to theme embedded ThoughtSpot to match your brand: colors, fonts, and component styling.

### How to use

Use the style guide as a starting point, then apply your values through the SDK's `customizations.style` option:

```js
init({
  thoughtSpotHost: "https://your-instance.thoughtspot.cloud",
  authType: AuthType.None,
  customizations: {
    style: {
      customCSS: {
        variables: {
          "--ts-var-root-background": "#F7F9FC",
          "--ts-var-root-color": "#1E293B",
          "--ts-var-button--primary-background": "#2563EB",
        },
      },
    },
  },
});
```

See the [ThoughtSpot CSS variables reference](https://developers.thoughtspot.com/docs/css-variables-reference) for the full list of variables you can set.

---

## Useful links

- [Visual Embed SDK documentation](https://developers.thoughtspot.com/docs/)
- [Customize icons](https://developers.thoughtspot.com/docs/customize-icons)
- [Customize styles with CSS](https://developers.thoughtspot.com/docs/custom-css)
- [Security settings and CSP](https://developers.thoughtspot.com/docs/security-settings)

## Contributing

Have a useful sprite or style guide? Open a pull request. Please include a preview image or `-preview.svg` for any new icon, and a short note on what it's for.
