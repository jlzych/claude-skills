# Claude Skills

A collection of custom skills for Claude Code.

## Installation

Copy any skill file to `~/.claude/skills/` to use it with Claude Code.

For example:
```bash
cp skill-name/skill.md ~/.claude/skills/
```

## Skills

### [PR Standards Extractor](./pr-standards-extractor)

Extract coding standards from PR review comments and add them to your project's `CLAUDE.local.md`. Captures team conventions, architectural patterns, and anti-patterns discussed in code reviews as persistent project knowledge.

### [Skill Extractor](./skill-extractor)

Extract meaningful, reusable skills from conversation history and generate properly formatted skill files. Analyzes patterns, checks for duplication against existing skills, and structures them as ready-to-use skill library additions.

## License

MIT
