
## 1) The fixed benchmark architecture

Use the GAME scaffold to structure the repo and the experiment loop:

**Goals**: portable operator gain, not just within-wrapper score.
**Algorithms**: executable G-Loop policy plus Spike-Tune rules.
**Measurements**: held-out wrapper performance, swap robustness, delayed recheck, and stability metrics.
**Evolution**: auditable change log of what variant changed, why, and what failed. That matches your lab’s simulate → fit → compare logic and the requirement to keep changes reproducible and boundary-aware.

Keep three things **fixed**:

* the wrapper universe
* the scoring rules
* the banking tests

Let the swarm vary only the **protocol policy**.

## 2) Plausible far-transfer baseline protocol

This is the baseline I would freeze first.

### A. Core state gate

Three states only:

* `IN_BAND`
* `OVERHEAT`
* `FLAT`

Escalation is allowed only in `IN_BAND`. If out of band, recovery or safe degradation routes fire first. That is directly aligned with your Ψ-gate rule and the idea that updates are most portable when they reflect task structure rather than survival of a bad state.

### B. Type-1 baseline: capacity/control transfer

Baseline rules:

* increase only one dial at a time
* when stable and mismatch is low, bump one constraint only
* when plateau + low drift appears, keep n stable and add a small constraint bump plus a wrapper swap
* when plateau + high drift appears, reduce constraint and prioritise clean re-entry
* count transfer only when gains hold across at least two wrappers and two demands without a mismatch spike
* if 2-tuple tracking holds but 3-tuple inference fails, keep n stable and raise relational variety and probe frequency instead of simply making the task harder

### C. Type-2 baseline: mindware/operator transfer

Baseline rules:

* Y0 rigour budget before serious action
* after Y9 commit, EOU is mandatory
* once a chain works, run an immediate wrapper swap
* confusion routes to Y10 discrimination, not more rumination
* entropy phase uses wrapper, stake, and representation swaps
* MI phase compresses what stayed predictive and retests it
* bank only after Y11 pass, repeated mission improvement, and delayed recheck

### D. Internal spike rule

Treat every click/spike as labile:

* protect a 1–3 session fragile phase
* stabilise first within the same wrapper
* then run minimal one-variable swaps
* require delayed recheck
* no same-day banking

That is your baseline protocol. It is already plausible and mechanistically coherent.

## 3) What the benchmark families should be

Start with **three benchmark families**, each with source wrappers, held-out wrappers, and distant-domain wrappers.

### Family 1: capacity/control family

Purpose: test portable control invariants.

Source wrappers:

* set-point regulation task
* relational tracking task
* interference/speed pulse task

Held-out wrappers:

* same deep demand, new symbols/rules/phrasing
* altered noise and timing

Distant-domain wrappers:

* fast regime-control toy trading task
* backend load-management or triage task

This is grounded in your own framing that far transfer comes from stabilise → perturb → select invariants → bank → deploy, and that repeated invariance testing across wrappers and stakes acts as a curriculum for generalisation.

### Family 2: operator/mindware family

Purpose: test whether Y-operator chains become portable.

Source wrappers:

* diagnosis/troubleshooting
* decision/planning
* explanation/teaching

Held-out wrappers:

* same operator demands, new content domains

Distant-domain wrappers:

* trading regime diagnosis
* backend incident diagnosis
* prioritisation and commit under uncertainty

Your protocol already specifies portable banking criteria for diagnosis, planning, negotiation, ethical choice, teaching, and install/bank mode, which makes these natural wrapper families for Y-chain testing.

### Family 3: spike/instability family

Purpose: test whether the protocol produces real regime shifts rather than thin automation.

Source wrappers:

* repeated challenge plateaux
* perturbation pulses
* first-success then immediate-swap cases

Held-out wrappers:

* different perturbation forms
* different cue bindings

Distant-domain wrappers:

* pressure-shift trading episodes
* backend incidents with changing stakes or observability

This family is justified by your Spike-Tune account: plateau signals, entropy then MI capture, minimal swaps after a click, and banking only after stabilisation and delayed recheck.

## 4) The key test parameters to freeze in the baseline

These should be fixed at first, not searched.

### State signals

* `psi_state`
* `mismatch`
* `drift`
* `recovery_latency`
* `error_burst_rate`
* `operator_fidelity`
* `mission_success_signal`
* `swap_cost`

These follow directly from your watch signals for Type-1 and Type-2 Spike-Tune.

### Trigger rules

* escalate only if `IN_BAND`
* plateau + low drift → Spike-Tune trigger
* plateau + high drift → corridor widening
* first successful Type-2 chain → immediate wrapper swap
* persistent confusion → Y10 discrimination
* successful spike candidate → same-wrapper stabilisation before portability test

### Banking rules

A baseline banked invariant requires:

* one same-wrapper stabilisation pass
* one wrapper swap pass
* one stake or boundary/trap pass
* repeated mission improvement for Type-2
* delayed recheck
* recorded trigger, boundary, and unpack trigger

## 5) What the swarm is allowed to vary

This is the interesting part. I would expose only these knobs.

### Protocol-level variants

* corridor width
* perturbation size
* plateau threshold
* low-drift threshold
* high-drift threshold
* fragile-window length
* delayed recheck gap
* exploration/exploitation bias

### Y-chain variants

* minimal core vs evaluation-heavy
* mandatory Y7 before Y10 vs optional
* early Y5 abstraction vs late abstraction
* stronger Y13/Y14/Y15 protection vs looser protection
* more aggressive Y11 banking gates vs lighter ones

### Curriculum variants

* blocked vs interleaved operator training
* near-to-far swap ladder vs early mixed swap exposure
* single-domain-first vs mixed-domain training
* same-wrapper consolidation length before first swap
* frequency of representation swaps

### Domain-routing variants

* trading introduced early vs only after core operator gains
* backend ops introduced as a final transfer test vs part of mixed training
* stake pressure introduced early vs late

Those are all plausible hypotheses about far transfer under your theory.

## 6) Plausible benchmark tests

I would make the evaluator run six tests for every variant.

### Test 1: source performance

Does the protocol actually improve within the training wrappers?

### Test 2: held-out wrapper transfer

Does the gain carry to new wrappers with the same deep demand?

### Test 3: demand transfer

Does the gain survive across at least two demand classes, as your Type-1 rule requires?

### Test 4: immediate post-success swap

When the protocol “works once”, does it survive the mandated early swap, or does it collapse as thin automation?

### Test 5: delayed recheck

Does the candidate invariant survive after a delay? No banking without this.

### Test 6: distant-domain transfer

Can the policy carry into toy trading and backend-ops wrappers without a major mismatch spike?

That last test is the real stretch goal.

## 7) Scoring

Use one primary score and a few veto gates.

### Primary score

`PortabilityScore`

Proposed form:

* source score
* plus held-out wrapper score
* plus distant-domain score
* plus validated-spike score
* minus state-drift penalty
* minus thin-automation penalty
* minus complexity penalty

### Veto gates

A variant cannot win overall if:

* it banks without delayed recheck
* it over-relies on one wrapper family
* it gains score by spending too much time out of band
* it improves source score but collapses on immediate swap

That keeps the benchmark faithful to your mechanism rather than reward hacking.

## 8) Minimal repo layout

I’d build the repo like this:

```text
tg-gloop-swarm/
  README.md
  program.md
  config/
    benchmark.yaml
    baseline_protocol.yaml
    search_space.yaml
  evaluator/
    run_benchmark.py
    score_protocol.py
    banking_gate.py
    spike_metrics.py
  policies/
    baseline_gloop.yaml
    variants/
  wrappers/
    capacity/
    operators/
    trading/
    backend_ops/
  missions/
    source/
    heldout/
    distant/
  results/
    runs/
    figures/
    tables/
  reports/
    reproducibility_log.md
    winning_variants.md
```

That mirrors your GAME repo logic: runnable, checkable, auditable, and easy to compare across variants.

## 9) The baseline variants I would start with

Do not start with a huge space. Start with five.

### Variant A: strict baseline

Exactly the February rules.

### Variant B: abstraction-heavy

More Y5/Y2 compression after successful swaps.

### Variant C: probe-first

Earlier Y10 under uncertainty or confusion.

### Variant D: strong Psi protection

Tighter out-of-band restrictions, slower escalation.

### Variant E: aggressive Spike-Tune

Earlier wrapper and representation swaps, but same strict banking gate.

That gives you interpretable contrasts.

## 10) My recommended MVP sequence

Phase 1:

* build capacity family only
* implement the strict baseline and two variants
* score source, held-out wrapper, and delayed recheck

Phase 2:

* add operator family
* add Y-chain logging and banking gates

Phase 3:

* add distant-domain trading and backend wrappers
* compare whether the best capacity/operator variants still generalise

That is the smallest version that still tests your theory properly.

The central mechanistic claim you are testing is already explicit in your February protocol: far transfer is most plausible when you stabilise a control regime in the Ψ-band, apply controlled perturbations that force preservation of deep invariants, and bank only what survives swaps, traps, and real deployment signals.

 

