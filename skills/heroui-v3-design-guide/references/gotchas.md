# Documentation conflicts

The [shared tables](shared-patterns.md) and component entries contain the implementation rules. This file records conflicts that could otherwise make an LLM choose the wrong API.

| Topic | Conflict and resolution |
| --- | --- |
| InputGroup, NumberField, SearchField | Some input-part API rows list variant. Their linked implementations own it on the root and pass styles to parts. Follow the root placement in the forms reference |
| ComboBox | The API table omits variant, but the on-surface example and root type support it |
| ButtonGroup outline | Examples and release notes include outline, while the API table omits it. Do not conclude it is unsupported from that table; check the installed type |
| Card colors | Documentation sections disagree about secondary/tertiary token mapping. Use documented variants without hard-coding that mapping |
| Surface transparent | The API includes transparent although the introductory variant list omits it |
| Kbd | Anatomy uses Abbr and Content; the API table also mentions Key/keyValue. Use anatomy supported by installed exports |

These are narrow documentation checks, not a guarantee for every v3 release. Component references link official docs and, where needed, implementation files. The public v3 branch can differ from the installed package. Resolve a mismatch against the installed types and source; do not suppress it with a cast.

[ButtonGroup examples](https://heroui.com/en/docs/react/components/button-group), [outline release note](https://heroui.com/en/docs/react/releases/v3-0-0-beta-4).
