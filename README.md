# claude_skills

Claude skills I use, one self-contained file each.

Every skill in this repository is a single markdown file: YAML
frontmatter naming the skill and describing when it should trigger,
followed by the instructions themselves. Nothing is split across
supporting files, so a skill can be appended to an existing SKILLS file,
dropped in as a `SKILL.md`, or simply read.

## Skills

| Skill | What it does | Triggers on |
|---|---|---|
| [tailor-resume](tailor-resume.md) | Tailors a resume variant and cover letter for a specific opportunity, then renders them with pandoc, records them in the application trackers, and commits. Carries the drafting judgment as well as the mechanics: ask for the underlying fact instead of inferring a claim from the job description, emphasize why an experience mattered rather than that it happened, name gaps openly and offer the nearest true analogue, and never use a term you cannot verify. Includes the house style for resumes and letters, a recipe for fitting a letter on one page, and a standing record of what the resume record does and does not support. | A job lead, a posting, a referral, a friend hiring, "another resume", a cover letter, a note to a referrer, or a revision to an existing variant. |

## Installing a skill

As a personal skill, available in every session:

```bash
mkdir -p ~/.claude/skills/tailor-resume
cp tailor-resume.md ~/.claude/skills/tailor-resume/SKILL.md
```

As a project skill, scoped to one repository, from inside that
repository:

```bash
mkdir -p .claude/skills/tailor-resume
cp /path/to/claude_skills/tailor-resume.md .claude/skills/tailor-resume/SKILL.md
```

Or append it to a file that collects skills:

```bash
cat tailor-resume.md >> ~/SKILLS.md
```

Claude Code discovers a personal skill at
`~/.claude/skills/<name>/SKILL.md` and a project skill at
`.claude/skills/<name>/SKILL.md`, so the directory name should match the
`name:` field in the frontmatter.

## Adding a skill

One file per skill, named for the skill, at the top level. Keep it
self-contained — if a skill grows large enough to want separate
reference files, inline them as `##` sections rather than splitting,
since a single file is what makes these appendable. Add a row to the
table above.

The frontmatter needs `name` and `description`. The description is the
only thing Claude sees when deciding whether to consult the skill, so it
should say both what the skill does and the situations that should
summon it, in concrete terms.

## A note on specificity

These are working skills rather than templates. `tailor-resume` names my
own repository paths, my own contact details, and a frank record of the
gaps in my own resume, because that specificity is what makes it useful
to me. Anyone else adopting it should expect to replace the paths, the
house style, and the claim boundaries with their own.

## License

GNU Affero General Public License v3 — see [LICENSE](LICENSE).
