# PR Standards Extractor

Extract coding standards and conventions from GitHub PR review comments and automatically add them to your project's `CLAUDE.local.md` file.

## What It Does

PR reviews often contain valuable insights about team conventions, architectural decisions, and coding patterns. This skill captures those insights by:

1. Reading all comments from a GitHub PR (review comments and discussions)
2. Identifying actionable coding standards and conventions
3. Checking what's already documented in `CLAUDE.local.md`
4. Adding new standards or augmenting existing ones with examples from the PR

## Usage

```
/pr-standards 123
```

This extracts standards from PR #123 and updates your project's documentation.

## Benefits

- **Avoid repetition**: Standards get documented once, referenced many times
- **Keep conventions fresh**: Review feedback becomes persistent project knowledge
- **Onboarding**: New team members can read documented conventions vs guessing from code
- **Accountability**: All standards are traceable to the PR where they were discussed

## License

MIT
