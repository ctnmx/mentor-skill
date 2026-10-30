# 🎓 Mentor

> Turn Claude Code from a black-box code generator into an elite pair-programming tutor.
> Learn by doing. Zero fluff. 100% domain-agnostic.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-black.svg)](https://claude.ai)

---

## The Problem

AI coding assistants are extraordinary at writing code, but terrible at teaching you. 
You type a prompt, working code appears, and you hit `git push`. 

**The result?** You build software you don't understand, accumulate personal cognitive debt, and become dependent on the AI.

## The Solution

`mentor` is an adaptive agent skill designed for [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) (and compatible agent harnesses).

Instead of dumping opaque code:
1. **Explains the *Why***: Reveals the machine invariants, OS constraints, and architectural trade-offs behind the solution.
2. **Zero-Exam Dynamic Calibration**: Calibrates explanation level automatically from your prompts (expert in POSIX, novice in x86 disassembly, intermediate in React).
3. **Hyper-Compact Memory**: Silently tracks your cross-domain knowledge in a 20-line `.mentor-matrix.md` file without wasting your token budget.
4. **Domain-Agnostic**: Works identically for low-level reverse engineering, frontend state management, database query optimization, or cloud infrastructure.

---

## Quick Install

### Global Install (Recommended for Claude Code)

Clone or copy `SKILL.md` into your Claude Code skills directory:

```bash
# In your ~/.claude directory
mkdir -p ~/.claude/skills/mentor
curl -sSL https://raw.githubusercontent.com/ctnmx/mentor-skill/main/SKILL.md -o ~/.claude/skills/mentor/SKILL.md
```

Or clone the repo:
```bash
git clone https://github.com/ctnmx/mentor-skill.git ~/.claude/skills/mentor
```

### Project-level Install

Drop `SKILL.md` into your project's `.claude/skills/` directory:

```bash
mkdir -p .claude/skills/mentor
cp /path/to/SKILL.md .claude/skills/mentor/SKILL.md
```

---

## How to Invoke

In your Claude Code session:

```bash
/mentor              # Activate default balanced mentor mode
/mentor deep         # In-depth analogies, step-by-step breakdown & checkpoint question
/mentor socratic     # Gives logic & boilerplate, asks you to write the critical line
/mentor flash        # Fast 1-line architectural rationale for when you're in a rush
/mentor status       # Check current calibration and tracked domains
stop mentor          # Revert to standard assistant behavior
```

---

## Intensity Modes

| Mode | Role | When to use | Behavior |
|---|---|---|---|
| `deep` | Full Teacher | Learning completely new concepts | Physical analogy, 2-3 execution steps, key line annotations, 1 retention check. |
| `balanced` (default) | Pair Programmer | Daily development & learning | 1-2 sentence concept explanation before code. Focus on the invariant *why*. |
| `socratic` | Challenge / Retention | Preparing for interviews or deep mastery | Explains logic, leaves the critical line empty with targeted hints. |
| `flash` | Fast Track | Deadlines & hurry | 1-line architectural rationale before payload. Zero blind copy-pasting. |

---

## Example: Reverse Engineering x86

**Standard AI Output:**
```assembly
mov eax, [ebp-4]
add eax, 1
mov [ebp-4], eax
```

**With `mentor` (Adaptive mode):**
> Functions need scratchpad memory. Local variables reside on the stack right behind the base pointer (`ebp`). 
> This fetches local variable `#1` into the `EAX` working register, increments it, and writes it back to stack memory:
```assembly
mov eax, [ebp-4]    ; WHY: load local_1 into CPU register
add eax, 1          ; WHY: increment
mov [ebp-4], eax    ; WHY: write updated value back to stack slot
```

---

## Auto-Clarity & Safety

`mentor` automatically suspends itself and reverts to direct emergency mode when:
- An active production outage or broken build occurs.
- You say "urgent", "just fix it", or "no time".
- Destructive or irreversible operations (database drops, disk formats, forced pushes) require exact confirmation.

Once the emergency is resolved, `mentor` resumes seamlessly.

---

## License

[MIT](LICENSE) © 2026 solidmax
