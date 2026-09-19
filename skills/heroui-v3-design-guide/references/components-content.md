# Content, controls, and layout

## Button

Variants are `primary`, `secondary`, `tertiary`, `outline`, `ghost`, and `danger`; primary is the default. Sizes are `sm`, `md`, and `lg`, with md the default. Use `isIconOnly` with an accessible name for an icon-only button, and `isPending` for pending state. Optional ripple effects are composed as children.

A Surface parent does not change the action's importance. Do not downgrade a primary action merely to match a field's secondary variant. [Docs](https://heroui.com/en/docs/react/components/button).

## ButtonGroup

Set shared size, variant, and disabled state on the group. Only direct Buttons inherit them, not buttons inside nested dialogs or menus. An individual `isDisabled={false}` overrides the group.

Put ButtonGroup.Separator inside each Button except the first. The group handles joined corner radii and removes the buttons' pressed scale transform. Outline appears in official examples despite an API-table omission; see [gotchas](gotchas.md). [Docs](https://heroui.com/en/docs/react/components/button-group).

## ToggleButton and ToggleButtonGroup

ToggleButton variants are `default` and `ghost`, not primary/secondary. Use `isSelected`, `defaultSelected`, and `onChange(boolean)`.

ToggleButtonGroup defaults to single selection and supports multiple selection. Use `disallowEmptySelection` when one option must remain selected. Child ids must match selectedKeys. The group supplies size, not variant. Put its Separator inside each ToggleButton except the first.

[ToggleButton](https://heroui.com/en/docs/react/components/toggle-button), [ToggleButtonGroup](https://heroui.com/en/docs/react/components/toggle-button-group).

## CloseButton

The default child is a close icon and the only variant is `default`. Supply an accessible name. [Docs](https://heroui.com/en/docs/react/components/close-button).

## Slider

Compose Label, Output, and Track containing Fill and Thumb. Name the slider when omitting Label. Output displays values automatically. A scalar value is a single slider; an array is a range. For a range, use Track's render function to map `state.values` to Thumbs with matching `index` values.

Slider has no surface variant. [Docs](https://heroui.com/en/docs/react/components/slider). For boolean controls, see [Switch](components-forms.md#switch-and-switchgroup).

## Toolbar

Toolbar provides roving arrow-key navigation and can contain ButtonGroup. Give it an accessible name. `isAttached` adds a surface background and full rounding; it is optional, not a requirement imposed by a Surface parent. [Docs](https://heroui.com/en/docs/react/components/toolbar).

## Dropdown

Use Dropdown for triggered actions. Compose Trigger with Button, then Popover containing Menu and Items. Name Dropdown.Menu. Items support `default` and `danger` variants; use danger for destructive actions.

Rich items can contain Label, Description, `Kbd slot="keyboard"`, and ItemIndicator with checkmark or dot treatment. Supply `textValue` for typeahead when content is not plain text. SubmenuTrigger creates submenus. Sections use Header and Separator. Selection defaults to none and can be configured per section. [Docs](https://heroui.com/en/docs/react/components/dropdown).

## ListBox

Use ListBox for inline options. Give it an accessible name; selection defaults to single, unlike Dropdown. Items support default/danger variants and rich-content `textValue`. Sections and separators follow the collection pattern. For virtualization, use React Aria Virtualizer with ListLayout. [Docs](https://heroui.com/en/docs/react/components/list-box).

## TagGroup

Use TagGroup for selectable or removable tags. It owns Tag size and variant; individual Tags cannot override them. `variant="surface"` gives tags a surface background. This is not a blanket rule for every TagGroup nested in Surface.

Selection defaults to none. Give Tags textValue. `onRemove` supplies default remove buttons; use Tag.RemoveButton for custom removal content. Put `renderEmptyState` on TagGroup.List and use ErrorMessage for errors. [Docs](https://heroui.com/en/docs/react/components/tag-group).

## Badge and Chip

Badge attaches a count or status to another element. Wrap the target and Badge in Badge.Anchor; an empty Badge renders a dot. It supports primary, secondary, and soft variants, status colors, and corner placement. Do not use it as a standalone label.

Chip is a static label. Its variants are primary for filled treatment, secondary for the default bordered treatment, tertiary for transparent treatment, and soft. It has no outline variant. Use color for status, and TagGroup when interaction is required.

[Badge](https://heroui.com/en/docs/react/components/badge), [Chip](https://heroui.com/en/docs/react/components/chip).

## Table

Compose Table.ScrollContainer with Table.Content, then Header/Column and Body/Row/Cell. Name Table.Content. Footer belongs outside ScrollContainer, not in a native tfoot. The root class is `.table-root`.

Primary gives a card-like background; secondary is flat. This guide recommends `variant="secondary"` when embedding a table in a panel that already supplies the background. That applies the documented styles; it is not the field-specific on-surface rule.

Sorting uses column `allowsSorting`, Content's `sortDescriptor`/`onSortChange`, and a SortableColumnHeader receiving `sortDirection`. Selection uses Content's selectionMode and `Checkbox slot="selection"`. Expandable rows use treeColumn and `Button slot="chevron"`. Resizing uses ResizableContainer and ColumnResizer.

Use LoadMore/LoadMoreContent for incremental loading and Body's renderEmptyState for no rows. Virtualization uses TableLayout. TanStack Table can supply data logic while HeroUI renders the table. [Docs](https://heroui.com/en/docs/react/components/table).

## Spinner

Use Spinner for unknown-duration activity. Sizes include sm, md, lg, and xl. Colors are current, accent, success, warning, and danger; use `current`, not `default`, to inherit text color. Preserve reduced-motion behavior when changing animation speed. [Docs](https://heroui.com/en/docs/react/components/spinner).

## ProgressBar, ProgressCircle, and Meter

ProgressBar and ProgressCircle represent a task, with `isIndeterminate` when progress cannot be measured. Their default color is accent. ProgressCircle's SVG Track contains TrackCircle and FillCircle for stroke customization.

Meter represents a static quantity within a known range. It has no indeterminate state and defaults to percent formatting. [ProgressBar](https://heroui.com/en/docs/react/components/progress-bar), [ProgressCircle](https://heroui.com/en/docs/react/components/progress-circle), [Meter](https://heroui.com/en/docs/react/components/meter).

## Skeleton

Match placeholders to the loading content's shape. Animation choices are shimmer, pulse, and none; `--skeleton-animation` sets shared behavior. For one synchronized shimmer, put `.skeleton--shimmer` on the parent and `animationType="none"` on the child Skeletons. [Docs](https://heroui.com/en/docs/react/components/skeleton).

## Alert

Use Alert for an in-page message. The prop is `status`, with default, accent, success, warning, and danger values. Compose Indicator and Content containing Title and Description. Indicator supplies a status icon by default. [Docs](https://heroui.com/en/docs/react/components/alert).

## Typography

Use `type` for h1 through h6, body, body-sm, body-xs, or code. Other options include align, default/muted color, weight, and truncate. Parts are Heading with level, Paragraph with base/sm/xs size, Code, and Prose. [Docs](https://heroui.com/en/docs/react/components/typography).

## Kbd

Use Kbd for keyboard shortcuts, not generic labels. Variants are default and light. Compose Abbr and Content; give abbreviations a title such as Command. In Dropdown.Item, use `slot="keyboard"`. The API table's Key/keyValue terminology conflicts with the anatomy; check installed exports before using it. [Docs](https://heroui.com/en/docs/react/components/kbd).

## Avatar

Compose Image and Fallback. Fallback appears while loading or after an error; delayMs avoids a brief fallback flash. Keep `src` on Avatar.Image even with `asChild` and a custom image, so Avatar can track loading.

Sizes are sm, md, and lg. Variants are default and soft; color styles the fallback rather than the image. [Docs](https://heroui.com/en/docs/react/components/avatar).

## ScrollShadow

Use scroll-position fades for overflow content. Auto mode uses scroll-driven animation and creates a stacking context and a containing block for fixed descendants. Set visibility explicitly to opt out. Do not put competing `animate-*` utilities on the same element. [Docs](https://heroui.com/en/docs/react/components/scroll-shadow).

## Card

Compose Header with Title and Description, followed by Content and Footer. Title defaults to h3. Variants are transparent, default, secondary, and tertiary. The docs recommend transparent for nested cards.

Card is not a link. Use actual link semantics for navigation and cardVariants when styling an anchor. Name semantic regions where appropriate. Form controls on a Card background follow the [on-surface table](shared-patterns.md#on-surface-fields). [Docs](https://heroui.com/en/docs/react/components/card).

## Surface

Surface supplies a container background and exports context describing its variant. Variants are default, secondary, tertiary, and transparent. Context availability does not mean every child automatically adapts.

On a Surface background, explicitly set secondary on the field owners in the [complete table](shared-patterns.md#on-surface-fields). Do not apply that rule to every component with a variant prop. [Docs](https://heroui.com/en/docs/react/components/surface).

## Separator

Variants default, secondary, and tertiary select divider contrast. Choose a variant explicitly when the background requires it. The implementation does not read SurfaceContext to select a variant. [Docs](https://heroui.com/en/docs/react/components/separator), [implementation](https://github.com/heroui-inc/heroui/blob/v3/packages/react/src/components/separator/separator.tsx).

## Accordion

Compose Item with Heading containing Trigger and Indicator, then Panel containing Body. Multiple expansion is off by default; use allowsMultipleExpanded to enable it. Items can be controlled individually, and hideSeparator removes dividers.

Variants are default and surface. Surface adds a background to the accordion itself; it is not required solely because a parent is Surface. [Docs](https://heroui.com/en/docs/react/components/accordion), [styles](https://github.com/heroui-inc/heroui/blob/v3/packages/styles/components/accordion.css).

## Disclosure and DisclosureGroup

Use Disclosure for one expandable section. Use DisclosureGroup to coordinate several, with an id on each child. Keep Trigger and Content in the documented composition. Tabs are for switching views rather than expanding sections. [Disclosure](https://heroui.com/en/docs/react/components/disclosure), [DisclosureGroup](https://heroui.com/en/docs/react/components/disclosure-group).

## Tabs

Put List inside ListContainer and Tabs.Tab inside List. Put Tabs.Panel under the Tabs root, as a sibling of ListContainer, with an id matching its Tab. Give Tabs.List an accessible name.

ListContainer supplies overflow chevrons and fades. Put Tabs.Separator inside each Tab except the first. Primary uses a filled indicator; secondary uses an underline, not an on-surface field treatment. Use start alignment for vertical sidebars and aria-selected for selected-state styling. [Docs](https://heroui.com/en/docs/react/components/tabs).

## Breadcrumbs and Pagination

In Breadcrumbs, omit href on the final current-page item so it receives aria-current automatically.

Pagination renders navigation. Give it an accessible name and mark the current Link with isActive. Ellipsis is hidden from assistive technology. Use onPress for actions. Pagination supports sm/md/lg sizes, not variants. [Breadcrumbs](https://heroui.com/en/docs/react/components/breadcrumbs), [Pagination](https://heroui.com/en/docs/react/components/pagination).

For routing composition, see [Link](components-pickers-overlays.md#link).
