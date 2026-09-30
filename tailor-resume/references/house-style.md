# House style for resume variants and letters

## Resume skeleton

Pandoc reads these as markdown; the leading HTML block sets document
metadata for the docx and PDF.

```markdown
<title>La Monte Henry Piggy Yarroll — <Target Title></title>
<meta content="L.H. Piggy Yarroll" name="author">
<meta content="YYYY-MM-DD" name="date">
<meta content="text/html; charset=UTF-8" http-equiv="content-type">

Piggy Yarroll
============================

<Target Title> — <two or three qualifiers separated by · >

3633 Ashland Drive, Bethel Park, PA 15102-1407 | [1.412.726.6619](tel:14127266619) | [<piggy.yarroll+resume@gmail.com>](mailto:piggy.yarroll+resume@gmail.com) | [linkedin.com/in/piggy](https://www.linkedin.com/in/piggy)

### Summary
### <Optional highlights block>
### Experience
#### <Employer> — <Role>
**<Mon YYYY> – <Mon YYYY>.**
  * bullet
### Core Competencies
### Education
### Teaching
### Selected Publications
### Patents and Protective Publications
### Certifications
### Open Source & Community
### Note on Preparation
```

Sections are omitted when they do not serve the target. Industry
resumes drop publications; research resumes keep them.

## Conventions

- **Employer headings** are `####`, dates bold on their own line.
- **Bullets** are two-space indented `  * `, wrapped near 72 columns.
  Every bullet carries its result: past tense for the action, gerund for
  the result. Up to two sentences is acceptable.
- **Bold the noun the reader is scanning for** inside a bullet, not the
  whole clause — `**LKSCTP:**`, `**HIPAA was a core design
  constraint**`.
- **Links** are inline markdown, used for anything verifiable: RFCs,
  repos, project pages, certificates.
- **Roles spanning several titles** collapse into one heading with the
  full date range, and the titles listed — `Manager, OS & Platform Team
  / Lead Engineer`.
- **Older work** compresses into a single `#### Earlier` entry with one
  bullet per employer once it stops earning full treatment. Fifteen
  years is the usual cutoff, but keep anything exceptionally relevant
  and give it its date.
- **`La&nbsp;Monte`** in patent author lists, to stop the name breaking
  across lines.
- **Note on Preparation** closes every variant, unchanged:

  > *Drafted with Claude Opus 5 from hand selected source material.
  > Output hand reviewed and verified. Remaining errors are my own and
  > not the fault of my tooling.*

  Update the model name to whichever model actually drafted it.

## Letter skeleton

Letters live in `cover_letters/` and are auto-discovered by the
Makefile. Same metadata block, then a contact line, the date, a
salutation, and bolded lead-ins on each substantive paragraph so a
skimming reader gets the argument from the bold text alone.

A **forwardable note** — for an unadvertised role reached through a
friend — is addressed to the friend but written so every paragraph is
safe for management to read, and says so in the first paragraph. That
constraint is the whole point: it keeps the note free of anything
awkward, so the referrer can forward it without editing.

A note or letter for a specific reader closes with the local angle if
there is one (same metro area, mutual contact, prior collaboration).

## Fitting a letter on one page

A letter someone must forward, or a hiring manager must read before a
meeting, earns its keep at one page. Add a YAML metadata block above the
HTML block — pandoc reads it and the LaTeX template honours it:

```yaml
---
geometry: margin=0.9in
fontsize: 11pt
pagestyle: empty
---
```

`pagestyle: empty` drops the page number, which a one-page letter should
not carry anyway. With those settings roughly 590 words of body text
fills the page.

Measure rather than guess, because the last line spilling is invisible
in the markdown:

```bash
pdfinfo output/cover_letters/<name>.pdf | grep -i Pages
pdftotext -f 2 -l 2 output/cover_letters/<name>.pdf - | sed '/^$/d'
```

If page two holds only the signature, trim two or three lines or nudge
the margin; do not cut an argument for the sake of one line.

Compressing a long letter is an argument-selection problem, not a
word-trimming one. Pick the single thesis the reader must accept, keep
only paragraphs that advance it, and let each surviving paragraph do
double duty — the method-weight paragraph can carry the regulated-domain
answer, since criticality is what connects them. Gap responses stay in
whatever the length: they are the credibility of everything else. Keep
the long version in git history for talking points.

## Pandoc pitfalls

- The PDF path is LaTeX and rejects unicode with no LaTeX setup. `↔`
  breaks the build. `—`, `–`, `·`, and `→` in existing variants have
  rendered fine.
- `-f markdown-implicit_figures` is already in the Makefile so a
  standalone image does not become a numbered figure.
- Always render both `.pdf` and `.docx`. Employers ask for either, and
  only the PDF path fails loudly.
