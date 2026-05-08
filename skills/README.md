# AAIF Public Agent Skills

This repository contains public Agent Skills for AAIF.

Agent Skills are portable bundles of instructions, references, scripts, and assets that help AI agents perform specialized tasks. A skill gives an agent reusable expertise for a specific domain, workflow, brand, tool, or process.

## Repository Structure

Each skill lives in its own directory.

```text
skills/
├── a-skill/
│   ├── SKILL.md
│   └── assets/
├── another-skill/
│   └── SKILL.md
└── README.md
```

Every skill directory contains a `SKILL.md` file with metadata and instructions. Some skills may also include supporting files such as:

- `assets/` — images, logos, templates, or other static resources
- `references/` — longer documentation or reference material
- `scripts/` — executable helper scripts

## Installing and Updating Skills

You can install individual skills from this repository using the [Skills CLI](https://skills.sh/docs/cli).

To install the CLI:

```bash
npx skills
```

To install a skill globally so it is available to all compatible agents:

```bash
npx skills add aaif/public-agents --skill aaif-brand-guidelines --global
```

To list available skills in this repository:

```bash
npx skills add aaif/public-agents --list
```

To install all skills from this repository:

```bash
npx skills add aaif/public-agents --all
```

To update a specific skill:

```bash
npx skills update aaif-brand-guidelines
```

## Using Skills

All major AI agents (goose, claude code, codex, gemini, etc.) support agent skills and load them on demand based on context.

For example, a prompt like this will trigger the agent to load the `aaif-brand-guidelines` skill if it's installed:

> make a flyer for XYZ event using the AAIF brand guidelines

You can also explicitly ask:

> use the AAIF brand guidelines skill to create a flyer for XYZ event

## Skill Format

Skills follow the [Agent Skills specification](https://agentskills.io/specification.md).

At minimum, each skill must include:

```text
skill-name/
└── SKILL.md
```

The `SKILL.md` file contains YAML frontmatter followed by Markdown instructions.
