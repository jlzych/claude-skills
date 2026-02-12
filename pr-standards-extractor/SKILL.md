---
name: pr-standards-extractor
description: "Extract coding standards from PR review comments and add them to CLAUDE.local.md."
license: MIT
---

# PR Standards Extractor

## Overview

This skill extracts coding standards and conventions from GitHub PR review comments and adds them to the project's `CLAUDE.local.md` file. PR reviews often contain valuable insights about team conventions, architectural decisions, and coding patterns that should be captured as persistent project instructions.

The skill reads all comments from a PR (both review comments and general comments), identifies actionable coding standards, checks what's already documented in `CLAUDE.local.md`, and adds new standards or augments existing ones.

## When to Use This Skill

- The user says `/pr-standards` or asks to extract standards from a PR
- The user references a PR number and wants to capture review feedback as project conventions

## Instructions

When this skill is invoked, follow these steps:

### Step 1: Identify the PR

The user will provide a PR number (e.g., `#3396` or just `3396`). If no PR number is provided, ask for one.

### Step 2: Fetch PR Comments

Use `gh` to fetch all comments from the PR:

```bash
# Get PR review comments (inline code comments)
gh api repos/{owner}/{repo}/pulls/{number}/comments --paginate

# Get PR issue comments (general discussion)
gh api repos/{owner}/{repo}/issues/{number}/comments --paginate

# Get the PR description for context
gh pr view {number} --json body,title
```

Determine `{owner}/{repo}` from the git remote:
```bash
gh repo view --json nameWithOwner -q .nameWithOwner
```

### Step 3: Analyze Comments for Coding Standards

Review all comments and identify:

- **Explicit conventions**: "We always do X", "Never do Y", "Prefer A over B"
- **Architectural patterns**: How data flows, where logic belongs, API design patterns
- **Anti-patterns caught in review**: Things the reviewer flagged as wrong approaches
- **Performance guidelines**: Query optimization, batching, caching patterns
- **Naming conventions**: How things should be named, structured, or organized
- **Type/schema patterns**: How IDs relate, how filters work, data relationships

Focus on comments that represent **general, reusable standards** — not one-off bug fixes or typo corrections.

For each standard identified, note:
- The convention itself (what to do or not do)
- Why it matters (from the reviewer's explanation)
- A concrete example from the PR (good and/or bad patterns)

### Step 4: Read Existing CLAUDE.local.md

Read the project's `CLAUDE.local.md` to understand what's already documented. The file is at `{project_root}/CLAUDE.local.md` — find the project root by looking for the nearest directory containing `CLAUDE.md` or `.git`.

If `CLAUDE.local.md` doesn't exist, create it with a header.

### Step 5: Compare and Merge

For each identified standard:

1. **Already documented and complete**: Skip it
2. **Already documented but incomplete**: Augment the existing section with new details, examples, or clarifications from the PR
3. **Not yet documented**: Add a new section

When augmenting, add a reference to the PR (e.g., "Guidelines from PR review #3396:") so the origin is traceable.

### Step 6: Write Updates

Edit `CLAUDE.local.md` with the new or augmented standards. Follow the existing file's formatting conventions. Group related standards together logically.

### Step 7: Present Summary

After updating, show the user:
- How many new standards were added
- How many existing standards were augmented
- A brief summary of each change

## Formatting Guidelines

- Use the same Markdown style as the existing `CLAUDE.local.md`
- Include code examples (good and bad patterns) when available from the PR
- Keep descriptions concise but complete
- Use headers (`##`, `###`) to organize by topic
- Reference the source PR number for traceability
- Use tables when comparing patterns or listing field mappings

## Anti-Patterns

### Capturing One-Off Fixes as Standards

**What it looks like**: Adding "fix the typo in line 42" as a coding standard.

**Instead**: Only capture patterns that would apply to future code — general rules, not specific fixes.

### Over-Documenting Obvious Things

**What it looks like**: "Use proper variable names" or "Write clean code."

**Instead**: Focus on project-specific conventions that someone new wouldn't intuit from the codebase alone.

### Duplicating Without Checking

**What it looks like**: Adding a standard that's already well-documented in `CLAUDE.local.md`.

**Instead**: Always read the existing file first and augment rather than duplicate.
