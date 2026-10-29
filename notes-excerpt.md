# Lab-notebook excerpt: paper 4 (The price of a post-selected signal)

Excerpted from the full running notebook (notes.md) in the program hub:
https://github.com/embeddetech/ghosts-program

---

## 2026-07-11 — T1 STEPS 1+2 DONE: triage CLEAR; the trade-off
## THEOREM found and numerically established (dimer exactly extremal)

**Step 1 (triage, agent; full report
`research/t1_literature_triage.md`):** NOT PREEMPTED. The exact
TV-vs-survival trade-off is unposed anywhere: steering literature has
the HJW constraint but never this optimization; postselected-metrology
bounds (Arvidsson-Shukur 1903.02563, Combes-Ferrie-Jiang-Caves) are
Fisher-information-shaped (local), don't imply a TV bound; the whole
LHFL resolution chain never bounds the magnitude. Closest: Reeb-
Kastoryano-Wolf 1102.5170 (Hilbert-metric contraction) and Regula-
Lami-Wilde 2209.10550 (postselected discrimination exponents) — cite
prominently. Toolkit: HJW + SDP duality, Hilbert/Thompson metrics,
SLOCC normal forms.

**Step 2 scoping fact (3-line argument):** with ARBITRARY local
filters the static trade-off is trivial — orthogonal projector
filters give TV = 1 at every p ≤ 1/2. The content is DYNAMICAL:
semigroup contractions are invertible and |det C| =
e^{−∫tr(loss)dt} is a message-independent invariant (X-conjugation
preserves det). The right conserved quantity was hiding in paper 1's
det Γ bookkeeping all along.

**Step 2 result (`t1_region_sweep.py`): the theorem.** For any 2×2
contraction C on one arm of a Bell pair, messages (C, XCX):

    TV_quantum ≤ sqrt(1 − (|det C|/p)²),   p = survival
    equivalently  TV² + (|det C|/p)² ≤ 1   (Pythagorean form)

- Broken-PT dimer saturates EXACTLY, pointwise in t, at every s
  tested (|TV−bound| ≤ 1.3e-15); unbroken dimers saturate too
  (≤4e-13): the whole balanced-gain/loss family is extremal, not
  just the broken phase.
- 0/99,846 random lossy generators violate; min margin 3e-10
  (envelope approached, never crossed).
- The paper-2 beable observable is the DIAGONAL part: TV_cl(25)
  matches κ̃/sinθ to 6 digits at s = 0.3/0.5/0.65; TV_cl ≤ TV_q
  strictly — **the conditioned coherences carry the difference: the
  beable currency sees a strictly weaker conditioning signal than
  the quantum currency.**
- Proof sketch (to write): σ_i = M_i^T/(2p); ||M − XMX||₁ ≤
  2(μ₁²−μ₂²) by Rayleigh quotients (v†Mv ≤ μ₁², (Xv)†M(Xv) ≥ μ₂²);
  (μ₁²−μ₂²)² = 4p² − 4|det C|²; saturation iff X swaps M's
  eigenvectors (loss eigenframe X-antisymmetric = exactly the dimer
  geometry). Controls: Hermitian and X-symmetric-loss dynamics give
  TV = 0 to machine precision.

**Remaining for the T1 paper:** clean proof write-up; arbitrary
ρ_AB (Bell extremality); n-dimensional / unequal-p generalization
(Ky Fan); the classical-TV version's own bound; positioning vs
RKW/RLW per triage. Target unchanged: PRA/Quantum theorem paper.

---

## 2026-07-11 — T3 IN PROGRESS: integrated spectrum built; THE WEDGE
## (a real correction to the s4c edge statistics)

Code: `t3_cosi_forecast.py` (instrument constants pending agent
data). Redshift-integrated arriving spectrum
I(E) = (c/4π)∫dz j((1+z)E, z)/[H(z)(1+z)³]; controls: line-source
closed form 1.1e-5, local-slab limit 1.7e-3, near-edge wedge law
0.6%.

**RESULT (new, modifies how s4c's numbers apply to the cosmological
signal): cosmological integration converts the local STEP edge into
a WEDGE** — I(E) vanishes linearly at Λ (superposition of edges at
Λ/(1+z)); the endpoint stays exactly sharp (I≡0 above Λ) but
near-edge counts scale as (window)², not (window). Edge-window
fractions: ±2% window holds 0.081% of counts (wedge) vs 2.1%
(step) — ×26 penalty at 1% resolution, ×9 at 3%. GV age factor
(t², i.e. rate growing with cosmic age) mildly flattens the low-E
stacking, leaves the wedge intact. Endpoint-regression MC (s4c
style, 8 cosθ bands, quantile estimator): N_5σ(edge, wedge) ≈ 1e7
signal photons vs the step-shape ~1-2e6 — **the cosmological wedge
costs ×5–10 in counts for the edge observable; the dipole
(3.7-4.3e-3, N_5σ ≈ 2.7-3.7e6) is untouched.** Resolution 1% vs 3%
barely matters once the shape is a wedge (quantile statistics
dominate). Estimator slope bias ~−15% (quantile+smearing),
self-calibrating in a template fit; numbers are signal-only
(background dilution adds 1/f_s²). Note for paper 2 v-next: the
s4c edge numbers describe the LOCAL (z≈0-dominated) signal; any
integrated-background version must use the wedge statistics.

COSI forecast + Λ_max re-derivation await the instrument-data agent
(effective area, exposure, CGB levels, Cline 2023-24 overlap).

---

## 2026-07-11 — T3 DONE: the bound moved (3 → 18.8 MeV), the edge
## moved into the MeV gap, and COSI cannot reach it — an honest null
## forecast

Instrument/bound data: `research/t3_instrument_data.md` (agent,
42 sources). **Headline: the CJM 2004 bound is OBSOLETE.**
Cline–Puel–Toma–Wang (arXiv:2308.12989, PRD 108 095033) refit
vacuum → 2 ghosts + 2 photons with exact phase space against
COMPTEL: Λ ≤ 18.8 MeV (real scalar, 95% CL) — 6× weaker. Their
companion 2401.02958 confirms our flat-edge shape (dn/dE ∝
Λ⁷ Θ(Λ−E)) and independently states our redshift integral. No other
post-2004 update exists; COSI (launch 2027, 0.2–5 MeV, ~1% FWHM,
~1.3e8 cm²s/direction over 2 yr) is the only funded MeV mission
through ~2030.

**Forecast (`t3_cosi_forecast.py`, anchor: signal = CGB at
0.8×bound when Λ = bound, factor ~2 proxy):**
- At the current bound the edge sits at ~19 MeV — ABOVE the COSI
  band and inside the MeV sensitivity gap (0.3–100 MeV is 2–3
  orders worse than adjacent bands; no funded mission).
- In-band (0.2–5 MeV) signal fraction: f_s ≤ 2.5e-9 for Λ ≤ 3 MeV,
  1.6e-7 at Λ = 5, 2.2e-3 even at Λ = 18.8 (flat signal under a
  steeply rising CGB). With N_cgb ≈ 5.5e7 full-sky band counts,
  N_sig ≤ 1.2e5 at the bound: **the wedge edge (needs ~1e7 signal
  photons, /f_s² dilution) is unreachable at every allowed Λ.**
- The 21σ "dipole" on total counts is the kinematic dipole of the
  whole CGB — shared with comoving AGN, NOT phantom-specific
  (concordant with the task-19 finding). The discriminating
  observable was always the edge.

**Conclusions banked:** (i) paper 2 updated (two sentences: intro +
tests(b)) to cite the 18.8 MeV bound and note the edge now lives in
the MeV gap; recompiled, 21 pp. (ii) The citable phenomenology
statement for any future write-up: *the phantom spectral edge of a
bound-saturating ghost sector lies in the MeV gap; COSI closes
nothing in-band because Λ⁸ scaling makes sub-5-MeV cutoffs
signal-free; the edge territory (5–19 MeV) waits for a
newASTROGAM-class instrument* — plus the WEDGE correction to the
edge statistics (previous entry), which any MeV-gap mission
forecast must use. (iii) The dipole-mining recommended test
((3+Γ(E))β energy-scaling along the fixed CMB axis on existing
Fermi data) remains the cheapest kinematic-vs-intrinsic
discriminator for the CGB itself, independent of phantoms.
"The phantom menaced, twenty years on" as a standalone paper is
DOWNGRADED to a section-length statement: the honest content is a
null forecast + the wedge statistics + the gap statement.

---

## 2026-07-11 — T1 STEP 3 DONE: theorem set completed, paper 3
## DRAFTED (v0.1, 7 pp — audits pending)

Extended `t1_region_sweep.py` (tests T-E/F/G) + `paper3/main.tex`
("The price of a post-selected signal: a sharp
survival–distinguishability trade-off, saturated by broken-PT
dynamics").

**Theorem upgrades since step 2:**
1. GENERALIZED to effects: the bound needs no single Kraus operator —
   for ANY survival effect 0 ≤ M ≤ 1 with flip-related messages
   (M, XMX): TV² + (√detM/p)² ≤ 1. Projectors have detM = 0 →
   vacuous bound → correctly reproduces the trivial static case
   (TV=1 at p≤1/2); the inequality has content precisely for
   dynamics, where √detM = |detC| = e^{−½∫TrΓdt} is the dissipated
   weight.
2. SATURATION PROVED analytically: dimer Bloch computation gives
   M = e^{−2at}[(c²+(a²+s²)σ_h²)1 + 2ac·σ_h σz + 2as·σ_h² σy] —
   n_x ≡ 0 (numerics: exactly 0.00e0), X-conjugation antipodal ⇒
   equality at every t, every s, BOTH phases.
3. CLASSICAL bound proved (Prop): same RHS via M₁₁M₂₂ ≥ detM;
   extremal family = uncoupled loss (tanh²+sech²=1 identity,
   verified 2e-16); coupled dimer's classical deficit = its
   conditioned coherence; κ̃/sinθ situated as the classical shadow
   of a bound-saturating quantum signal.
4. GENERAL PURE INPUTS (Prop): TV ≤ √(1 − 2detρ_B√(detM₁detM₂)/
   (p₁p₂)) via qubit fidelity identity + Fuchs–van de Graaf;
   0/39,663 violations.
5. CONJECTURE REFUTED (kept in the paper per honesty policy): Bell
   state is NOT extremal at fixed (|detC|, √(p₁p₂)) — counter-
   examples exceed the Bell envelope by up to 0.80. The detρ_B
   dependence is real.
6. GENERAL DIMENSION (Prop): TV ≤ Σ|μ²↓−μ²↑|/(2TrM) via Lidskii +
   Schur convexity; 0/20,000 violations at d=3 and d=4.

## 2026-07-11 — PAPER-3 AUDIT CYCLE (three agents): v0.2, all
## findings applied; one theorem UPGRADED by the audit

**Bibliography agent:** 14/15 OK; RLW journal details verified by
direct web check (IEEE TIT 70, 3453 (2024) — restored; overrides
the triage's abstract-level "69 (2023)"); Bhatia pointer sharpened
to Thm III.4.1; Hübner attribution for the qubit fidelity identity
CONFIRMED correct (not Jozsa).

**Independent calc agent: ALL SEVEN CLAIMS PASS** from scratch
(fresh scripts, first-principles construction of Bob's conditioned
state incl. multi-Kraus decompositions — marginal depends only on
the effect, 6.7e-16; sympy symbolic proof of the dimer Bloch form
on both branches; Haar-random G at d=3,4,5; qubit fidelity identity
vs Uhlmann 2.6e-14; FvdG near-equality "violations" chased to
machine epsilon). Every headline script number reproduced exactly.
**And it caught a code-vs-comment factor-2 mismatch in T-F whose
resolution UPGRADED Prop 5.1:** the code was already testing the
stronger factor-4 bound — which turns out to be PROVABLE
(rearrangement + AM-GM gives Trσ₁σ₂ ≥ 2√(detσ₁detσ₂), so
F² ≥ 4√(detσ₁detσ₂)) and REDUCES EXACTLY to the sharp Bell-state
theorem at ρ_B = 1/2: the general proposition now interpolates to
the main theorem instead of being weaker by a factor 2.

**Adversarial agent:** 0 CRITICAL, 4 MAJOR, 12 MINOR — all fixed:
(1) Prop 5.1 purification bookkeeping corrected (polar
decomposition, unitary absorbed into effect relabeling wlog);
(2+3) factor-4 rewrite + numerics extended to fully independent
message pairs (0/39,460 mixed draws); (4) "deficit = exactly the
coherence" was FALSE as stated — replaced by the exact result it
gestured at, now Corollary (Pythagorean decomposition of the
signal): TV² = TV_cl² + χ², χ = |n_y|/p = 2|Im σ₀₁|, holds for
EVERY effect and flip pair (verified 4.4e-16) — a strictly better
statement than the error; (5) trial count corrected 1.6e5 → 1.8e5;
(6) d=3,4 now Haar+permutation relabelings, margins updated
(1.7e-6, 1.1e-6); (7) Prop 5.2 setup stated for general d;
(8) LHFL resolution history split correctly (Tang located the
signal; Brody/Ju restored consistency); (9) κ̃/sinθ qualified as
configuration-level at first mention; (10) experimental-proposal
pointer fixed (proposal/, not paper 1); (11) extremal rhetoric
tightened ("equality set n_x = 0; the dimer traces it
dynamically"; classical equality set strictly smaller);
(12) strict-deficit claim scoped to broken phase/t>0 (Rabi-node
exception); (13) σ_h → h (Pauli collision); (14) "dissipated
weight" → "accumulated total-loss factor"; (16) 0/39,460 count now
quoted in the manuscript.

Compiles clean, 7 pp. **Remaining before circulating (small):**
full-text read of RKW 1102.5170's postselected-distinguishability
section (triage called it the closest textual overlap; current
"appears never to have been answered" rests on abstract-level
triage), and the user's own read-through.

**Paper 3 status: v0.2, audit-clean.** Open problems recorded in
the draft: sharp general-input bound (extremal family at fixed
detρ_B), multipartite/CV, a trade-off for the coherence side χ of
the Pythagorean decomposition, and the suggestive detΓ/detM
connection to the paper-1 divisibility bookkeeping.

---

## 2026-07-11 — RKW FULL-TEXT READ: PARTIAL OVERLAP FOUND AND
## REPOSITIONED (v0.3) — the audit's last item, and it mattered

Full-text read of Reeb–Kastoryano–Wolf 1102.5170 (all sections +
appendices). **Finding: partial overlap — machinery, not
statement.** Our RHS is a Hilbert-metric quantity in disguise:
√(1−detM/p²) = tanh[h(M,𝟙)/2], and the core inequality is
DERIVABLE in three lines from their published Cor. 15
(TV ≤ tanh[h/4]) + projectivity of h + X-isometry + triangle
inequality. A one-line elementary Bloch proof also exists (both
conditioned states have Bloch radius √(1−detM/p²); flip pair =
antipodal at most). NOT in RKW: any statement trading
distinguishability against survival probability (their h mods out
normalization — their Thm 21 quantifies the probabilities away,
deliberately blind), any steering/bipartite-conditioned setup, the
invariant detM/p², the saturation/extremal analysis, the
decomposition. Their pointwise bound tanh[h(σ₁,σ₂)/4] is SHARPER
off the saturating orbit; ours is the sharp eigenvalue-only
(uniform) closure — and the two coincide exactly on the PT-dimer
orbit (m_x = 0), verified numerically by the agent.

**Repositioning applied (v0.3, 8 pp):** new Remark (Hilbert-metric
reading) states the debt precisely — contraction technology is
RKW's; the statement, the invariant, the operational reading, the
steering formulation, and the equality structure are ours; intro
and discussion claims softened from "never answered" to "never
posed as such, though assemblable from RKW"; the elementary Bloch
proof acknowledged. This is exactly the referee-vulnerability the
triage flagged, now closed on our terms. AUDIT CYCLE COMPLETE.
Remaining before circulating: user read-through only.
