# When to use Text input

Use a text input to collect a single line of text from the user.
Label every input — placeholder text is not a label substitute.

## When to use

- One-line text entry — name, email, search query, identifier.
- Numeric entry where the format is text-shape (currency with
  symbol, formatted phone number).

## When not to use

- For multi-line text, use the textarea recipe (subsequent
  milestone).
- For selection from a known list, use a select or combobox.
- For booleans, use a checkbox or switch.

## Anatomy

| Element | Purpose |
|---|---|
| Label | Above the input, always visible. utility-1 weight 600. |
| Input field | The text entry. 40px height, semantic border. |
| Helper text | Below the input. utility-1 weight 400. Used for guidance OR errors. |

## States

- **Default** — neutral border, no focus ring.
- **Focus** — primary border + 2px focus ring.
- **Disabled** — surface-subtle background, ink-disabled text.
- **Error** — critical border, critical helper text. Set
  `aria-invalid="true"` on the input.

## Brand voice

Labels are nouns or noun phrases: `Email address`, `Account
identifier`. Avoid imperatives in labels — `Enter your email`
becomes the placeholder, the label is `Email`.

Helper text is one short sentence that completes the thought:
`We'll only use this for account recovery.` not `Please enter
your email so we can send you a recovery link if necessary.`

Error messages are direct and actionable: `Email address is
required.` not `Oops! Looks like you forgot something.`
