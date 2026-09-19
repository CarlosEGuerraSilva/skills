# Forms and fields

## Validation

Compose `Label`, `Description`, and `FieldError` inside the field. Use `isInvalid` with an error message, and `validate` for custom validation where supported. `validationBehavior="native"` blocks invalid submission; `"aria"` reports validation without native submission blocking. It does not, by itself, define when your application validates.

Pass server errors to Form as `validationErrors` keyed by field name. A field's validation result may contain a `validationErrors` array; that is not the same API. See the [shared validation summary](shared-patterns.md#labels-and-validation).

## TextField

Compose `Label`, `Input` or `TextArea`, `Description`, and `FieldError` under TextField. Use it when an input needs field-level labeling or validation. `onChange` receives a string. Use `isFocusWithin` rather than the deprecated `isFocused` render prop. An invalid TextField hides Description.

On Surface, set `variant="secondary"` on the child Input, TextArea, or InputGroup, not TextField. [Docs](https://heroui.com/en/docs/react/components/text-field).

## Input and TextArea

These render native input elements. Use native `disabled`, `required`, and change events; put field-level validation on TextField. TextArea handles multiline content and defaults to three rows.

Both default to `variant="primary"`. On Surface, set `variant="secondary"` directly on Input or TextArea. [Input](https://heroui.com/en/docs/react/components/input), [TextArea](https://heroui.com/en/docs/react/components/text-area).

## InputGroup

Inside TextField, compose `InputGroup.Prefix`, `InputGroup.Input` or `InputGroup.TextArea`, and `InputGroup.Suffix`. Keep Label, Description, and FieldError outside the group, under TextField. The group inherits field state. TextArea composition top-aligns the prefix and suffix.

Give icon-only suffix actions accessible names. On Surface, set `variant="secondary"` on InputGroup only; its input parts use the group's styles. [Docs](https://heroui.com/en/docs/react/components/input-group), [implementation](https://github.com/heroui-inc/heroui/blob/v3/packages/react/src/components/input-group/input-group.tsx).

## InputOTP

Set required `maxLength` and a zero-based `index` on each `InputOTP.Slot`. Use `pattern` to restrict characters; exported patterns include `REGEXP_ONLY_DIGITS`. `onComplete(value)` runs when the input is filled.

On Surface, set `variant="secondary"` on InputOTP. [Docs](https://heroui.com/en/docs/react/components/input-otp).

## Checkbox

Put `Checkbox.Control` and label text inside `Checkbox.Content`, the clickable label. Put `Checkbox.Indicator` inside Control. Description and FieldError are siblings of Content. Without visible label text, name Checkbox with ARIA.

Set `isIndeterminate` on the root. Root render props describe field state; Control and Indicator expose interaction state. On Surface, set `variant="secondary"` on Checkbox. [Docs](https://heroui.com/en/docs/react/components/checkbox).

## CheckboxGroup

Compose Label, Description, Checkboxes, and FieldError. The group value is a string array; each Checkbox needs a value.

On Surface, set `variant="secondary"` on every child Checkbox. CheckboxGroup has no variant. [Docs](https://heroui.com/en/docs/react/components/checkbox-group).

## RadioGroup and Radio

Compose Label, Description, Radios, and FieldError under RadioGroup. Within each Radio, put Control and label text in `Radio.Content`, with Indicator inside Control. Keep per-radio Description outside Content. The default orientation is vertical; customize the indicator through its children.

On Surface, set `variant="secondary"` on RadioGroup, not individual Radios. [Docs](https://heroui.com/en/docs/react/components/radio-group).

## Switch and SwitchGroup

Compose `Switch.Content` with Control, Label, and Description. Thumb belongs inside Control; an optional Icon belongs inside Thumb. Use `isSelected`, `defaultSelected`, and `onChange(boolean)`, not checkbox-library aliases.

Switch supports size, not a surface variant or color prop. SwitchGroup groups switches and defaults to vertical orientation. Use the field's `name` and supported `isRequired`, `isReadOnly`, or `isInvalid` props for forms. [Docs](https://heroui.com/en/docs/react/components/switch).

## NumberField

Put DecrementButton, Input, and IncrementButton inside `NumberField.Group`. Use `minValue`, `maxValue`, and `step`, which defaults to 1. `formatOptions` accepts number formatting such as currency or percent. Use `isFocusWithin`; invalid state hides Description.

On Surface, set `variant="secondary"` on NumberField itself. Group and Input consume its styles; do not put variant on them. [Docs](https://heroui.com/en/docs/react/components/number-field), [implementation](https://github.com/heroui-inc/heroui/blob/v3/packages/react/src/components/number-field/number-field.tsx).

## SearchField

Compose SearchIcon, Input, and ClearButton inside `SearchField.Group`. Enter calls `onSubmit(value)`; clearing calls `onClear()`. The clear button hides when empty. Use `isFocusWithin`; invalid state hides Description.

On Surface, set `variant="secondary"` on SearchField itself, not Group or Input. [Docs](https://heroui.com/en/docs/react/components/search-field), [implementation](https://github.com/heroui-inc/heroui/blob/v3/packages/react/src/components/search-field/search-field.tsx).

## Label and Description

Composed fields associate these parts automatically. Standalone Label needs `htmlFor` matching the input's id. Standalone Description needs an id referenced by `aria-describedby`.

Label's own `isRequired`, `isDisabled`, and `isInvalid` props change its appearance, not the control's validation. Set required state on the field; its Label supplies the indicator without manually duplicating asterisks across groups. [Label](https://heroui.com/en/docs/react/components/label), [Description](https://heroui.com/en/docs/react/components/description).

## FieldError and ErrorMessage

Use FieldError for form fields and ErrorMessage for non-form components such as TagGroup and Calendar. FieldError follows parent validation state and exposes a render function, such as `{(validation) => validation.validationErrors.join(", ")}`. Its `data-visible` attribute controls visibility.

[FieldError](https://heroui.com/en/docs/react/components/field-error), [ErrorMessage](https://heroui.com/en/docs/react/components/error-message).

## Fieldset and Form

Fieldset is structural and uses native props. Compose Legend, Group, and Actions; Group becomes two columns at the medium breakpoint. Form integrates field validation and submission. Its `onInvalid` focuses the first invalid field unless you override that behavior with `preventDefault()`.

Style Form with `className`; it has no component BEM class. Give it an accessible name when it should be a form landmark. Use `Button type="submit"` or `type="reset"` explicitly.

On Surface, apply `variant="secondary"` to the child controls at their documented owners. Neither Form nor Fieldset owns a field variant. [Fieldset](https://heroui.com/en/docs/react/components/fieldset), [Form](https://heroui.com/en/docs/react/components/form).
