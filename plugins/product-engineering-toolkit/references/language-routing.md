# Language routing

Use `../locales/registry.json` as the source of truth for supported locales and localized command aliases.

## Detection order

Resolve the response locale in this order:

1. An explicit language preference in the user’s request.
2. The language of the current user request.
3. The established language of the conversation.
4. English when the language is unsupported or detection is uncertain.

If the request is mixed-language, use the dominant language unless the user explicitly asks for another language. Do not infer a locale from nationality, name, location, or email address.

## File selection

- If the user invokes a localized command, select the command file named by the registry and invoke its canonical skill.
- If the user makes a natural-language request, select the canonical skill by intent and use the detected locale for the response and any available localized artifact template.
- If no localized artifact exists, use the canonical English template and translate its user-facing labels while preserving its machine-readable fields.
- Preserve the canonical skill ID in handoffs, evidence records, filenames, and metadata so reports remain traceable across languages.

## Output rules

- Translate explanations, findings, recommendations, and headings into the resolved response language.
- Keep skill IDs, command IDs, file paths, code symbols, and evidence field names stable.
- Use canonical evidence values (`confirmed`, `inferred`, `unknown`, and `needs validation`) for machine-readable status; a translated display label may appear alongside them.
- If confidence is low, state the detected language and ask whether the user wants another language before producing a large artifact.
