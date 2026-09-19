# Pickers and overlays

## Select

Use Select for choosing from options without typing. Compose Trigger with Value, ClearButton, and Indicator, then a Popover containing ListBox. On Surface, set `variant="secondary"` on Select.

Use `Select.ClearButton` rather than a nested button inside the button trigger. It renders a pointer affordance; Backspace or Delete provides keyboard clearing. Both paths call `onClear`. [Docs](https://heroui.com/en/docs/react/components/select).

## ComboBox

Use ComboBox for editable filtering, with `allowsCustomValue` when arbitrary input is allowed. Compose its input and trigger in `ComboBox.InputGroup`. The menu opens on focus by default. `formValue` defaults to `"key"`; use `"text"` for text submission.

For multiple selection, set `selectionMode="multiple"` on both ComboBox and its ListBox. On Surface, set `variant="secondary"` on ComboBox. The root implementation declares this prop even though the API table omits it. [Docs](https://heroui.com/en/docs/react/components/combo-box), [implementation](https://github.com/heroui-inc/heroui/blob/v3/packages/react/src/components/combo-box/combo-box.tsx).

## Autocomplete

Use Autocomplete for a selection trigger with search inside its popover through `Autocomplete.Filter`. On Surface, set `variant="secondary"` on Autocomplete.

A bare Value can reproduce the selected items' full ListBox content. In multiple mode, use `selectedText` or `state.selectedItems` to control the summary. Item render functions reused by Value receive `isSelected: false`. [Docs](https://heroui.com/en/docs/react/components/autocomplete).

For asynchronous option lists, use the collection's supported empty-state and load-more parts. Keep an empty popup open with `allowsEmptyCollection` where supported. Client filtering can use `useFilter({sensitivity: "base"})`; check which component owns each prop rather than copying one picker's API to another.

## DateField

Use DateField for typed segmented dates. DateField.Input needs a segment render function:

```tsx
<DateField.Input>
  {(segment) => <DateField.Segment segment={segment} />}
</DateField.Input>
```

On Surface, set `variant="secondary"` on DateField.Group. Do not repeat it on every segment or input. Invalid state hides Description. [Docs](https://heroui.com/en/docs/react/components/date-field).

## DatePicker

Compose DateField.Group and its input, then DatePicker.Popover with Calendar. Put the trigger in DateField.Suffix; TriggerIndicator supplies a calendar icon by default.

On Surface, set `variant="secondary"` on the composed DateField.Group, not DatePicker. The DateField.Input still needs its segment render function. [Docs](https://heroui.com/en/docs/react/components/date-picker).

## DateRangePicker

Place two DateField.Input parts inside one DateField.InputContainer. Put `slot="start"` and `slot="end"` on the inputs, not the container, and render their segments. Separate them with DateRangePicker.RangeSeparator. Use RangeCalendar in the popover.

The value is `{start, end} | null`. Submit with `startName` and `endName`, not a single `name`. On Surface, set `variant="secondary"` on the composed DateField.Group. [Docs](https://heroui.com/en/docs/react/components/date-range-picker).

## TimeField

Render each input segment with TimeField.Segment. Granularity defaults to `"minute"`. On Surface, set `variant="secondary"` on TimeField.Group. Invalid state hides Description. DateField and TimeField share `.date-input-group` styling. [Docs](https://heroui.com/en/docs/react/components/time-field).

## Calendar and RangeCalendar

Give the grid an accessible name. Use date values and utilities from `@internationalized/date`. RangeCalendar supports `allowsNonContiguousRanges` and an anchor date for unavailable-date checks.

Display locale and value calendar are separate. `onChange` preserves the value's calendar system, Gregorian when no value establishes another one. Use I18nProvider to change the displayed locale or calendar. Date/time fields expose formatting options such as `granularity`, `hourCycle`, and `hideTimeZone`; use supported minimum, maximum, and unavailable-date constraints.

[Calendar](https://heroui.com/en/docs/react/components/calendar), [RangeCalendar](https://heroui.com/en/docs/react/components/range-calendar).

## ColorField

Use ColorField for precise text entry. `isWheelDisabled` prevents wheel changes. On Surface, set `variant="secondary"` on ColorField.Group, not ColorField. Invalid state hides Description. [Docs](https://heroui.com/en/docs/react/components/color-field).

## ColorPicker and color controls

ColorPicker shares one Color value among composed controls, without separate child state wiring. A composed ColorField on a surface still uses `ColorField.Group variant="secondary"`.

| Component | Use |
| --- | --- |
| [ColorArea](https://heroui.com/en/docs/react/components/color-area) | Two-dimensional selection with `xChannel` and `yChannel` |
| [ColorSlider](https://heroui.com/en/docs/react/components/color-slider) | One channel, such as hue, with the matching color space |
| [ColorSwatch](https://heroui.com/en/docs/react/components/color-swatch) | Static preview; `shape="circle"` or `"square"`, sizes `xs` through `xl` |
| [ColorSwatchPicker](https://heroui.com/en/docs/react/components/color-swatch-picker) | Palette selection; `variant="circle"` or `"square"` means shape, not emphasis |

Supply an accessible color name with `colorName` or the supported ARIA label. `parseColor` is re-exported by HeroUI. [ColorPicker](https://heroui.com/en/docs/react/components/color-picker).

## Dialogs, popovers, and tooltips

| Component | Use and defaults |
| --- | --- |
| [AlertDialog](https://heroui.com/en/docs/react/components/alert-dialog) | Critical confirmation. Backdrop dismissal and Escape dismissal are disabled by default; Icon status defaults to danger |
| [Modal](https://heroui.com/en/docs/react/components/modal) | General dialog. Dismissible by default; scrolling can be inside or outside |
| [Drawer](https://heroui.com/en/docs/react/components/drawer) | Edge panel, bottom by default. Dismissible like Modal; drag regions are handle, header, and footer; no size prop |
| [Popover](https://heroui.com/en/docs/react/components/popover) | Anchored interactive content. Default offset is 8; supports flipping and optional Dialog and Arrow parts |
| [Tooltip](https://heroui.com/en/docs/react/components/tooltip) | Noninteractive hover/focus help. Default delay is 700 ms; `showArrow` is a boolean, not an Arrow part |

Modal and AlertDialog compose Backdrop, Container, then Dialog. Drawer uses Content instead of Container; set placement on Drawer.Content. Within Dialog, compose Header, Body, Footer, and an optional CloseTrigger. Put open/dismissal props and backdrop variant on Backdrop. Backdrop variants are opaque, blur, and transparent. Modal.Container and AlertDialog.Container accept xs, sm, md, lg, and cover sizes; Modal also accepts full.

Use controlled `isOpen`/`onOpenChange` or `useOverlayState`, which exposes `isOpen`, `open`, `close`, `toggle`, and `setOpen`. Modal.Dialog and AlertDialog.Dialog render functions expose `close`. Preserve the overlay's focus and dismissal behavior; do not assume every Popover is non-modal merely because it is anchored.

## Toast

Mount Toast.Provider once in the client application. Toasts render through a client portal. Use `toast(message)`, status helpers, or `toast.promise` with loading, success, and error content. Update or dismiss with `toast.update`, `toast.close`, and `toast.clear`; global timers have `pauseAll` and `resumeAll`.

Options include description, indicator, actionProps, `isLoading`, and timeout. Timeout defaults to 4000 ms; zero persists. Updates inherit omitted options, so provide a timeout when changing a persistent toast to a timed one. Variants are `default`, `accent`, `success`, `warning`, and `danger`.

Provider defaults are bottom placement, three visible toasts, and Alt+T access. An empty hotkey array disables that shortcut. F6 navigation is supported; timers pause on hover, focus, and background tabs. [Docs](https://heroui.com/en/docs/react/components/toast).

## Link

Keep router navigation in the router's link component. Compose through HeroUI Link's `render` prop, or apply `linkVariants`/BEM classes to the router link. A replacement without HeroUI context needs explicit icon-slot styling. Set underline treatment with CSS utilities, not old underline props. Use `onPress` for press handling. [Docs](https://heroui.com/en/docs/react/components/link).
