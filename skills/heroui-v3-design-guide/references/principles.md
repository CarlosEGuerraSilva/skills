# Principles, theming, and composition

## Choose intent before styling

For actions, use `primary` for the main action in a context, `secondary` for alternatives, `tertiary` for cancellation or dismissal, and `danger` for destructive actions. Use `ghost` or `outline` when their treatment fits the action hierarchy and the component supports them.

These meanings do not apply to every component. Field variants distinguish background treatments; Tabs uses `secondary` for an underline; ColorSwatchPicker uses `variant` for shape. See [variant families](shared-patterns.md#variant-and-status-families).

Use semantic variants and theme tokens before palette overrides. Start with the component's required parts; add indicators, descriptions, and custom styling when the interface needs them. React Aria supplies interaction behavior, but the application still needs correct names, content, and composition.

[Design principles](https://heroui.com/en/docs/react/getting-started/design-principles).

## Colors and themes

| Token family | Purpose |
| --- | --- |
| `--background`, `--foreground` | Page background and text |
| `--surface`, `--surface-secondary`, `--surface-tertiary` | Container backgrounds |
| `--accent`, `--accent-foreground` | Brand emphasis and text on it |
| `--default`, `--default-foreground` | Neutral controls |
| `--success`, `--warning`, `--danger` and their foregrounds | Status feedback |
| `--field`, `--field-*` | Field styling |
| `--separator`, `--focus` | Dividers and focus indicators |

Pair background and foreground utilities, such as `bg-accent text-accent-foreground`. Do not assume every token without a suffix is a background token. Use the [on-surface table](shared-patterns.md#on-surface-fields) for field treatment rather than changing raw colors.

Set `class="dark"` or `data-theme="dark"` on the theme root. Keep both synchronized when using both. HeroUI's `useTheme` handles stored preference, system preference, and root updates; framework-specific theme providers are also valid. Reserve `dark:` overrides for differences the semantic theme does not cover.

[Colors](https://heroui.com/en/docs/react/getting-started/colors) and [dark mode](https://heroui.com/en/docs/react/getting-started/dark-mode).

## Compose without losing behavior

Use compound parts and their required nesting. A `render` override must return one compatible root element and forward supplied props and the ref. Applying styles to another element does not give it React Aria behavior.

Variant functions from `@heroui/styles`, also re-exported by `@heroui/react`, style native elements and router links. When replacing the HeroUI component entirely, apply required child-slot classes too; the replacement does not create the component's context. Keep link navigation semantics. See [Link](components-pickers-overlays.md#link).

Extend existing variants with `tv({extend: buttonVariants, variants: {...}})`. For wrapper types, use `Button["RootProps"]`, named exports, or `ComponentProps`; use `Omit` to replace a prop. `Button.RootProps` is not a type namespace.

## Customize the relevant part

Use `className` for local changes, theme variables for shared values, and BEM selectors inside `@layer components` for global overrides. Target the part that owns the state. Pseudo-classes, data attributes, and render-prop states vary by component; do not assume every part exposes all of them.

Preserve focus indicators and reduced-motion behavior. Most sized controls support `sm`, `md`, and `lg`, but check each API. Avatar supports that scale; Spinner also supports `xl`, and ColorSwatch supports `xs` through `xl`.

Scrollbar utilities are `scrollbar`, `scrollbar-thin`, `scrollbar-default`, and `scrollbar-none`; `data-scrollbar` controls a subtree. Documentation icon sets are examples, not dependencies required by HeroUI.

[Composition](https://heroui.com/en/docs/react/getting-started/composition) and [styling](https://heroui.com/en/docs/react/getting-started/styling).
