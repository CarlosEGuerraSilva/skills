---
name: heroui-v3-design-guide
description: "Design and review HeroUI v3 interfaces with @heroui/react and Tailwind CSS v4. Use for component selection, on-surface variants, forms, pickers, overlays, collections, theming, and compound component composition."
---

# HeroUI v3 design guide

## Read before implementation

Read [shared patterns](references/shared-patterns.md) and the relevant component reference. Check the on-surface table before choosing field variants. Each component entry repeats its own rule so it remains visible during focused lookups.

| Task | Reference |
| --- | --- |
| Shared recommendations and exact prop owners | [Shared patterns](references/shared-patterns.md) |
| Theme, colors, action hierarchy, styling, composition | [Principles](references/principles.md) |
| Inputs, selection controls, labels, validation | [Forms](references/components-forms.md) |
| Selection pickers, dates, colors, dialogs, notifications | [Pickers and overlays](references/components-pickers-overlays.md) |
| Buttons, collections, feedback, navigation, layout | [Content](references/components-content.md) |
| Conflicting documentation and version-sensitive details | [Gotchas](references/gotchas.md) |

## Implementation rules

Use `@heroui/react` compound components such as `Card.Header` and `Select.Trigger`. Named part exports also work. Import Tailwind CSS v4 before HeroUI styles:

```css
@import "tailwindcss";
@import "@heroui/styles";
```

HeroUI v3 does not require `HeroUIProvider` or Framer Motion for built-in animations. This does not prohibit `Toast.Provider`, locale or theme providers, or custom animation libraries. Do not copy v2 setup, flat component APIs, or variant names into v3 code. [Setup](https://heroui.com/en/docs/react/getting-started/quick-start).

Use `onPress` on pressable components, `isPending` on Button, and `isSelected` on toggles. Raw Input and TextArea use native `disabled`, `required`, and change events. Check the component's props rather than applying one naming convention everywhere.

Compose form fields with `Label`, `Description`, and `FieldError`. Supply an accessible name where visible text does not provide one. Preserve keyboard behavior and focus handling when replacing parts.

Choose variants per component. A primary action can remain primary inside Surface. The secondary-on-surface rule applies to the fields in the shared table, not every child component.

## Choose the component

| Need | Use |
| --- | --- |
| Static label / anchored count or dot / interactive tags | Chip / Badge / TagGroup |
| Triggered actions / inline options | Dropdown / ListBox |
| Selection without typing / editable filtering / search inside a selection popover | Select / ComboBox / Autocomplete |
| Typed date / date with calendar / date range | DateField / DatePicker / DateRangePicker |
| Critical confirmation / general dialog / edge panel | AlertDialog / Modal / Drawer |
| Anchored interactive content / hover or focus help | Popover / Tooltip |
| Transient notification / persistent in-page message | Toast / Alert |
| Unknown-duration activity / task progress / static quantity / content placeholder | Spinner / ProgressBar or ProgressCircle / Meter / Skeleton |
| One expandable section / coordinated sections / alternate views | Disclosure / Accordion or DisclosureGroup / Tabs |
| Structured content / background container | Card / Surface |

## Review before delivery

Check field variants against their actual background and prop owner. Then check names, errors, selection state, group inheritance, and part placement against the shared tables. Read the relevant gotcha when docs disagree; the installed package's types and implementation decide what code is valid.
