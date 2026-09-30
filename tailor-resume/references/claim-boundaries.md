# Claim boundaries

Facts established in conversation that are **not** recoverable from the
repo, and the standing cautions that follow from them. Verify anything
here against the current resume files before relying on it, and add to
it whenever a conversation settles a new boundary.

## Established facts

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

## Standing gaps — name them, never paper over them

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

## Terms to avoid

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

## Self-characterizations to flag

When a letter needs a sentence about what he is like — "sitting down
with domain professionals before there is a design to defend is a part
of this job I am comfortable in" — that is the drafter's
characterization, not his. Write it if it serves the argument, then flag
it explicitly in the handover so he can cut it. He is the only one who
can vouch for claims about his own disposition.
