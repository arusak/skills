---
name: ar-tailwind-format
description: Format and semantically group Tailwind classes in React components while preserving behavior.
disable-model-invocation: true
---

# Tailwind Format

Format Tailwind class strings in JSX and TSX files. Preserve styling behavior and keep edits focused on class expressions and required imports.

## Workflow

1. Run `git status --short`. Explicit user targets take priority. Without a target, select existing uncommitted JSX/TSX files containing Tailwind classes, including staged and untracked files. If no target is given and the working tree is clean, offer comparison with `master` or another base branch and wait for the user's choice. For an agreed branch comparison, select existing JSX/TSX files changed in `git diff --name-only <base>...HEAD` from the common ancestor.
2. Read every target and inspect the project's class helpers and their implementations. Reuse an internal `cn()`, direct `clsx`/`classnames` import, or equivalent established helper. If none exists, recommend adding `clsx`; continue with behavior-preserving formatting that needs no new helper, leaving installation for an explicit request.
3. Assess each `className` for readability. Around five classes is a cue to consider grouping with a helper, not a mandatory conversion threshold. Apply the grouping guidance below; leave expressions already clear and consistent unchanged. Match the file's import and quote style, using the actual helper path rather than assuming `@/lib/utils`.
4. Verify every changed expression preserves class tokens, conditional branches, precedence, and responsive behavior. A helper using `tailwind-merge` may remove conflicting utilities: inspect its behavior before converting and skip conversions whose equivalence is uncertain. Keep precedence-sensitive utilities and helper arguments in their original relative order.
5. Review the diff for focused edits, valid helper imports, coherent groups, and useful comments. Report each modified file with the number of `className` attributes reformatted, plus any skipped expressions or dependency recommendation. If no edits are needed, say so.

## Semantic grouping

For roughly 6–15 classes, use broad groups: layout, spacing and sizing; backgrounds, borders, rounding and shadows; typography, colors and states.

```tsx
className={cn(
  "flex items-center gap-4 p-6",
  "bg-background border border-border rounded-lg shadow-sm",
  "text-foreground hover:bg-accent transition-colors"
)}
```

For roughly 16+ classes, use smaller groups for layout, spacing, appearance, typography, transitions, states and responsive variants. Keep responsive utilities with their related base utilities when that makes the relationship clearer.

```tsx
className={cn(
  "flex flex-col gap-2",
  "p-4 md:p-6",
  "bg-card border border-input rounded-md",
  "shadow-sm hover:shadow-md",
  "text-sm text-muted-foreground",
  "transition-all duration-200",
  "focus-within:ring-2 focus-within:ring-ring"
)}
```

Prefer multi-class groups. A single-class line is appropriate when it is the only class or combining it would obscure a condition or reduce readability. Grouping yields to behavior preservation.

## Comments

Express ordinary styling through the groups themselves. Add a comment only when it explains non-obvious conditional styling, a layout workaround, meaningful z-index layering, or critical breakpoint behavior that the classes alone do not communicate.

## Conditional classes

Always add `cn()` when some conditional logic for classes has place.

```jsx
className={`border ${isAlert ? "border-alert" : "border-border"}`} // bad
className={cn("border", isAlert ? "border-alert" : "border-border")} // good
```
