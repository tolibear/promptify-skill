---
name: promptify
description: "+ask +deep +web <- modifiers | optimize your prompts"
---

# Prompt Optimizer

Transform the user's prompt into a clear, effective one. Model-agnostic. Concise output.

## Modifier Detection

Parse ARGUMENTS for these modifiers (any order, any combination):
- **+ask** → Ask 1-3 clarifying questions before optimizing
- **+deep** → Explore codebase for patterns and context
- **+web** → Web search for current best practices

Examples:
- `/promptify Write a landing page` → quick mode
- `/promptify +ask Help me debug this` → asks questions first
- `/promptify +deep Add an API endpoint` → explores codebase
- `/promptify +ask+deep+web Build auth system` → full power

**Check ARGUMENTS below and apply matching sections.**

---

## Always: Image Analysis

If an image is included, analyze it thoroughly:
- **Screenshots**: Note UI elements, layout, errors, or content shown
- **Diagrams**: Understand the structure, relationships, or flow depicted
- **Examples**: Use as reference for desired output style or format

Include image-derived context in the optimized prompt.

## Always: Context Awareness

Review the existing conversation for relevant context:
- Prior messages may contain domain knowledge, constraints, or preferences
- Reference specific details from chat (names, projects, goals)
- Incorporate implicit requirements from earlier discussion

**Structure context properly:**
- Label what's **rules** (immutable) vs **editable** (suggestions) vs **historical** (background)
- Order by relevance to the task
- Scope to only what's needed

---

## If +deep → Codebase Exploration

**Explore the codebase to gather relevant context.** Use Glob, Grep, Read to understand:
- Project structure and conventions
- Existing patterns and APIs
- Domain-specific terminology

Before optimizing:
1. **Identify relevant files** - What code relates to the prompt?
2. **Understand patterns** - How does this codebase do similar things?
3. **Check conventions** - Are there style guides, README, or CLAUDE.md?

---

## If +web → Web Research

Search the web for:
- Current best practices for the task domain
- API documentation if relevant
- Recent patterns or approaches (2024-2025)
- Framework-specific conventions

Incorporate findings into the optimized prompt's context section.

---

## If +ask → Clarifying Questions

Use AskUserQuestion tool. Ask 1-3 questions max. Tailor to prompt type:

**Coding prompts:**
- What language/framework?
- Error handling requirements?
- Performance constraints?

**Writing prompts:**
- Who is the audience?
- What tone? (formal/casual/technical)
- Length constraints?

**Analysis prompts:**
- What criteria matter most?
- How deep? (overview vs detailed)

**General:**
- What will this output be used for?
- Any hard constraints?

Only ask what's truly unclear - skip obvious ones.

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

Strip these from the optimized prompt:
- Excessive politeness ("please", "kindly", "I would like you to")
- Redundant framing ("I want you to...", "Can you...", "I need you to...")
- Filler words ("just", "really", "very", "actually")
- Apologetic language ("sorry if this is confusing")
- Over-explanation of obvious things

## Contract Checklist

Before outputting, verify all four non-negotiables are present:

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

## Output

1. Show optimized prompt in a code block
2. Copy to clipboard (macOS): `echo 'PROMPT' | pbcopy`
3. Brief explanation of changes (2-3 sentences max)
