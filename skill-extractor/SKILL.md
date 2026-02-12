---
name: skill-extractor
description: "Extract meaningful, reusable skills from conversation history and generate properly formatted skill files."
license: MIT
---

# Skill Extractor

## Overview

This skill extracts meaningful, reusable patterns from conversation history and structures them as properly formatted skill files. It provides a systematic framework for identifying patterns worth preserving, evaluating them against existing skills to avoid duplication, and generating skill files that can be added to the skill library.

## When to Use This Skill

- The user invokes `/skill-extractor`
- The user asks to extract skills from a conversation or capture patterns for future reuse
- The user wants to formalize ad-hoc workflows into documented, reusable skills

## Instructions

When this skill is invoked, follow these steps:

### Step 1: Analyze the Conversation

Review the current conversation history to identify patterns worth capturing:

- **Recurring multi-step workflows**: Processes that happened multiple times or have clear, reusable steps
- **Problem-solving approaches**: Systematic methods for debugging, designing, or implementing solutions
- **Decision frameworks**: Structured thinking for choosing between options or evaluating tradeoffs
- **Domain-specific patterns**: Conventions, best practices, or specialized techniques relevant to a domain
- **Meta-processes**: Ways of organizing work, communicating with users, or structuring investigations

For each potential skill, note:
- What the pattern is (the core workflow or approach)
- Why it's valuable (when and why someone would want to use it)
- What inputs it needs (what information the user provides)
- What outputs it produces (what the user gets back)
- Step-by-step instructions for executing it

### Step 2: Filter for Reusable Patterns

Not every conversation pattern should become a skill. Keep only patterns that are:

- **General enough**: Applies to multiple contexts, not just this specific conversation
- **Valuable enough**: Solves a real problem or saves meaningful time/effort
- **Complete enough**: Can be executed with clear, step-by-step instructions
- **Distinct**: Represents a coherent, well-defined workflow

Discard patterns that are:
- One-off solutions to specific problems
- Already well-covered by existing Claude features
- Vague or hard to document with clear steps
- Overly narrow or niche

### Step 3: Check for Duplication

For each extracted pattern, check if it already exists:

1. Review the skill names from the system reminder (available skills listed at the start of conversations)
2. Read the existing SKILL.md files in the claude-skills project to understand what's already covered
3. Evaluate whether your extracted pattern is:
   - **A duplicate**: Don't extract it; the user should use the existing skill instead
   - **Complementary**: Solves a different problem or covers a different context; extract it
   - **An enhancement**: Similar to an existing skill but with improvements; discuss with the user whether to extract as new skill or suggest enhancing the existing one

### Step 4: Structure Each Skill

For each skill to extract, create a structured skill file with:

**Frontmatter**:
```
---
name: skill-name
description: "One-line description of what the skill does."
license: MIT
---
```

**Overview Section**: 2-3 sentences explaining what the skill does and why it matters

**When to Use Section**: Specific trigger phrases or situations where this skill applies

**Instructions Section**: Step-by-step guide for executing the skill:
- Use numbered steps for linear processes
- Use sub-steps (with letters or additional numbering) for branching logic
- Be explicit about what information is needed at each step
- Include examples of commands or queries to run
- Note any special cases or considerations

**Anti-Patterns Section** (optional): Common mistakes or misuses to avoid, with explanations

**Formatting Guidelines**:
- Use clear, action-oriented language ("fetch all comments", "identify actionable standards")
- Include code examples or command templates where relevant
- Keep descriptions concise but complete
- Organize with headers and sections
- Use lists and tables for clarity

### Step 5: Present Extracted Skills

Show the user:
- Each extracted skill with its name, description, and overview
- Why each skill is valuable and when to use it
- Any duplication findings and recommendations
- Instructions for adding the skills to their skill library

Ask the user which skills they want to:
- Generate and save to files
- Refine or modify
- Discard

### Step 6: Generate Skill Files

For each skill the user approves:

1. Generate the complete SKILL.md file with all sections
2. Generate a concise README.md file (user-facing documentation)
3. Show the user the file contents
4. Either create the files in their claude-skills project (if it exists) or provide them as output

## Skill File Template

Use this template structure for the SKILL.md file:

```
---
name: skill-name
description: "Brief one-line description."
license: MIT
---

# Skill Name

## Overview

[2-3 sentence explanation of what the skill does and why it's valuable]

## When to Use This Skill

- Specific trigger: User says X or asks about Y
- Context: When the user needs to do Z

## Instructions

### Step 1: [First major step]

[Detailed explanation and how to execute]

### Step 2: [Second major step]

[Detailed explanation and how to execute]

[Additional steps as needed]

## Anti-Patterns

### [Common mistake 1]

[Explanation of the mistake and the right approach]

### [Common mistake 2]

[Explanation of the mistake and the right approach]
```

## Evaluation Criteria

When deciding if a pattern is worth extracting as a skill, ask:

**Does it solve a real problem?** Would someone benefit from using this approach again?

**Is it repeatable?** Could another person follow the steps and get good results?

**Is it distinct?** Does it represent a coherent, well-defined workflow (not just "do X then do Y")?

**Is it general enough?** Does it apply to multiple contexts, or is it too specific to this conversation?

**Would it change how someone works?** Does it improve outcomes, save time, or make thinking clearer?

If the answer to most of these is "yes," it's a good candidate for extraction.
