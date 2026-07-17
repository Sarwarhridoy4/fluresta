# AGENTS.md

## Purpose

This file contains instructions for analyzing Fluresta course markdown files and generating structured learning outcomes and summaries.

## Workflow

When working with Fluresta course materials:

1. **Analyze** all `.md` files in the repository to identify class content
2. **Extract** key learning outcomes from each class's table of contents and content sections
3. **Write** structured learning outcomes and concise summaries to `@learning_outcomes.md`
4. **Link** `@learning_outcomes.md` in `@README.md` under the Classes section

## File Analysis Instructions

- Read each class markdown file completely
- Identify the Table of Contents to understand all covered topics
- Extract the "Summary" or "Best Practices" sections as the class summary
- Derive 3-5 specific learning outcomes per class from the topics covered
- Focus on actionable knowledge: commands, concepts, tools, and techniques taught

## Output Format for learning_outcomes.md

Each class section should contain:

```markdown
## Class XX - [Class Title](class_file.md)

### Learning Outcomes

- Outcome 1
- Outcome 2
- Outcome 3
- Outcome 4

### Summary

[Concise 2-4 sentence summary of the class content]
```

## README.md Updates

Add a new entry in the README.md under the `## Classes` section:

```markdown
- [Learning Outcomes](learning_outcomes.md)
  - [Class 01 - ...](learning_outcomes.md#class-01)
  - [Class 02 - ...](learning_outcomes.md#class-02)
  ...
```

## Quality Standards

- Learning outcomes must be measurable and specific
- Summaries should capture the essence of each class without unnecessary detail
- All markdown links must be valid relative paths
- Maintain consistent formatting across all class sections
