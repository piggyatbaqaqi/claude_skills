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

Then read `references/house-style.md` for the document skeleton and
`references/claim-boundaries.md` for what is and is not claimable. The
second one matters most: it records facts established in past
conversations that are nowhere in the resume repo, including standing
gaps.

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

Follow `references/house-style.md`. Two structural choices worth making
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

## Reference files

- `references/house-style.md` — document skeletons, formatting
  conventions, the one-page letter recipe, and pandoc pitfalls. Read
  before drafting.
- `references/claim-boundaries.md` — the standing inventory of what the
  record supports, the known gaps, and the terms to avoid. Read before
  drafting, and update it whenever a conversation establishes a new fact
  or boundary.
