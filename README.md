# claude_skills

Claude skills I use, one directory each.

A skill is a directory containing `SKILL.md` — YAML frontmatter naming
the skill and describing when it should trigger, followed by the
instructions — plus optional supporting files. Supporting material lives
in `references/`, which `SKILL.md` points at rather than including,
because a skill's `SKILL.md` is loaded into context whenever the skill
triggers while a reference file is read only when it is actually needed.
Keeping the detail in `references/` is what lets a skill carry a lot of
material without paying for all of it on every invocation.

## Skills

| Skill | What it does | Triggers on |
|---|---|---|
| [tailor-resume](tailor-resume/) | Tailors a resume variant and cover letter for a specific opportunity, then renders them with pandoc, records them in the application trackers, and commits. Carries the drafting judgment as well as the mechanics: ask for the underlying fact instead of inferring a claim from the job description, emphasize why an experience mattered rather than that it happened, name gaps openly and offer the nearest true analogue, and never use a term you cannot verify. Its references hold the house style for resumes and letters, a recipe for fitting a letter on one page, and a standing record of what the resume record does and does not support. | A job lead, a posting, a referral, a friend hiring, "another resume", a cover letter, a note to a referrer, or a revision to an existing variant. |

## Installing a skill

As a personal skill, available in every session:

```bash
cp -r tailor-resume ~/.claude/skills/
```

As a project skill, scoped to one repository, from inside that
repository:

```bash
mkdir -p .claude/skills
cp -r /path/to/claude_skills/tailor-resume .claude/skills/
```

Claude Code discovers personal skills under `~/.claude/skills/` and
project skills under `.claude/skills/`, so the directory name should
match the `name:` field in the frontmatter.

## Adding a skill

One directory per skill, named for the skill:

```
skill-name/
├── SKILL.md          # frontmatter + instructions
└── references/       # optional, read on demand
    └── topic.md
```

Keep `SKILL.md` to the procedure and the judgment behind it — a few
hundred lines — and push detail, tables, and long examples into
`references/`, naming each one in `SKILL.md` along with when to read it.
A reference file over a few hundred lines wants a table of contents.

The frontmatter needs `name` and `description`. The description is the
only thing Claude sees when deciding whether to consult the skill, so it
should say both what the skill does and the situations that should summon
it, in concrete terms. Then add a row to the table above.

## A note on specificity

These are working skills rather than templates. `tailor-resume` names my
own repository paths, my own contact details, and a frank record of the
gaps in my own resume, because that specificity is what makes it useful
to me. Anyone else adopting it should expect to replace the paths, the
house style, and the claim boundaries with their own.

## License

GNU Affero General Public License v3 — see [LICENSE](LICENSE).
