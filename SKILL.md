---
name: promptify
description: Optimize prompts for clarity and effectiveness. Use when user says "improve this prompt", "optimize my prompt", "make this clearer", or provides vague/unstructured prompts. Intelligently routes to sub-agents for codebase research, clarifying questions, or web search as needed.
metadata: {"moltbot":{"emoji":"✨"}}
---

# Prompt Optimizer

Transform prompts into clear, effective ones. Model-agnostic. Concise output.

## Modifier Detection (Optional Overrides)

Parse ARGUMENTS for explicit modifiers (any order, any combination):
- **+ask** → Force clarifying questions before optimizing
- **+deep** → Force codebase exploration
- **+web** → Force web search for best practices

Examples:
- `/promptify Write a landing page` → auto-detect mode
- `/promptify +ask Help me debug this` → forces clarification
- `/promptify +deep Add an API endpoint` → forces codebase research
- `/promptify +ask+deep+web Build auth system` → all agents

## Auto-Detection Logic

**If no modifiers specified, analyze the prompt and trigger agents when:**

### Trigger codebase-researcher when:
- References "this project", "our API", "existing code", "current implementation"
- Mentions specific files, functions, or modules
- Asks to add/modify features in existing system
- Uses terms like "integrate", "extend", "refactor"

### Trigger clarifier when:
- Ambiguous requirements ("make it better", "fix this thing")
- Multiple valid interpretations exist
- Missing critical constraints (audience, format, scope)
- Vague pronouns ("this", "it") without clear referents

### Trigger web-researcher when:
- Mentions "best practices", "current standards", "modern approach"
- References external APIs, services, or libraries
- Asks about framework-specific patterns
- Includes "2024", "2025", "latest" version references

## Agent Dispatch

When agents are needed:

1. **Announce which agents will run and why**
2. **Run applicable agents in parallel using Task tool**
3. **Synthesize findings into unified context**
4. **Proceed with optimization using gathered context**

Agent files are in `agents/` directory:
- `codebase-researcher.md` - Deep codebase exploration
- `clarifier.md` - Targeted clarifying questions
- `web-researcher.md` - Web search for best practices

---

## Core Optimization (Always Applied)

### Image Analysis
If an image is included:
- **Screenshots**: Note UI elements, layout, errors, or content shown
- **Diagrams**: Understand structure, relationships, or flow depicted
- **Examples**: Use as reference for desired output style

Include image-derived context in the optimized prompt.

### Context Awareness
Review existing conversation for relevant context:
- Prior messages may contain domain knowledge, constraints, preferences
- Reference specific details from chat (names, projects, goals)
- Incorporate implicit requirements from earlier discussion

**Structure context properly:**
- Label what's **rules** (immutable) vs **editable** (suggestions) vs **historical** (background)
- Order by relevance to the task
- Scope to only what's needed

---

## Prompt Type Detection

Auto-detect and apply type-specific techniques:

| Type | Signals | Focus |
|------|---------|-------|
| **Coding** | code, function, API, debug, implement | Precise specs, edge cases, language/framework |
| **Writing** | write, draft, blog, email, copy | Tone, audience, length, style |
| **Analysis** | analyze, compare, evaluate, review | Criteria, structure, depth |
| **Creative** | brainstorm, ideas, generate, design | Constraints, quantity, novelty |
| **Data** | extract, parse, transform, format | Input/output format, edge cases |

## Process vs Output Detection

**Critical:** Detect if user asks for OUTPUT ("write me X") vs PROCESS ("analyze then write").

Process-oriented prompts get better results. When user asks for raw output, convert to process:

- "Write me a landing page" → "First, identify the target audience's primary pain points. Then, define positioning that addresses those. Then, write the page. Show reasoning at each step."

Add process steps appropriate to the task type:
- **Coding:** Analyze requirements → Plan approach → Implement → Validate
- **Writing:** Understand audience → Define angle → Draft → Refine
- **Analysis:** Gather context → Define criteria → Evaluate → Synthesize

## Anti-Pattern Removal

Strip from the optimized prompt:
- Excessive politeness ("please", "kindly", "I would like you to")
- Redundant framing ("I want you to...", "Can you...", "I need you to...")
- Filler words ("just", "really", "very", "actually")
- Apologetic language ("sorry if this is confusing")
- Over-explanation of obvious things

## Contract Checklist

Before outputting, verify all four non-negotiables:

| Element | Question | If Missing |
|---------|----------|------------|
| **Role** | Who is the model? | Add specific persona with expertise |
| **Task** | What exactly must it do? | Make action explicit and specific |
| **Constraints** | What rules apply? | Infer reasonable ones from context |
| **Output** | What does "done" look like? | Specify format, length, structure |

If any element is missing or vague, fix it.

## Optimization Techniques

Apply as needed:
1. **Specificity** - Replace vague words ("good", "better") with criteria
2. **Structure** - XML tags for complex prompts: `<context>`, `<task>`, `<format>`
3. **Constraints** - Add "Do NOT..." when helpful
4. **Format spec** - Clarify expected output structure
5. **Persona** - Add role if task benefits from expertise framing
6. **CoT** - "Think step by step" for reasoning tasks

---

## Output

1. Show optimized prompt in a code block
2. Copy to clipboard (macOS): `echo 'PROMPT' | pbcopy`
3. Brief explanation of changes (2-3 sentences max)
