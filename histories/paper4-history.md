# Process history — Paper 4 (conditioned): "The price of a post-selected signal"

Sources: session record 2026-07-11/12 (direct), notes.md entries, git
history, research/t1_literature_triage.md. All events below occurred
within roughly one working day and are commit-anchored.

## Timeline

**2026-07-11 (late evening) — literature triage.**
- Agent dispatched: T1 literature triage (post-selection no-gos,
  steering, postselected metrology, PT no-signaling resolutions).
  VERDICT: not preempted. The exact trade-off (conditioned
  distinguishability vs survival probability) unposed anywhere; the
  steering literature has the constraint but never the optimization;
  Fisher-information trade-offs don't imply TV bounds. Toolkit
  identified (HJW, SDP duality, Hilbert/Thompson metrics, SLOCC).
  Caution flagged by the agent itself: check the naive LP bound
  before claiming extremality.

**Scoping insight (minutes later, main session).** With arbitrary
filters the static trade-off is TRIVIAL (orthogonal filters give
TV = 1 at any p <= 1/2) — so the content had to be dynamical. This
reframing happened BEFORE any theorem was conjectured and shaped
everything after.

**Numerical discovery (same hour).** Region sweep script
(`t1_region_sweep.py` v1): candidate bound TV <= sqrt(1-(|detC|/p)^2)
tested; the FIRST version of the bound coded was the WEAK form
(sqrt(1-(detM/p)^2)) — an algebra slip caught within the hour when
the dimer's "gap" of 0.414 contradicted the saturation hypothesis;
the corrected tight form then saturated to 1e-15. **Error 3.1**
(algebra slip; caught by: numerics contradicting an expected
saturation).

**Same run — object confusion caught.** The sweep's TV(25) = 1.000
contradicted the paper-2 closed form kappa-tilde/sin(theta): resolved
as two different observables (quantum trace distance vs
configuration-basis TV). Not an error in any document, but a
near-miss that would have become one; became the Pythagorean-
decomposition insight instead. **Miss-averted 3.2.**

**Theorem established numerically (same evening).** Dimer saturation
pointwise to 1e-15 at all times/phases; 0/99,846 random violations;
classical TV = kappa-tilde/sin(theta) recovered to 6 digits.

**2026-07-12 (early) — draft v0.1** (7 pp) written and compiled;
explicitly labeled pre-audit; RLW journal details deliberately left
at arXiv-level pending verification.

**Audit cycle (three agents, same day).**
- BIBLIOGRAPHY: 14/15 clean. One required fix (RLW = IEEE TIT 70,
  3453 (2024), restored by direct web verification — overriding the
  abstract-level triage record); Bhatia pointer sharpened to
  Thm III.4.1; Hubner attribution CONFIRMED correct.
- INDEPENDENT CALC: all seven claims PASS from scratch (including
  first-principles reconstruction of the conditioned state with
  multi-Kraus decompositions, sympy proof of the dimer Bloch form,
  Haar-random relabelings at d=3-5). **It caught a code-vs-text
  factor-2 mismatch (Error 3.3): the script tested a STRONGER bound
  than the manuscript stated.** Resolution: the stronger (factor-4)
  bound is provable (one added rearrangement+AM-GM line) and reduces
  EXACTLY to the sharp Bell bound — the audit UPGRADED Prop 5.1.
- ADVERSARIAL: 0 critical, 4 major, 12 minor. Major items: (i)
  purification bookkeeping wrong for arbitrary pure states (repaired
  by polar-decomposition wlog); (ii+iii) the factor-2/coverage
  issues above (numerics extended to fully independent message
  pairs); (iv) **"the deficit is exactly the conditioned coherence"
  was FALSE as stated (Error 3.4)** — replaced by the exact result
  it gestured at: the Pythagorean decomposition TV^2 = TV_cl^2 +
  chi^2 (verified 4.4e-16), a strictly better statement than the
  error. Minors included a trial-count arithmetic error (1.6e5 ->
  1.8e5), a citation-history flattening (Tang located the signal;
  Brody/Ju restored consistency), and notation collisions.

**Refuted conjecture (kept in the paper).** The Bell state is NOT
extremal at fixed invariants — counterexamples exceed the Bell
envelope by up to 0.81. Recorded in the manuscript as a numerically
established negative per program policy.

**Post-audit preemption check (same day).** The triage had flagged
Reeb-Kastoryano-Wolf 1102.5170 as the closest textual overlap,
verified only at abstract level. A dedicated full-text read found
**PARTIAL OVERLAP (Miss 3.5, caught before circulation):** the core
inequality is assemblable in three lines from their published
Cor. 15 (our RHS = tanh[h(M,1)/2] in Hilbert's projective metric),
and a one-line elementary Bloch proof also exists. NOT in RKW: any
statement trading distinguishability against survival probability,
the steering setup, the invariant, the saturation analysis, or the
decomposition. Repositioned in v0.3 with a dedicated remark stating
the debt precisely; "never answered" softened to "never posed as
such." A referee fluent in that literature would have found this;
the process found it first because the triage explicitly flagged
what it had NOT verified.

## Errors & misses ledger

| # | What | Introduced by | Caught by | Fate |
|---|---|---|---|---|
| 3.1 | weak form of the bound coded | algebra slip | numerics vs saturation hypothesis (same hour) | corrected; tight bound saturates 1e-15 |
| 3.2 | quantum-vs-classical TV conflation (near-miss) | object ambiguity | closed-form mismatch noticed same run | became the Pythagorean corollary |
| 3.3 | manuscript factor-2 weaker than code | drafting | independent calc agent | Prop UPGRADED (factor 4, exact Bell interpolation) |
| 3.4 | "deficit = exactly the coherence" false sentence | overreach in prose | adversarial agent | replaced by exact quadrature corollary |
| 3.5 | RKW derivability unnoticed at drafting | abstract-level triage | dedicated full-text read (pre-circulation) | honest repositioning remark, v0.3 |
| — | refuted conjecture: Bell extremality | plausible guess | 40k-draw sweep | reported as negative in the paper |

## Process events (high level)

prior-art search: 2 (triage; RKW deep read). adversarial review: 1
(three-agent cycle). independent recomputation: 1 (all claims, from
scratch). controls: every script prints inline controls; two of the
five ledger items were caught by numerics disagreeing with
expectations. human steering: commissioned the work, ordered the
audit cycle, read-through pending. Status at write-up: v0.3,
audit-clean, awaiting author read-through.

---

## 2026-07-13 — GATE PASS 1 (first fresh-eyes gate audit; Opus x3)

First release-gate audit of paper 3 (previously development-clean at
v0.3). Fresh-eyes Opus x3 (claims / biblio / numerics); no
histories/notes; numerics given absolute output paths + the standalone-
only constraint (no full stiff/sweep runs); biblio given raw-Crossref
instructions. Enters the gate at counter 0 in all three lanes.

**Claims — NOT CLEAN (2 NIT; 1 applied, 1 held).** Full line-by-line
re-derivation of every theorem/prop/corollary + the dimer computation.
Thm 3.1 "equality iff n_x=0" airtight both directions; dimer eq. (7)
re-derived from scratch (n_x=0 in both phases and at the EP); the
fidelity bound (Prop 4.4) and general-d Lidskii bound (Prop 4.5) reduce
exactly to the main bound at d=2 / Bell; Fuchs-van de Graaf, Hubner
qubit-fidelity, and Bhatia/Lidskii citations all verified against
primary sources. No false converses / overclaims / scope errors /
saturation-condition errors / dimensional slips.
  NIT-1 (APPLIED) Prop 4.4 proof :384-389: after the relabeling
    M_i -> U M_i^T U^dagger, the conditioned states were still written
    sqrt(rho_B) M_i^T sqrt(rho_B); stray/duplicated transpose. Purely
    notational (det M_i, det rho_B, p_i all transpose/conjugation-
    invariant; result unaffected). FIX: introduced \tilde M_i :=
    U M_i^T U^dagger explicitly and dropped the extra transpose.
  NIT-2 (HELD) Remark 3.4 :254-258: the exact RKW Cor. 15 constant
    (TV <= tanh[h/4]) could not be machine-verified from the binary
    PDF; the two load-bearing steps (RHS = tanh[h(M,1)/2];
    h(sig1,sig2) <= 2 h(M,1)) were re-derived independently and are
    correct, and the remark is heavily hedged ("can be assembled
    from"). Left as an author-confirm item; no edit.

**Numerics — NOT CLEAN (1 MINOR applied, 1 NIT no-action).** Every
quoted number reproduced (saturation residuals 1.28e-15 broken /
3.68e-13 unbroken; classical asymptote kappa/sin theta; d=3,4 zero-
violation with margins; the 0.807 Bell-non-extremality negative; the
~1.8e5 = 181,306 violation-search subtotal arithmetic, correctly
excluding the T-D envelope map). Reduced-trial reruns for the 10^5-
class searches per the standalone constraint; zero violations in all.
  MINOR (APPLIED) scripts/t1_region_sweep.py:19 docstring stated the
    central theorem with a wrong exponent, sqrt(1-(|det C|^2/p)^2)
    instead of sqrt(1-(|det C|/p)^2) (= paper eq:main since
    sqrt(det M)=|det C|). The bound() code itself is correct; only the
    header comment on the advertised reproduction script was wrong.
    FIX: corrected the docstring exponent.
  NIT (no action) scripts/t3_cosi_forecast.py is an orphan (phantom-
    decay/COSI MeV cosmology, unrelated to this paper) physically
    colocated here; Code availability correctly cites only
    t1_region_sweep.py and assemble_repos.ps1 ships only that. Parked
    research artifact, not a paper-3 script -> no fix (housekeeping).

**Bibliography — CLEAN.** 13 external items all verified against
primary publisher/Crossref records (LHFL2014, Tang2016, Brody2016,
Ju2019, CFJC2014, AS2020, RKW2011, RLW2022, Gisin1996, Hubner,
FvdG1999, Bhatia, Ehrhardt2022) on authors/title/journal/vol/page/year;
the RLW2022 key(2022)/printed-year(2024) split is correct (key = arXiv
submission year, printed = publication year). Companion/Companion2
self-refs internally consistent. No chimeras / wrong authors / title
drift / vol-page-year errors. In-text claim spot-checks all supported.

Recompiled clean (8 pp); log shows no errors, no undefined
refs/citations. No auditor leads rejected (NIT-2 and the orphan are
held/no-action, not refuted). Not CRITICAL/MAJOR and no prior-fix
reversal -> nothing for major-findings-ledger.md.

**Counter move (first gate pass):** claims applied a finding -> stays
0; numerics applied a finding -> stays 0; biblio CLEAN -> +1. After
pass 1: **claims 0/4, biblio 1/3, numerics 0/3.**


## SESSION 2026-07-18/19 (numbering unification + claim-support)
- Folder paper3/ -> paper4/ (series 4); cite keys -> codenames; release-gate leak removed.
- Claim-support (Opus): CLEAN; all load-bearing attributions SUPPORTED (incl. the RKW tanh(h/4) bound, LHFL signaling, Tang/Brody/Ju consistency, Lidskii/Bhatia, Gisin hidden nonlocality). RKW "Cor.~15" -> "Prop.~7 (in the arXiv version)" -- the bound is genuinely RKW's; the "Cor.15" journal label was never confirmed, "Prop.7" is the verified arXiv-version label.

## OPUS 4-PAPER WAVE 2026-07-19 (out-of-rotation audit; claims + numerics + biblio) -- CLEAN
- **Claims: SOUND, zero CRITICAL/MAJOR/MINOR.** Every load-bearing result re-derived from scratch: the steering identity; Thm 3.1 main trade-off TV≤√(1−detM/p²) (BOTH routes -- variational AND Hilbert-metric tanh[h/2] -- agree exactly, a strong cross-check); Rem 3.2 invariant √detM=|detC|; Cor 4.2 Pythagorean decomposition; the κ̃/sinθ asymptote; Prop 5.1 fidelity bound (reduces to Bell exactly); Prop 5.2 general-d Lidskii majorization. Hypothesis-sufficiency specifically hunted -- none missing (each restriction stated explicitly). Only 2 notation NITs (DEFERRED to a notation micro-pass, "no derivation affected" per auditor): h collision (Hilbert metric h(·,·) vs dimer scalar h=sinh(κ̃t)/κ̃); μ reuse (eigenvalues of M in Thm 3.1 vs eigenvalues of σ₂ in the Prop 5.1 proof).
- **Numerics: CLEAN.** Every quantitative claim reproduces from t1_region_sweep.py (seeded/deterministic): ~1.8e5 randomized violation searches, 0 violations; all saturation residuals (1.3e-15, 4e-13), the κ̃/sinθ asymptotes, the Pythagorean identity 4.4e-16, general-d margins -- all match; manuscript rounding honest. Analytic re-derivations confirm to machine precision.
- **Biblio: 13/13 CLEAN.** All external metadata + claim-support verified (LHFL2014, Tang2016, RKW2011 Prop-7 attribution confirmed vs ar5iv, FvdG/Hübner formulas, Ehrhardt2022, etc.). No corrections.
- HOUSEKEEPING (flagged for user decision, not a p4 defect): `paper4/scripts/t3_cosi_forecast.py` is ORPHANED -- a phantom-decay/COSI MeV forecast (Λ≤18.8 MeV, dipole) with NO claim anywhere in paper4 (Code-availability correctly lists only t1_region_sweep.py). Likely belongs to the p3 instantaneous / p5 choosing line (vacuum decay / dipole). Move or confirm home; runs clean on its own.
- No manuscript edits this wave (paper CLEAN; NITs deferred). Both gates PASS.

## NOTATION MICRO-PASS 2026-07-19 (deferred NITs resolved)
- Hilbert projective metric h(.,.) -> d_H (Rem 3.3, always function-form); the dimer scalar h=sinh(kt)/k untouched. sigma_2 eigenvalues mu_i -> nu_i in the Prop 5.1 fidelity proof; the M-eigenvalues mu_1,mu_2 untouched. Recompiled 8pp, 0 undefined.

## t3 ORPHAN RESOLVED 2026-07-19
- `t3_cosi_forecast.py` was NOT paper4 material (confirmed: phantom-decay COSI forecast, no claim in conditioned). Traced via git + content + its sibling s4c_dipole_template.py to paper3 (instantaneous) Sec (b); MOVED to paper3/scripts/ and cited there. paper4/scripts/ now holds only t1_region_sweep.py (its sole, correctly-cited script).

## OPUS CLAIMS REVALIDATION 2026-07-20 (Wave B; 2nd Opus pass)
- **SOUND.** Every result re-derived from scratch again (steering identity, Thm 3.1 BOTH routes still agree exactly after the h->d_H rename, √detM=|detC|, Pythagoras, Prop 5.1 fidelity->Bell, Prop 5.2 Lidskii). The ν rename (σ₂ eigenvalues) consistent. **1 real NIT (fixed): a stale `$h$` at L253 survived this session's h->d_H notation micro-pass sibling sweep** ("probability-blind by construction (h mods out normalization)") -> $d_H$. Re-swept: no other stale Hilbert h (dimer h=sinh at L277 is a legitimately different object, correctly untouched). Recompiled 8pp, 0 undefined.

## OPUS DEEP CLAIMS 2026-07-20 (Wave E; Nth adversarial pass) -- CLEAN
- No math error. Variational + Hilbert-metric routes genuinely agree on the SAME bound (not one weaker); general-d Lidskii not sharpness-overclaimed (d>=3 non-sharpness needs no disclosure -- none made; bound is attainable by reversing-permutation G); fidelity Bell reduction exactly tight (mixed antipodal equal-spectrum -> every inequality simultaneously tight). RKW2011 Prop-7/Thm-21 eq-numbers flagged provisional -- ALREADY confirmed this session by the p4 biblio lane (ar5iv Prop 7). No change.

## OPUS DEEP CLAIMS 2026-07-20 (hunt-what-was-rationalized wave, p1-p4) -- SOUND, 1 NIT applied
- All four lanes re-verified SOUND (hypothesis-sufficiency: Thm 3.1, Prop 3.4, Prop 4.1, Prop 4.3 Lidskii all check; cross-ref drift: abstract<->body match, h/d_H + mu/nu disambiguation clean with no half-rename; defensible-not-derived and sign/inequality clean) -- consistent with this session's Waves B/E. Applied 1 NIT: abstract exp-notation "$\exp[-\!\int\!\Tr\Gamma\,dt/2]$" (ambiguous grouping, dropped limits) -> "$\exp[-\tfrac12\!\int_0^t\!\Tr\Gamma\,ds]$" matching the body form (L221).
- HELD/defensible (auditor-error-log 07-20): RKW2011 Prop.7/Thm.21 eq-numbers + tanh factor $1/4$ -- machine("ar5iv")-verified this session but per [[pdf-reads-provisional]] ar5iv is NOT a trusted read; needs published/arXiv-PDF confirmation before circulation (main proof Thm 3.1 does NOT depend on the Remark, so impact low). RLW2022 cite-key(2022)/journal-year(2024) mismatch = deliberate preprint-year key convention (NIT, no action).
- Recompiled 8pp, 0 undefined. Both gates PASS. No MAJOR.

## OPUS BIBLIO 2026-07-20 (Wave 5; web cross-check, machine-provisional) -- no manuscript change
- All 15 bibitems machine-match (authors/venue/vol/page/year/arXiv); no orphans; RLW2022 key/year deliberate. RKW \cite{RKW2011}: bibitem arXiv 1102.5170 CONFIRMED correct; Prop.7 + tanh 1/4 machine-cross-check OK (ar5iv shows ≤tanh 𝔥/4, underwrites TV≤tanh[d_H/4]); but "Thm.21 quantifies the success probabilities" MACHINE-AMBIGUOUS (ar5iv reads Thm 21 = "converse of Birkhoff" realizability iff, not clearly a success-probability formula) → HELD-BIBLIO, human-PDF check Thm 21 specifically (minor-ledger #42). Claim-support all machine-OK (Hübner, FvdG, Lidskii/Bhatia III.4.1, LHFL, Gisin). Machine reads PROVISIONAL per [[pdf-reads-provisional]].

## FABLE CLAIMS 2026-07-20 (cross-model wave p2/p4/p7) -- 1 MINOR + 3 NIT applied
- Fable re-derived the spine intact (Thm 3.1 equality-iff BOTH directions, Prop 4.1 Bell reduction, Prop 4.3 Lidskii, the kt/sinth asymptote, TV^2=TVcl^2+chi^2; cross-paper TV consistency with paper3 at finite t). Zero CRITICAL/MAJOR, zero false converses.
- Applied (#69,71): (MINOR) `\ref{sec:code}` renders "Sec. 7" (Discussion) since sec:code is a starred/unnumbered section -> "(see Code availability)". (NITs) abstract exp-notation given the (s) arg matching the body; stray comma after the URL deleted; "(projectors)" -> "(rank-deficient effects, e.g. projectors)" (a rank-1 projector forces p=1/2, too narrow for "any p<=1/2").
- HELD (#70): "dissipated weight" is sign-inverted -- sqrt(detM)/p is a SURVIVAL factor (=1 at no dissipation); used consistently 3x incl. the abstract "total-loss factor" -> flagged for a terminology pass (formulas correct). F6 (extremal "trajectory" family) held.
- Recompiled 8pp, 0 undefined. Both gates PASS. No MAJOR.

## HELD-ITEM CLEARED 2026-07-21 -- "dissipated weight" terminology
- minor-ledger #70 (Fable F2): unified the loose "dissipated weight" (L130 Pythagorean term, L231) to the paper's OWN defined term "total-loss factor" (L222 already glosses it "the determinant-level survival"). Removes the sign-inverted synonym; no wholesale rename. Recompiled 8pp, 0 undefined, both gates PASS.

## OPUS CLAIMS AUDIT 2026-07-23 (fresh, not in prior waves) — SOUND/CLEAN
- Every theorem re-derived from scratch (Thm 3.1 variational, Rem 3.2/3.3 Hilbert cross-check, Prop 4.1/4.3/4.5); hypothesis-sufficiency + overclaim + terminology ("total-loss factor" only, no stale) + cross-ref all clean. No CRITICAL/MAJOR/MINOR. Only residue: the two pre-existing RKW machine-provisional locators (Thm 21 L254, Prop 7 L248) — HELD for human-PDF, reconciled as the known held item, not a fresh finding.

## RKW HUMAN-PDF CONFIRMATION 2026-07-23 (user-supplied) — both locators CORRECT, item retired
- The held RKW machine-provisional item (minor-ledger #12/#42) is RESOLVED. User supplied RKW2011 (Reeb-Kastoryano-Wolf, JMP 52 082201 (2011), arXiv:1102.5170) Thm 21 + Prop 7.
- Prop.7 Eq.(21): ½‖b1−b2‖_B ≤ tanh[ħ_C/4] — confirms p4's "TV≤tanh[d_H(σ1,σ2)/4]" (½‖·‖=TV, ħ_C=d_H). The /4 (Prop 7, pair distance) vs /2 (Rem 3.3, distance-to-1) is NOT a conflict: p4 bridges via its stated triangle bound d_H(σ1,σ2)≤2 d_H(M,1), giving tanh[2 d_H(M,1)/4]=tanh[d_H(M,1)/2].
- Thm.21 = "Converse of Birkhoff's theorem": CP map T(ρi)=pi ρi' for SOME pi>0 exists iff ħ(ρ1,ρ2)≥ħ(ρ1',ρ2'). The success probs pi are existentially bound / absent from the condition → p4's "quantifies the success probabilities away / probability-blind by construction" is a FAIR, correct reading. (Resolves the ar5iv ambiguity flagged in #42.)
- No manuscript edit (citations correct). p4's only remaining pre-circulation biblio note was this; now cleared.

## W22 CONVERGENCE RE-CONFIRMATION 2026-07-26 (Fable, adversarial; claims+numerics+biblio) — CLEAN; convergence HOLDS
- Every theorem/prop/cor/remark re-derived from scratch adversarially: Thm 3.1 trade-off (iff BOTH directions via Bloch nₓ=0); Rem 3.2 invariant |detC|=exp[−½∫TrΓ]; Rem 3.3 Hilbert tanh + RKW assembly; Eq(3) dimer Bloch nₓ≡0 (saturation "every time/coupling/both phases" exact); Prop 4.1 classical; Cor 4.2 Pythagoras identity; Prop 5.1 fidelity (Hübner/Fuchs-van de Graaf every step); Prop 5.2 Lidskii (Bhatia III.4.1 with B→−B). Cross-paper (paper3 TV(∞)=κ̃/sinθ, paper1 detΓ_red zero-crossing) confirmed; Discussion (iv) direction/wording correct.
- **NUMERICS CLEAN (fresh rerun t1_region_sweep.py, seed 20260711, exit 0):** every number reproduces (broken saturation 1.28e-15; 0/99846 generators, min margin 2.997e-10; Pythagoras 4.44e-16; fidelity 0/39460; Bell 0.8087; d=3/4 margins 1.66e-6/1.12e-6; ~1.79e5 searches). Model-congruent (dimer_C=H_eff up to global phase; ny sign convention correct).
- **BIBLIO CLEAN:** RKW2011 locators (Prop 7, Thm 21) human-PDF-confirmed 07-23 (retired); 13/13 external refs claim-appropriate (standing machine-provisional).
- 2 NITs, both defensible / no action: "2×10⁴ draws each at d=3,4" (actual 19,997/20,000; 1-sig-fig accurate); RLW2022 cite-key year (deliberate preprint-year convention). 
- No manuscript change. Both gates PASS (unchanged). **p4 CONVERGENCE HOLDS (still 3/3).**

## W24 WIDE-OPEN AUDIT 2026-08-01 (Fable, adversarial; claims+numerics+biblio) - CONTENT CLEAN on all three lanes; 1 corpus-wide MAJOR (#88, user-gated); 2 re-flags rejected
- **CLAIMS CLEAN, earned by full re-derivation:** Bob's conditioned marginal from the Bell ricochet (incl. that it depends only on the effect, not the Kraus decomposition); **Thm 3.1 in full** (Delta = M - XMX traceless with ||Delta||_1 = 2*lambda, the variational step, the algebra, and the iff-condition cross-checked in Bloch form - equality iff n_x = 0 exactly as stated, degenerate M ~ 1 included); the invariant remark incl. the projector counterexample giving TV=1 at p <= 1/2; the Hilbert-metric identity and the RKW assembly chain; eq. (2) by hand from K^2 = kappa~^2; Prop 4.1 with the strict inclusion of the classical equality set; Cor 4.2; Prop 5.1 (polar decomposition, Hubner, von Neumann/rearrangement, Fuchs-van de Graaf); Prop 5.2 (Lidskii majorization, Schur-convexity, d=2 recovery). Counterexample hunts against every iff and quantifier found nothing.
- **NUMERICS CLEAN, no script skipped** (t1_region_sweep.py run in full, exit 0, seed 20260711, ~1.5 min - the paper's sole script). Every quoted number reproduces (1.28e-15 / 3.68e-13 saturation; 0/99,846 with margin 2.997e-10; Pythagorean 4.44e-16; 0/39,460 with Bell envelope 0.8087; d=3/4 margins 1.655e-6 / 1.118e-6; kappa~/sin(theta) to 6 digits). Model congruence verified line-by-line (dimer_C = H_eff up to an irrelevant global phase; B PSD <=> Gamma >= 0; script ny = the paper's chi). Parameter homogeneity consistent with the phase labels.
- **BIBLIO CLEAN:** 12/12 external entries verified against Crossref/publisher records with the published form governing (the new prompt-level rule worked - zero arXiv-over-publisher flags this pass, against three in the last p5 pass).
- **MAJOR #88 (corpus-wide, USER-GATED):** the Code-availability and provenance claims assert present-tense public reproducibility, but `p04-conditioned-ghosts` is README-only ("arriving shortly"), the hub `ghosts-program` is EMPTY, and `p02-measurable-ghosts` is EMPTY. Verified by direct fetch. Not a p4-specific defect and not orchestrator-fixable (populating the repos is user-gated by the standing content-push hold). Recorded as a CIRCULATION BLOCKER; NOT counted as a streak-resetting content finding, since it is one external condition hitting nine papers identically. **p4's content lanes are clean.**
- **REJECTED (both re-flags the auditor could not have known were closed):** (1) RKW Prop 7 / Thm 21 flagged MACHINE-EXTRACTED pending human-PDF - these were **human-PDF confirmed by the user on 2026-07-23** and the item was retired; the auditor's independent ar5iv read agreeing with the manuscript is corroboration, not a new hold. (2) "0 violations in 2x10^4 draws each at d=3,4" vs the actual 19,997/20,000 - **adjudicated defensible in W22** (1-significant-figure accurate; the abstract's ~1.8e5 total is exact). No edit.

## W26 WIDE-OPEN AUDIT 2026-08-01 (Fable, prompted to BREAK it) - 1 MINOR applied; counter -> 0
- The paper was framed to the auditor as the most-converged in the corpus and therefore the most dangerous to audit lazily, with an explicit instruction to break it and, failing that, to say precisely what was tried. **That framing found an inverted claim in the ABSTRACT that every prior clean pass had missed.**
- **MINOR applied:** "anisotropy costs survival" (abstract) and "anisotropy is exactly what a fixed total-loss factor must give up in survival" (Remark) are backwards under the paper's own definitions. Orchestrator verified numerically at fixed Tr(Gamma), i.e. fixed |det C| = e^-1: isotropic p = 0.367879, Gamma = diag(2,0) p = 0.567668, Gamma = diag(1.5,0.5) p = 0.414830 -- **at fixed total loss, anisotropy strictly INCREASES survival**, which is the paper's own AM-GM (p >= |det C|, equality iff isotropic) read the right way round. The true identity is |det C|/p = sqrt(1 - bound^2), reproduced to six decimals at three couplings. The word "survival" was doing double duty (the probability p vs the determinant-level survival |det C|). Both sites reworded; corpus re-grepped, zero stale copies.
- **The mathematics survived a serious attempt to break it:** every theorem re-derived including BOTH directions of all three equality-iffs, degenerate and rank-deficient M, singular rho_B, the full RKW assembly chain (projectivity, transpose-invariance, X-isometry, triangle inequality) and the exact Bell reduction. Script exit 0, nothing skipped, every number reproduced, model congruence verified analytically. 12/12 bibitems Crossref-verified field by field.
- **Noted as an UNDERSELL, not a defect:** Prop 5.2's Lidskii bound is exactly attained in every d (diagonal M, reversal permutation), so sharpness could be asserted rather than left at ~1e-6 numerical margins. Left for the author.
- **Re-flag, no action:** the empty-repo pointers are the user-decided #88 item. minor-ledger #177.
