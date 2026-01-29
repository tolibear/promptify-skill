# promptify

Optimize prompts for clarity and effectiveness.

Works in **Claude Code** and **molt.bot**.

## Usage

```
/promptify Write a landing page
```

## Smart Auto-Detection

Unlike manual modifier systems, promptify automatically detects what your prompt needs:

| Your Prompt | Auto-Triggers |
|-------------|---------------|
| "Add auth to our API" | Codebase research |
| "Help me with this thing" | Clarifying questions |
| "Best practices for React hooks" | Web search |
| "Write a landing page" | Direct optimization |

## Optional Modifiers

Force specific capabilities when needed:

- `+ask` - Ask clarifying questions first
- `+deep` - Explore codebase for context
- `+web` - Search web for best practices

```
/promptify +ask+deep Build a new feature
```

## What It Does

1. **Analyzes** your prompt for type (coding, writing, analysis, creative, data)
2. **Routes** to sub-agents when context is needed
3. **Optimizes** using proven techniques:
   - Converts output requests to process-oriented prompts
   - Adds missing role/task/constraints/output spec
   - Removes anti-patterns (filler words, over-politeness)
   - Structures context with XML tags when helpful
4. **Outputs** clean prompt + copies to clipboard

## Install

**Claude Code:**
```bash
/install-plugin tolibear/promptify-skill
```

**Molt.bot:**
```bash
npx molthub install promptify
```

## License

MIT
