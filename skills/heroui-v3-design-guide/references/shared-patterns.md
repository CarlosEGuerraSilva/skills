# Shared recommendations

Component entries repeat their local rule and source. The container table separates documented styles from this guide's design applications.

## On-surface fields

Use `variant="secondary"` for these controls on Surface or Card backgrounds. Set variants explicitly. Check the rendered background, especially in nested or transparent containers; a Surface ancestor alone does not describe it.

[Surface guidance](https://heroui.com/en/docs/react/components/surface) and [explicit field variants](https://heroui.com/en/docs/react/releases/v3-0-0-beta-4).

| Component | Set `variant="secondary"` on |
| --- | --- |
| [Input](components-forms.md#input-and-textarea) | `Input` |
| [TextArea](components-forms.md#input-and-textarea) | `TextArea` |
| [TextField](components-forms.md#textfield) | Its child `Input`, `TextArea`, or `InputGroup` |
| [InputGroup](components-forms.md#inputgroup) | `InputGroup`, not its input parts |
| [Checkbox](components-forms.md#checkbox) | `Checkbox` |
| [CheckboxGroup](components-forms.md#checkboxgroup) | Each child `Checkbox`, not the group |
| [RadioGroup / Radio](components-forms.md#radiogroup-and-radio) | `RadioGroup` |
| [InputOTP](components-forms.md#inputotp) | `InputOTP` |
| [NumberField](components-forms.md#numberfield) | `NumberField`, not Group or Input |
| [SearchField](components-forms.md#searchfield) | `SearchField`, not Group or Input |
| [Select](components-pickers-overlays.md#select) | `Select` |
| [ComboBox](components-pickers-overlays.md#combobox) | `ComboBox` |
| [Autocomplete](components-pickers-overlays.md#autocomplete) | `Autocomplete` |
| [DateField](components-pickers-overlays.md#datefield) | `DateField.Group` |
| [DatePicker](components-pickers-overlays.md#datepicker) | The composed `DateField.Group` |
| [DateRangePicker](components-pickers-overlays.md#daterangepicker) | The composed `DateField.Group` |
| [TimeField](components-pickers-overlays.md#timefield) | `TimeField.Group` |
| [ColorField](components-pickers-overlays.md#colorfield) | `ColorField.Group` |
| [Fieldset / Form](components-forms.md#fieldset-and-form) | Child controls at the owners listed above |

For compound fields, set the variant once on the listed owner. Do not repeat it on every nested Input or Group. ColorPicker's composed ColorField follows the ColorField row; ColorPicker itself is not an additional secondary-variant field.

Switch and Slider have no corresponding variant. Buttons keep their action hierarchy. Do not infer a secondary variant for an unlisted component.

## Related container styles

| Component | Documented style | How to apply it |
| --- | --- | --- |
| [Card](components-content.md#card) | `transparent` removes its background | Docs recommend it for nested cards |
| [Table](components-content.md#table) | `secondary` is flat rather than card-like | Guide application: use it when the containing panel already provides the background |
| [Accordion](components-content.md#accordion) | `surface` gives the accordion a surface background | Optional treatment, not a requirement for every accordion inside Surface |
| [TagGroup](components-content.md#taggroup) | `surface` gives tags a surface background | Set on TagGroup; not a universal parent-Surface rule |
| [Separator](components-content.md#separator) | `default`, `secondary`, `tertiary` control contrast | Choose explicitly when needed; do not assume SurfaceContext changes it |
| [Toolbar](components-content.md#toolbar) | `isAttached` adds a surface background and rounding | Optional toolbar treatment, not required by a Surface ancestor |

## Labels and validation

| Pattern | Components and placement |
| --- | --- |
| Shared form content | Compose `Label`, `Description`, and `FieldError` inside the field |
| Errors outside form fields | Use `ErrorMessage` for TagGroup and Calendar |
| Description hides when invalid | TextField, NumberField, SearchField, DateField, TimeField, ColorField |
| Focus state covers the whole field | Use `isFocusWithin` in TextField, NumberField, SearchField render props |
| Standalone label or description | Wire `htmlFor`/`id` and `aria-describedby`; composed fields handle association |
| Name an otherwise unnamed control | Icon-only Button/CloseButton, Slider, Checkbox, color controls |
| Name the collection or region | `Table.Content`, `Tabs.List`, `Dropdown.Menu`, ListBox, Calendar, RangeCalendar, Toolbar; name Form when it should be a landmark |

Prefer a visible label or `aria-labelledby` where suitable. Use `aria-label` when there is no usable visible name. Do not replace a meaningful visible label with redundant ARIA text.

## Parent-owned props and part placement

| Pattern | Components |
| --- | --- |
| Group supplies shared props | ButtonGroup passes size, variant, disabled state to direct Buttons; ToggleButtonGroup supplies size; TagGroup owns Tag size and variant |
| Field owns shared styling | InputGroup, NumberField, SearchField own variants; CheckboxGroup delegates variants to Checkboxes; RadioGroup owns its variant |
| Shared color value | ColorPicker coordinates its color controls |
| Separator inside each item except the first | ButtonGroup.Separator in Button; ToggleButtonGroup.Separator in ToggleButton; Tabs.Separator in Tabs.Tab |
| Stable selection identifiers | ToggleButtonGroup child ids match selectedKeys; Tabs.Tab and Tabs.Panel ids match; DisclosureGroup children have ids |
| Text for rich collection items | Supply `textValue` for Dropdown/ListBox items with rich content and for Tags; customize Autocomplete.Value to avoid copying complex selected-item visuals |
| Segment render function | DateField.Input and TimeField.Input; DatePicker and DateRangePicker compose DateField.Input |
| Multiple independently indexed controls | Range Slider thumbs use `index`; InputOTP slots use zero-based `index`; date-range inputs use `slot="start"` and `slot="end"` |
| Dialog configuration belongs to parts | Modal, AlertDialog, Drawer use Backdrop for open/dismissal props and backdrop variant. Modal/AlertDialog sizes belong on Container; Drawer placement belongs on Content |

## Variant and status families

| Meaning | Components and prop |
| --- | --- |
| Action emphasis | Button and ButtonGroup `variant`; ToggleButton has its own `default`/`ghost` set |
| Field background | The primary/secondary owners in the on-surface table |
| Container background | Card, Surface, Table, Accordion, TagGroup `variant`; sets differ |
| Filled indicator or underline | Tabs `variant`, not a field-background switch |
| Swatch shape | ColorSwatchPicker `variant`; ColorSwatch instead uses `shape` |
| Feedback status | Alert and AlertDialog.Icon `status`; Toast `variant` |
| Status color | Badge, Chip, Avatar, Meter, ProgressBar, ProgressCircle, Spinner `color`; allowed colors differ |
| Pending state | Button `isPending`; Toast `isLoading`; ProgressBar/ProgressCircle `isIndeterminate` |

Use value callbacks on composed fields and toggles. Raw Input/TextArea use native change events and native boolean props. Field booleans commonly use `isDisabled`, `isRequired`, and `isInvalid`; do not rename native props or assume all components share one signature.
