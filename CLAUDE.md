# CLAUDE.md

## Project Rules

1. All forms must use react-hook-form + zod for validation — never build unvalidated or uncontrolled inputs.
2. Every input must have an associated <label htmlFor="..."> — placeholder text alone is not acceptable for accessibility.
3. Error messages must be field-specific and visible in the UI (using role="alert"), not just logged to console.