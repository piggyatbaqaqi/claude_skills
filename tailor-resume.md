---
name: tailor-resume
description: Tailor a resume variant and cover letter for a specific job, opportunity, or referral in the /data/piggy/lab/resume repo, then render, track, and commit them. Use this whenever the operator mentions a job lead, a position, a company that is hiring, a friend who wants to bring them onto a team, a posting they want to apply to, "another resume", a cover letter, or a note to a referrer — and also when they want an existing variant revised, a claim corrected, or a gap handled honestly. Use it even when the opportunity is vague, unadvertised, or described only in conversation, because the tailoring decisions and the accumulated claim boundaries live here rather than in the repo.
---

# Tailoring a resume variant

Resume work lives in `/data/piggy/lab/resume` — its own git repo, usually
not the directory the session opened in. Everything below happens there.

Each new opportunity gets its own `resume_<angle>.md` rather than an edit
to an existing one. The variants are a portfolio, not a history: an old
variant stays valid for the job it was written for, and the operator may
send it again.

## Before drafting: read, then ask

Read three files to load the material and the voice:

1. `resume.md` — the base, terse and complete.
2. `resume_research_programmer.md` — the longest and most detailed
   variant; the fullest inventory of bullets with their results attached.
3. The most recently modified tailored variant — the current house style.

Then read **House style** below for the document skeleton and **Claim
boundaries** for what is and is not claimable. The second matters most:
it records facts established in past conversations that are nowhere in
the resume repo, including standing gaps.

Now ask the operator, in one batched round, only the questions whose
answers change the work:

- **Which angle leads?** Offer two or three real framings with their
  tradeoffs, and recommend one. This is the highest-leverage question and
  it cannot be answered from the posting.
- **Any experience the repo does not record?** Name the specific
  adjacency the target wants. Do not ask "anything else to add?" — ask
  "were you involved in X?", because that is answerable.
- **Deliverable scope** — resume only, resume plus a forwardable note,
  resume plus a conventional cover letter.

Anything the posting or the operator already settles is not a question.

## The rule that matters most

**Ask for the underlying fact rather than inferring a claim from the job
description.** The plausible guess is usually wrong in a way that is
discovered in the interview, and the true, narrower fact is usually the
more distinctive one. When asked about clinical exposure, the operator's
real answer — HIPAA was a core design constraint on the distributed ML
algorithms, so providers exchange models rather than patient records —
was far stronger than the "healthcare ML exposure" a job description
would have invited.

Two corollaries the operator has had to apply by hand, so apply them
from the start:

- **Emphasize why an experience mattered, not that it happened.** Being
  invited into early collaboration meetings is a weak bullet. Being
  invited *because of an architectural background* is third-party
  corroboration of the exact thing the resume claims. Ask what the fact
  is evidence *of*.
- **Do not name what you cannot verify.** A methodology name you cannot
  place, a product domain you do not actually understand, a taxonomy you
  might mis-map onto (Cockburn's Crystal colors are graded by team size
  *and* criticality — reference the family and the grid rather than
  guessing a color). Leave it out and say you left it out. A confident
  wrong term in front of a hiring manager costs more than the precision
  would have bought.

## Name gaps openly

When the target wants something genuinely absent, say so plainly in the
letter and offer the nearest true analogue. This reads as confidence and
it survives the interview. Worked examples:

- No Qt experience → deep and long C++ (a compiler back end, threaded
  packet classifiers, a platform build system, kernel work), and a UI
  framework framed as an API to learn rather than a competency claimed.
- No shipped regulated medical device → years of IETF standards work
  (SIGTRAN, TSVWG, RSERPOOL; the SCTP sockets-API Internet Draft; the
  RFC 2960 state-analysis acknowledgement) *plus* the implementation
  judged against that specification, and CGL 2.0 as the institutional
  analogue — editor of the registration requirements, then coordinator
  of the first registration ever completed.

The analogue works because it is the same *shape* of work, and saying
which standard was not done ("none of that is IEC 62304") is what makes
the rest credible.

## Drafting

Follow **House style** below. Two structural choices worth making
deliberately:

- **A highlights block** between the summary and Experience, when the
  resume will be handed to someone who must argue for the candidate.
  The operator's own notes record that top lines carry the most value,
  and a referrer needs something scannable to forward upward.
- **Ordering Experience by relevance, not strictly by date.** Lead with
  whatever the target actually buys.

Every bullet carries its result — what changed because the work
happened. Past tense for the action, gerund for the result. That is the
operator's standing instruction from a resume consultant.

Cut bullets that belong to a different narrative even when they are
good. An outage root-cause reads as SRE work and weakens an architect
resume.

## Mechanics

```bash
cd /data/piggy/lab/resume
# 1. write resume_<angle>.md, and the letter in cover_letters/
# 2. append the basename to RESUMES in the Makefile (letters auto-discover)
# 3. render
make output/resume_<angle>.pdf output/resume_<angle>.docx
```

Rendering goes through pandoc to LaTeX, which rejects unicode it has no
setup for — `↔` breaks the PDF build. Em dashes and `–` are fine because
existing variants already use them. Always render before committing; a
broken PDF is not discovered any other way.

`output/` and `*~` are gitignored, so only markdown, the Makefile, and
the trackers get committed.

## Record and commit

Both trackers, every time:

- `applications.md` — a per-employer section with a table. Include the
  resume and letter filenames, and the status with its reasoning.
- `notes.txt` — a dated entry describing the opportunity, the angle
  chosen, the gaps named, and the exact boundary of any claim that
  required asking. Future sessions reconstruct the reasoning from here.

If the repo has unrelated uncommitted changes when you arrive — the
operator logs job statuses by hand — commit those separately first, with
their own message, so the application material lands in a clean commit.

Commit messages explain the tailoring decisions, not just the file list:
which angle was chosen and why, what was claimed and on what basis, what
was deliberately left out.

## Report the disposition

The operator requires the disposition of every finding: what was
recorded, where (file and section), and the commit. A git hash alone is
not a disposition. Cover everything in the response, and name what you
chose *not* to record with the rationale — unverifiable terms, claims
too thin for paper, standards you introduced on your own initiative.

The resume and the letter are written for the hiring reader, not for the
operator, so open the handover with one short line naming that audience.

## When updating an existing variant

A correction to a claim usually needs fixing in more than one place: the
highlights block, the Experience entry, the Core Competencies line, the
letter, and the `notes.txt` record of what is being claimed. Grep for
the phrase before assuming one edit covers it. Then re-render and commit
the correction on its own.

---

## House style

### Resume skeleton

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

### Conventions

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

### Letter skeleton

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

### Fitting a letter on one page

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

### Pandoc pitfalls

- The PDF path is LaTeX and rejects unicode with no LaTeX setup. `↔`
  breaks the build. `—`, `–`, `·`, and `→` in existing variants have
  rendered fine.
- `-f markdown-implicit_figures` is already in the Makefile so a
  standalone image does not become a numbered figure.
- Always render both `.pdf` and `.docx`. Employers ask for either, and
  only the PDF path fails loudly.

---

## Claim boundaries

Facts established in conversation that are **not** recoverable from the
repo, and the standing cautions that follow from them. Verify anything
here against the current resume files before relying on it, and add to
it whenever a conversation settles a new boundary.

### Established facts

**Auton Lab clinical exposure.** HIPAA was a core design constraint on
the CMU distributed-AI project: the algorithms exchange *models* rather
than patient records, so several healthcare providers can build one
shared model without sharing patient data. Separately — and this is a
different thing — the lab invited him into early collaboration meetings
with healthcare professionals approaching the Auton Lab about
prospective projects. Those meetings concerned **work of a similar
kind, not that project**, and the point worth emphasizing is that the
invitation came *because of his architectural background*. He was a
spectator on clinical projects via the weekly lecture series, which is
too thin to put on paper. No clinical modeling, ever.

**Human factors and UX.** No Qt, no desktop GUI framework. He built the
SKOL front end in React as the applied UX component of his master's. The
concluding independent study included a full section on human factors:
Don Norman (*The Design of Everyday Things*), David Marr (*Vision*),
Andrew Csinger (*The Psychology of Visualization*), Martin Sarter
(attention and memory). He wrote an annotated bibliography from that
reading and offers it on request — its existence as a file has not been
confirmed, so check before promising it again. He is comfortable in the
vocabulary, e.g. affordances versus signifiers.

**Standards and conformance.** The strongest analogue for regulated
development, and he wants both halves of it foregrounded: years in the
IETF (SIGTRAN, TSVWG, RSERPOOL) as early coauthor of the SCTP
sockets-API Internet Draft, the first complete state analysis of SCTP
acknowledged in RFC 2960, and then LKSCTP as the implementation judged
against that specification — specifying precisely enough for strangers
to interoperate, then proving conformance. CGL 2.0 is the institutional
analogue: editor of the registration requirements, then coordinator of
the first registration ever completed.

### Standing gaps — name them, never paper over them

- **No Qt.** C++ depth is the answer; a UI framework is an API to learn.
- **No life-critical project, ever.** This is the honest formulation; he
  says it plainly rather than hedging. IETF plus CGL 2.0 is the analogue
  for working under a formal specification and proving conformance, and
  naming what he has *not* worked to is what makes the analogue
  credible.

  For medical device software he is willing to learn and work within
  **IEC 62304** and **AAMI TIR45**, while stating he is not deeply
  familiar with either. TIR45 is the strong card: it exists because
  Agile practice and a rigorous lifecycle are compatible, so the
  practices it asks you to document — Fagan inspections, TDD, pair
  programming — are ones he already has, which turns his Agile
  credential into a regulated-development asset rather than something to
  reconcile. Note that IEC 62304 grades software by safety class, and an
  automated contrast injector is class C.

  Keep **"safety-critical"** out of competency headings unless the work
  genuinely was. Carrier-class telecom and DoD programs are
  high-reliability or high-availability; calling them safety-critical
  contradicts the honest statement above. Use "high-reliability".

### Terms to avoid

- **"Grizzly Agile"** — the operator has used this phrase; it could not
  be verified as a named methodology. Keep it out of anything a hiring
  manager reads until he confirms what it is.
- **Crystal color names** — Cockburn's grid is graded by team size *and*
  criticality. Reference the family and the grid rather than asserting
  Yellow, Orange, or Sapphire for a given team; a reader who knows the
  grid will catch a mis-mapping.
- **Unfamiliar product domains** — he described a target's field as
  "automated contrast ingestion" and the term was not confidently
  understood, so it stayed out of both documents entirely. Silence beats
  a wrong-domain claim. Ask him what the field actually is.

### Self-characterizations to flag

When a letter needs a sentence about what he is like — "sitting down
with domain professionals before there is a design to defend is a part
of this job I am comfortable in" — that is the drafter's
characterization, not his. Write it if it serves the argument, then flag
it explicitly in the handover so he can cut it. He is the only one who
can vouch for claims about his own disposition.
