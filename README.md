# CLI Design System

A comprehensive design system and standards guide for command-line interfaces, packaged as a Claude Code plugin.

Covers four layers of CLI design: **Contract** (commands, flags, arguments, exit codes, I/O, configuration), **UX** (help, errors, feedback, interactivity, discoverability, copy and tone), **UI** (color, typography, spacing, terminal components), and **Documentation** (README structure, command docs, changelogs, migration guides).

Language and framework agnostic. Sources include POSIX Utility Conventions, GNU Coding Standards, [clig.dev](https://clig.dev/), 12 Factor CLI Apps, and practices observed in CLIs like gh, ripgrep, kubectl, and Docker.

## What's included

This plugin contains three skills:

| Skill | Purpose | Invocation |
|-------|---------|------------|
| **cli-design-system** | Design knowledge and standards — auto-loaded when Claude works on CLI-related tasks | Automatic |
| **cli-audit** | Audit a CLI against the standards, producing a scored report with violation map and command health dashboard | `/cli-design-system:cli-audit` |
| **cli-copy-review** | Review and fix human-facing strings (tone, vocabulary, punctuation, consistency) — strings only, no logic changes | `/cli-design-system:cli-copy-review` |

## Installation

### Claude Code (plugin marketplace)

```
/plugin marketplace add fvena/cli-design-system
```

### Claude Code (manual)

```bash
git clone https://github.com/fvena/cli-design-system.git
claude --plugin-dir ./cli-design-system
```

### Other agents (Codex, Cursor, VS Code Copilot)

The `skills/cli-design-system/` directory follows the [Agent Skills](https://agentskills.io) open standard and can be used standalone:

```bash
# Codex CLI
git clone https://github.com/fvena/cli-design-system.git
cp -r cli-design-system/skills/cli-design-system ~/.codex/skills/

# Cursor
git clone https://github.com/fvena/cli-design-system.git .cursor/skills/cli-design-system

# VS Code / GitHub Copilot
git clone https://github.com/fvena/cli-design-system.git
cp -r cli-design-system/skills/cli-design-system .github/skills/
```

Note: The audit and copy-review skills use Claude Code plugin features. The knowledge skill works on any agent that supports the Agent Skills standard.

## Usage

### As design reference (automatic)

The knowledge skill loads automatically when Claude detects CLI-related work — designing commands, implementing terminal output, writing help text, choosing flags, formatting errors, documenting a CLI. No explicit invocation needed.

### Auditing a CLI

```
/cli-design-system:cli-audit
```

The audit evaluates a CLI across all four layers and produces:

- **Command inventory** with types, flags, and output classification
- **Exit code scenario table** testing every command against failure scenarios
- **Error scenario matrix** evaluating error quality per command
- **Violation map** grouping findings by violation (systemic patterns visible)
- **Command health dashboard** scoring each command individually
- **Layer scores** (Contract, UX, UI, Docs) out of 100

### Reviewing copy and tone

```
/cli-design-system:cli-copy-review
```

Reviews all human-facing strings against the copy style guide. Checks tone, vocabulary, tense, punctuation, and cross-command consistency. Produces a change report grouped by violation type (tone → structure → wording → format) and applies string-only fixes. Safe to run independently of a full audit.

## Reference files

The knowledge skill contains 16 reference files organized by layer:

**Principles:** Universal rules that apply across all layers — predictability, safe defaults, composability, reversibility, empathy, and more.

**Contract layer:** Command structure and naming, flag conventions (POSIX/GNU), positional arguments, exit codes and signal handling, I/O stream rules, configuration hierarchy (XDG, env vars, precedence).

**UX layer:** Help system design, error message structure and templates, progress feedback and verbosity, interactivity and confirmations, discoverability (completions, suggestions, onboarding), copy style (voice, tone, vocabulary, punctuation).

**UI layer:** Semantic color system with NO_COLOR/FORCE_COLOR/TERM=dumb support, typography and output anatomy (header → body → detail → summary → next step), terminal components (glyphs, tables, trees, diffs, progress indicators, JSON mode).

**Documentation layer:** README structure, command documentation standards, flag documentation format, exit code documentation, configuration documentation, changelog and migration guide conventions.

## Structure

```
cli-design-system/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── cli-design-system/           # Knowledge (auto-load)
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── principles.md
│   │       ├── contract/            # 6 files
│   │       ├── ux/                  # 6 files
│   │       ├── ui/                  # 3 files
│   │       └── docs/                # 1 file
│   ├── cli-audit/                   # Audit (manual)
│   │   ├── SKILL.md
│   │   ├── audit-checklist.md
│   │   └── scoring-rubric.md
│   └── cli-copy-review/            # Copy review (manual)
│       └── SKILL.md
├── LICENSE
└── README.md
```

## Sources

- [POSIX Utility Conventions](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html)
- [GNU Coding Standards](https://www.gnu.org/prep/standards/html_node/Command_002dLine-Interfaces.html)
- [Command Line Interface Guidelines (clig.dev)](https://clig.dev/)
- [12 Factor CLI Apps](https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46)
- [NO_COLOR standard](https://no-color.org/)
- [FORCE_COLOR standard](https://force-color.org/)
- [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir/latest/)
- [BSD sysexits.h](https://man.freebsd.org/cgi/man.cgi?query=sysexits)
- [Keep a Changelog](https://keepachangelog.com/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Agent Skills specification](https://agentskills.io/specification)

## Privacy

This plugin consists entirely of static Markdown files. It does not collect,
transmit, or store any user data. It does not make network requests. It does
not include telemetry. No personal information is accessed or processed.

## License

MIT
