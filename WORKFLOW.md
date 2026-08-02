# WORKFLOW.md

## Feature
Settings form with Name, Email, Password fields.

## Round 1 (Vague Prompt: "build a settings form")
- Correctness: Form submitted with empty or invalid data — no validation at all.
- Accessibility: No <label> elements, inputs only had placeholder text.
- Edge cases missed: Empty email accepted, 1-character passwords accepted.
- Review/fix time: ~5 minutes to notice missing validation.

## Round 2 (Precise Prompt with constraints + verification)
- Correctness: Zod schema rejects invalid email, empty name, and short passwords before submit.
- Accessibility: Every input has an associated <label htmlFor>, aria-invalid toggles on error, error text uses role="alert".
- Edge cases handled: empty fields, malformed email, short password all blocked with visible messages.
- Review/fix time: ~10 minutes to review the schema and test manually in the browser.

## Specific Diff Highlights
- Round 1's SettingsForm.jsx had zero validation logic; Round 2 added a zod schema that Round 1 never had.
- Round 1 used placeholder-only inputs; Round 2 added explicit <label> tags — an accessibility gap I had to catch manually in Round 1.
- Round 1 had no error messages at all; Round 2 shows a specific message per field.

## AI Mistake Caught
In Round 1, the form allowed a 1-character password to be submitted successfully with no error, since there was no validation logic at all. I caught this by manually typing a single character and watching it submit with no error shown.

## Time Comparison
Round 1: ~2 min prompting + ~15 min catching problems afterward = ~17 min total.
Round 2: ~15 min writing the detailed prompt and installing dependencies + ~10 min reviewing = ~25 min total, but delivered a working, validated, accessible form with no follow-up fixes needed.

## Takeaway
Round 2 took longer upfront but needed almost no rework afterward, while Round 1 looked "done" fast but had validation and accessibility gaps that would have needed a second pass anyway. Specifying constraints (validation library, accessibility requirements) up front moved the review burden earlier, where it was cheaper to fix.