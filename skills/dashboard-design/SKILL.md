---
name: dashboard-design
description: Should be triggered when the user requests the creation or editing of functional and structured user interfaces.
---

# Dashboard design

Instructions and guides for AI agents on the process of layout and construction of functional user interfaces such as dashboards or application interfaces.

## Process

1. Understand the project's purpose.
2. Check if the project already has a design system, UI library, primitive components, or building blocks to use, instead of recreating or duplicating components.
3. Follow established design conventions. If a UI library or design system is already available in the repository, it will already define sizes, colors, hierarchies, radii, states, shadows, etc. Don't try to define your own styles unless you have a justifiable reason.
4. When creating files, ensure you follow the file naming convention as well as the best practices for folder organization and structure specific to the repository's stack.
5. Analyze the user request and organize the content (see the following section).
6. Make sure you use clear language that corresponds visually (see Tone and Language section).

## Organize the content

### The information

- The content displayed must have a purpose. Make sure not to overwhelm the user with poor, unhelpful, or filler content. The main actions should be clear and easily recognizable. Each page should help you make a decision or take an action.
- Ensure you optimize the content displayed to the user. Prioritize useful information, data that they can recognize, compare, or that helps them take relevant actions related to the page's purpose.
- When data is not real-time, make its freshness clear. Show when it was last updated or how often it refreshes when that information matters to the user. Provide a way to request newer data when appropriate, while respecting any refresh or rate limits.

### The layout

- Establish a clear visual hierarchy. Organize information so users can quickly understand what is important, what is related, and what they can act on. Use size, position, spacing, and color intentionally to guide attention.
- Give actions a clear hierarchy. Distinguish primary, secondary, and tertiary actions, and avoid giving multiple actions competing visual emphasis unless they are genuinely equivalent.
- Keep important actions visible and easy to find. Do not hide frequently used or high-priority actions behind menus, hover states, or additional navigation without a good reason.
- Avoid unnecessary steps, interactions, or navigation. Do not reduce steps at the expense of clarity, safety, or comprehension.
- Group related information and controls together. Keep unrelated content visually separated so users can understand the structure of the page without having to inspect every element.
- Match the interaction pattern to the scope of the task. Keep small, contextual interactions inline when they naturally belong to the surrounding content. Use dialogs or sheets for focused tasks that temporarily require the user's attention, and prefer dedicated pages for complex, multi-step, or information-dense workflows.
- Inline patterns such as accordions, expanders, expandable rows, inline editing, and contextual details are appropriate when they preserve context and have a clear relationship with the surrounding content.
- Avoid introducing content in ways that unexpectedly obscure, replace, or significantly disrupt the user's current context.
- Use available space deliberately. Prefer layouts that make important information easier to scan, compare, and act on. Do not add content, oversized elements, or decoration solely to fill empty space.
- Choose components based on the type and amount of information they need to communicate. Do not force content into cards, tables, dialogs, or other patterns when another structure would make it easier to understand or use.
- Design for realistic content rather than idealized placeholders. Account for long labels, empty states, missing values, large datasets, loading states, errors, and different viewport sizes.
- Preserve usability across screen sizes. Reorganize, collapse, or reprioritize content when necessary instead of simply shrinking the desktop layout.

## Notifications and Feedback

- Show feedback close to the action or element that caused it.
- Prefer inline messages for errors, warnings, and information that requires attention.
- Use temporary notifications only for low-importance confirmations such as “Copied” or “Saved”.
- Do not hide important information behind messages that disappear automatically.
- Avoid placing critical actions inside temporary notifications.
- Make messages understandable without relying only on color, position, or animation.
- Ensure dynamic messages work with keyboard navigation, zoom, and screen readers.
- Avoid stealing focus or interrupting the user unless immediate action is required.

**Golden rule:** if the user needs to read, remember, fix, or act on a message, keep it visible.

## Secondary panels and asides

Avoid introducing a persistent secondary column unless the content clearly benefits from remaining visible alongside the primary workspace. Preserve horizontal space for the main content, especially for tables, boards, editors, dashboards, and other width-sensitive interfaces.

Prefer placing compact controls, filters, summaries, and actions within the relevant header, toolbar, or content area. Do not create an aside merely to separate secondary information from the main flow.

Use an aside or inspector panel when it contains enough persistent, contextual information or controls to justify reducing the width of the primary workspace, such as inspecting or editing the currently selected item. If the content is occasional or lightweight, prefer an inline placement, popover, dialog, or temporary sheet instead.

## Tone and Language

- Write UI text for the person using the interface, not for the person who requested or implemented it.
- Do not expose implementation instructions, design decisions, component choices, or internal requirements as UI text. The interface should communicate what the user needs to know or do, not explain how it was built.
- Phrase actions and descriptions according to who they apply to. When the current user is the subject, use direct language such as "Your password" or simply "New password." When acting on another person or entity, identify the subject when needed for clarity.
- Prefer concise, task-oriented language. Labels and supporting text should help users understand an action, restriction, state, or consequence.
- Address the user directly when explaining constraints or required actions instead of describing users in the abstract.

DON'T:

> Instruction: Display the content in cards instead of a table.
> UI Text: Content is displayed in cards.

> Instruction: Use badges to show order status.
> UI Text: Orders use badges to display statuses.

> Instruction: Users can select up to two options.
> UI Text: Users can only choose two options.

> Instruction: The data should be updated every 5 minutes.
> UI Text: Users see updated information every 5 minutes.

DO:

> Instruction: Users can select up to two options.
> UI Text (supporting text): You can select up to two options.

> Instruction: The file size limit is 10 MB.
> UI Text (supporting text): Maximum file size: 10 MB.

> Instruction: Archived projects are read-only.
> UI Text (status message): This project is archived and can no longer be edited.

> Instruction: The data should be updated every 5 minutes.
> UI Text (supporting text): Last updated N minutes ago · Updates every 5 minutes.
