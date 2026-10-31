# Same Evidence, Different Judgment? A Small Experiment on Implied Conclusions and Evidence Ordering

*GnomeMan4201 · Study: `composed-inference-ordering-v1.1` · Collected October 31, 2026 UTC*

**What I ran:** Four synthetic evidence cases × three presentation conditions × three independent tasks: 36 completed responses from `gpt-4.1-mini`, with the original failed API attempt retained.

**What I observed:** Under the frozen parser, 19/36 responses were accepted and 17/36 were rejected solely for Markdown code fences surrounding JSON. A free-form audit endorsed coordination in one condition despite insufficient evidence; a separately prompted explicit judge withheld support.

**What I cannot conclude:** One response per condition cannot establish that ordering caused the disagreement, or that the behavior generalizes to real retrieval systems.

> **Study status and disclosure:** This is a self-conducted exploratory pilot, not peer-reviewed research or a validated detector. I assigned the synthetic case labels, which have not been independently human-adjudicated. AI assistance was used in drafting and computational analysis; repeated computational checks of the same records are not independent scientific review. Public commenters discussed the underlying question but did not conduct or endorse this experiment.

## The question came from a discussion, not from a benchmark leaderboard

The starting point was Rudratosh Shastri's DEV.to article, [*How to Make RAG Show Its Evidence: Claim Verification at 15M-Document Scale*](https://dev.to/rudratosh/a-correct-answer-and-a-confident-lie-look-identical-heres-how-i-made-rag-tell-them-apart-2n45), and the discussion beneath it involving Rudratosh, Squeaky, and me. The concern was narrower than hallucination detection in general: individually well-supported observations can be composed into a paragraph that **invites** a broader explanation the evidence does not establish. Checking every explicit atomic statement may miss that implied conclusion.

In the thread, I used an infrastructure example: two domains can share an IP and publish the same narrative without that alone establishing coordinated operation. Squeaky suggested extracting the conclusion the arrangement invites and treating it as its own claim against the **combined** cited evidence. The subsequent exchange clarified something I originally underweighted: reordering can probe the judge's consistency, but a stable verdict cannot establish evidentiary correctness. We also discussed keeping surviving explanations separate from any ranking among them, because an alternative can be less plausible without being ruled out. A conclusion that remains unestablished is not necessarily false; the evidence may simply be insufficient to choose between viable explanations. This account is traceable to the actual nested replies: [my initial question](https://dev.to/gnomeman4201/comment/3j7d4), [Rudratosh's reply about composition](https://dev.to/rudratosh/comment/3j8ao), [Squeaky's extraction proposal](https://dev.to/squeaky_spirit/comment/3jaca), [my distinction between stability and validity](https://dev.to/gnomeman4201/comment/3jbo7), and [Squeaky's distinction between surviving explanations and their ranking](https://dev.to/squeaky_spirit/comment/3jbof). These exchanges motivate the pilot; none of those participants took part in the experiment or endorsed its results.

That led to four predeclared research questions:

- **RQ1:** Given a proposed relational conclusion, how does the model judge its support against stipulated evidence?
- **RQ2:** With the composed paragraph and candidate unchanged, does reversing the **evidence list** change outputs?
- **RQ3:** With the evidence list and candidate unchanged, does reversing the **sentences in the paragraph** change outputs?
- **RQ4:** When the model must identify its **own implied claim**, does it distinguish that inference from what the evidence supports?

**Scope boundary:** This experiment did **not** run a retrieval system, inspect real infrastructure, compare *not retrieved* with *retrieved but inconclusive*, or measure what actual readers infer. The distinction between evidence that was never retrieved and evidence that was read but remains insufficient mattered in the original discussion; this pilot addresses **only the second kind of interpretive gap**, with all stipulated evidence supplied directly. Here *evidence* means synthetic statements in the prompt, not independently sourced observations.

## Related research and the sample-size boundary

Rudratosh's article cites [Liu et al., *Lost in the Middle* (2023)](https://arxiv.org/abs/2307.03172) and [Veseli et al., *Positional Biases Shift as Inputs Approach Context Window Limits* (2025)](https://arxiv.org/abs/2508.07479). Those studies investigate position effects in much longer contexts and retrieval/answering tasks. Their results are relevant context for asking whether ordering matters, **not validation or replication of this three-sentence synthetic inference experiment**. The later work also warns against treating the classic lost-in-the-middle pattern as universal.

The [original post's sample-size warning](https://dev.to/rudratosh/a-correct-answer-and-a-confident-lie-look-identical-heres-how-i-made-rag-tell-them-apart-2n45) likewise matters. My 12 case-condition trials and one sample per task-condition were **never designed to estimate a failure rate or establish near-zero error**. No population-level rate, p-value, or causal ordering estimate is justified. Repeating only the one interesting flipped condition *after* seeing the output would be a selected follow-up, not a predeclared replication. A stronger prospective study would replicate **both** matched arrangements and use independent labels.

## Why there were two pilot versions

The original `v1.0` design rearranged the evidence list but left its compressed composed paragraph fixed. That could not answer the proposed question about ordering within the composition itself. Before any `v1.1` live requests, I revised the design: the composed paragraph now contains the three original evidence sentences, either in original or reversed order, while an independent condition reverses only the enumerated evidence list. The prior design is disclosed in the protocol. **v1.0 and v1.1 are different stimuli and are not pooled.**

The v1.1 protocol, script, prompts, trial labels, and scoring rules were frozen before live data collection, but my initial draft was prepared with AI assistance; that assistance was not independent adjudication of the labels. The Chromebook decision ledger records acceptance on **October 31, 2026 at 00:43:18 UTC**. Initial script SHA-256 was `ff196d55c0033059ea89b4f5c61e9ec24486b6d7fa6cbe3f47188a11b514cde5`; the canonical manifest digest was `114ab37edfcd055932fb2e5ad34d9c5ee8623a4e16fafab0e15f82f7601326dd`. These values are independently checked against the supplied archive. A hash shows byte identity against a recorded value; without a separately trusted external timestamp it does not by itself prove when those bytes existed.

## What I actually tested

I wrote four small hypothetical cases, each consisting of three stipulated factual sentences, a relational conclusion to evaluate, a provisional author-assigned support label, and an alternative interpretation. These labels are **not independently adjudicated ground truth**.

| Case | What the hypothetical evidence says | Candidate conclusion | Predeclared label | Why the label is provisional |
| --- | --- | --- | --- | --- |
| `shared-host` | Two domains shared an IP and published narrative X during one observation window | Their operators coordinated publication | `NOT_ESTABLISHED` | Shared hosting and independent publication are also compatible |
| `same-owner-control` | Separate signed records identify Organization Q as operator of each domain for the same window | The records identify a common operator | `SUPPORTED` | The signed records are stipulated authentic *within the hypothetical* |
| `temporal-leap` | Domain A published narrative X at 10:00; Domain B at 10:02 | B copied from A | `NOT_ESTABLISHED` | Both could have received X from another source |
| `direct-coordination-control` | An authenticated joint release signed by both operators states that they coordinated publication | According to the release, the operators coordinated publication | `SUPPORTED` | The label concerns what that release establishes, not unrelated collaboration |

For each case I prepared three conditions, changing sentence **order only**:

1. `baseline`: evidence list 1–2–3, paragraph 1–2–3;
2. `evidence_reverse`: evidence list 3–2–1, paragraph 1–2–3;
3. `paragraph_reverse`: evidence list 1–2–3, paragraph 3–2–1.

Each of the 12 case-condition trials received three **separate, stateless** requests to the same API:

- **`extract`:** read only the composed paragraph; identify its strongest invited relational claim, without a proposed conclusion or evidence list;
- **`judge`:** inspect the stipulated evidence, composed paragraph, and a **provided** candidate conclusion; return `SUPPORTED`, `NOT_ESTABLISHED`, or `ABSTAIN`;
- **`audit`:** inspect evidence and paragraph, identify an implied claim **itself**, and judge whether that self-selected claim is supported.

These tasks are not interchangeable. The `judge` has the desired candidate supplied to it; the `audit` must find one. The `extract` task sees the **exact same input** in `baseline` and `evidence_reverse`, because it does not receive the evidence list. Differences between those two extract results cannot be evidence-list effects.

The requests used OpenAI's Responses API with requested model `gpt-4.1-mini`, `max_output_tokens=900`, `store=false`, and no temperature explicitly specified in the request. The returned model identifier for all 36 completed requests was `gpt-4.1-mini-2025-04-14`; response metadata reported `temperature=1.0` and `top_p=1.0`. The test ran in Python 3.11.2 on Debian GNU/Linux 12 in a Chromebook Linux environment. The 12 trial positions were shuffled using a fixed scheduling seed of 42; **that seed did not control model generation**. Each task-condition was sampled once, with no replicate set or randomized presentation to a reader population.

## Execution record, including the failure

The first live attempt (`temporal-leap:evidence_reverse`, task `extract`) returned HTTP **429** at `2026-10-31T00:45:06+00:00` and produced no model verdict. That failure was appended to `model_raw.jsonl` and `events.jsonl`. After API credits were added, execution resumed with an explicit retry flag, keeping the failed attempt instead of overwriting it. The earlier successful responses were skipped automatically during completion of the remaining trials.

The retained record has **37 request starts, 37 matching finishes, 36 completed API responses, and one HTTP 429 failure**. There are no unresolved starts and no duplicate successful task-condition entries. The 36 successful outputs span the 12 planned trials, three tasks each. All 36 completed response records report the same model identifier. The archive contains full returned response objects, exact prompts and their per-trial hashes, and UTC events.

## Results under the frozen scoring rule

The original parser accepted only a JSON object returned directly as the response text. **Nineteen of 36 responses met that strict formatting rule. Seventeen did not**, because the model wrapped its otherwise readable JSON object in Markdown code fences. All 17 were returned with API status `completed`: this is an **output-format compliance failure**, not a transport failure, and not a model abstention.

| Task | Strictly valid | Fenced / invalid under frozen rule |
| --- | ---: | ---: |
| `extract` | 6 | 6 |
| `judge` | 6 | 6 |
| `audit` | 7 | 5 |
| **Total** | **19** | **17** |

For the six strictly valid `judge` responses, **6 matched the author-assigned case labels, 0 disagreed, and 0 abstained**. This is **6 of 6 valid explicit-judge outputs**, not 6 out of all 12 judging trials, and certainly not proof of an independently established 100% accuracy rate. The remaining six judge outputs failed the frozen format rule.

One **strictly valid** comparison is especially relevant. On the `shared-host` case, the `audit` task produced:

| Condition | Model's self-selected relation | Audit verdict | Format |
| --- | --- | --- | --- |
| `baseline` | `COORDINATION` | `NOT_ESTABLISHED` | Strictly valid |
| `evidence_reverse` | `COORDINATION` | `NOT_ESTABLISHED` | Fenced / invalid in frozen score |
| `paragraph_reverse` | `COORDINATION` | **`SUPPORTED`** | Strictly valid |

Both baseline and paragraph-reversed audits addressed substantially the same question of whether the domains coordinated publication. In the paragraph-reversed condition, the audit explicitly treated coincident publication and shared IP as establishing coordination, despite the synthetic case's predeclared counter-explanation. In **the same paragraph-reversed trial**, the independently requested explicit `judge` instead returned `NOT_ESTABLISHED`.

This is an **observed disagreement** between the two prompt tasks, and an observed difference between audit outputs under different paragraph orders. These are not two independent adjudicators: both requests used the same model, with different instructions. It does **not** establish that paragraph order caused the difference: there was one request per condition, with uncontrolled model sampling. A stable or changing verdict in this setting is a description of responses, not a causal estimate.

Among strictly valid baseline-versus-paragraph-reversal audit pairs, **one of three** changed verdict. There were **no** strictly valid audit baseline-versus-evidence-reversal pairs, because all four evidence-reversed audit responses used fenced JSON. For the strict explicit `judge`, only **one** baseline-versus-paragraph-reversal pair had two valid responses; it did not change. No strict baseline-versus-evidence-reversal judge pair was complete. Reporting a global strict-format flip percentage here would conceal those uneven denominators.

## A separate, clearly labeled exploratory analysis of the fenced responses

**This section does not change the frozen scorer or its published primary counts.** I inspected the 17 raw outputs that were rejected for formatting. All 17 consist of exactly one Markdown-fenced JSON object with the expected task fields. Removing only the opening and closing code fences permits syntactic parsing and schema checks. The original strings remain untouched in the archive.

This **post-run format-normalized** reading produces a complete descriptive matrix:

| Case | Author label | Explicit `judge`: baseline / evidence reverse / paragraph reverse | Self-selected `audit`: same three conditions | `extract` relation: same three conditions |
| --- | --- | --- | --- | --- |
| `shared-host` | NE | NE / NE / NE | **NE / NE / S** | COORDINATION / COORDINATION / COORDINATION |
| `same-owner-control` | S | S / S / S | S / S / S | COMMON_OPERATOR / COORDINATION / COORDINATION |
| `temporal-leap` | NE | NE / NE / NE | NE / NE / NE | COPYING / COPYING / COPYING |
| `direct-coordination-control` | S | S / S / S | S / S / S | COORDINATION / COORDINATION / COORDINATION |

Here `NE` means `NOT_ESTABLISHED`; `S` means `SUPPORTED`. These are **exploratory** decoded readings, not retroactively valid frozen-protocol outputs.

In this secondary reading, all **12/12** explicit judge outputs match the author-assigned labels; no explicit-judge verdict changes across the eight baseline/reversal comparisons (four cases × two reversals). The open audit has **one verdict difference among eight** comparable baseline/reversal comparisons, the `shared-host` paragraph-reversal result described above. Do **not** treat 12/12 as externally validated accuracy: the author supplied the target claim and labels, and the model saw clear synthetic premises.

There is also a useful warning about treating category changes as ordering effects. In `same-owner-control`, the `extract` task returned `COMMON_OPERATOR` for `baseline` but `COORDINATION` for `evidence_reverse`, **even though those two extraction prompts had identical instructions and paragraph text**. Both outputs described Organization Q operating both domains. The different category labels therefore cannot be attributed to the evidence-list reversal; that list was never in the extractor's input. The same category drift appears in the paragraph-reversed extraction, but without repeated trials the cause is unresolved. Similarly, the audit's `COORDINATION` tag sometimes describes **common operation**, not evidence of coordinated publication. This weakens any attempt to score relation tags as interchangeable with actual claim semantics.

## What the pilot does and does not answer

**Observed in the archive:** a single open-audit response endorsed coordination from a shared IP and shared publication observations where another open-audit request, and the explicit judge of that same reversed paragraph, withheld support. The fixed judge's complete exploratory verdict set was stable. The frozen data-collection record includes 17 strict-format failures and an earlier HTTP 429 failure, all retained. The same-owner extractor exhibited category drift even under identical model-facing input.

**Not demonstrated:** that rearranging sentences *caused* the audit's disagreement; that any reader would infer coordination from these particular paragraphs; that a RAG pipeline would fail similarly; that an independently judged model can reliably detect implied claims; or that all four author labels are independently established. This pilot also does not distinguish *not retrieved* from *retrieved but insufficient*—all hypothetical evidence was supplied directly, and no retrieval process was run.

**Further limitations:** four deliberately chosen cases; simplistic positive controls; two negative cases using obvious unsupported leaps; unblinded, self-evaluating `audit`; one sample per task/condition; no second human adjudicator of implied meaning or rival plausibility; no test of evidence freshness, provenance, or real-world attribution; no p-values or population effect estimates. A response may be correct about a supplied candidate while failing to identify an implied conclusion in free composition, and those must remain distinct questions.

**Kill criterion:** If the inputs, comparison denominators, or label review cannot separate mere verdict variability from evidentiary validity, the study is **inconclusive for detection-capability claims**. On that criterion, v1.1 is useful as a transparent exploratory record and as a concrete counterexample to overinterpreting a single self-audit, **not** a qualified detector or generalized causal experiment.

## Conclusion

The central lesson of this small run is not that an ordering attack was proven, nor that explicit verification solved the problem. In one trial, the **explicit judge withheld support for coordination while the open audit endorsed it from the same synthetic observations**. When the evidence was held constant across independently requested conditions, the audit's verdict also differed once. Because model sampling was not replicated or controlled, the cause remains open. The strict-parser failures are part of the result, not numbers to be silently repaired away.

That is the result I can bring back to the discussion: one transparent observed disagreement, an explicit non-result for causal attribution, a complete record of format failures, and materials another person can inspect or rerun from the [public research archive](https://github.com/GnomeMan4201/composed-inference-ordering-v1.1/blob/main/Research_v1_1.zip). A stronger next study would preregister independently assessed, blinded implication labels and rival explanations, add repeats per condition, and keep extraction, explicit judgment, and free-form audit scores separate.

---

## Appendix A — Reproducibility, hashes, and complete trace

The raw archive is `evidence_inference_results_v1_1.zip`, with SHA-256:

`b117050aa57dd573ac8bec20211ae706a7bd957ecda60ff051a5a15b836b543e`

Its principal source artifacts are `manifest.json` (case/condition data), `prompts.jsonl` (36 exact task prompts), `model_raw.jsonl` (36 successful API responses plus a failure), `events.jsonl` (37 starts and finishes), `report_gpt-4.1-mini.json` (frozen-derived report), `evidence_inference_pilot_v1_1.py` (generation and scoring code), `EXPERIMENT_PROTOCOL_v1_1.md` (pre-run rules), and `DECISIONS_AND_DEVIATIONS.md` (pre- and post-preflight decisions).

The response archive and event hashes are respectively:

- `888d9e94b3e36379b175e51d7fcf602d1e31b0b15221026e09de9fc4aa897cab`
- `983590dc9cb85d16cca78447d680a51311e8bbdb58663bb8e80d0e17e8a1631d`

A separately implemented, read-only Python standard-library script, `independent_audit_v1_1.py`, verifies the recorded file hashes, reconstructs prompt texts and hashes, checks start/finish pairs and unique outcomes, recomputes strict and exploratory counts, and writes a 36-row matrix without modifying the original archive. With the files together:

```bash
python3 independent_audit_v1_1.py \
  --archive evidence_inference_results_v1_1.zip \
  --out independent_audit_output
```

`derived_audit_v1_1.json` and `trial_matrix_v1_1.csv` are newly generated **analysis artifacts**, not original experimental records. For any individual result, follow `trial_id + task` in the matrix to its `attempt_id`, `prompt_sha256`, and provider response ID, then consult the exact entry in `prompts.jsonl` and `model_raw.jsonl`.

**Archival caveat:** The results ZIP flattens its paths. Its retained `SHA256SUMS.txt` refers to an earlier pre-run `DECISIONS_AND_DEVIATIONS.md`, whose hash appropriately changed when append-only decisions were recorded, as well as two initial-bundle files not included in the results ZIP (`README_CHROMEBOOK.md` and an archived v1.0 script). The principal **v1.1** protocol/script and generated prompt/raw files have been checked separately. Preserve the originally downloaded v1.1 bundle alongside the results ZIP for full historical documentation.


## Appendix B — Origin links and review boundaries

These are specific comments in the original DEV.to discussion, included so a reader can audit the research question without relying on my paraphrase:

- [Initial composed-claim question](https://dev.to/gnomeman4201/comment/3j7d4) — GnomeMan4201, October 27.
- [Acknowledgment of the claim-composition gap](https://dev.to/rudratosh/comment/3j8ao) — Rudratosh, October 28.
- [Extractor idea and same-evidence ordering proposal](https://dev.to/squeaky_spirit/comment/3jaca) — Squeaky, October 28.
- [Separating verdict stability from evidence support](https://dev.to/gnomeman4201/comment/3jbo7) — GnomeMan4201, October 29.
- [External-standard / rival-inference objection](https://dev.to/squeaky_spirit/comment/3jaol) — Squeaky, October 29.
- [Surviving alternatives versus prior-based ranking](https://dev.to/squeaky_spirit/comment/3jbof) — Squeaky, October 29.

The article motivates a new self-conducted experiment; it does not claim these commenters performed, supervised, or reviewed it.

**Public artifact:** [Research_v1_1.zip](https://github.com/GnomeMan4201/composed-inference-ordering-v1.1/blob/main/Research_v1_1.zip) in the [public GitHub repository](https://github.com/GnomeMan4201/composed-inference-ordering-v1.1). The ZIP contains `materials/evidence_inference_results_v1_1.zip`, the original unmodified archive (SHA-256 `b117050aa57dd573ac8bec20211ae706a7bd957ecda60ff051a5a15b836b543e`), as well as `materials/independent_audit_v1_1.py`, the trial matrix, and accompanying documentation. The publication ZIP SHA-256 is `598527528087ca10efdd09523c27f242861062d75e01432d0c4df377e8428c0e`. After extracting `Research_v1_1.zip`, run `python3 materials/independent_audit_v1_1.py --archive materials/evidence_inference_results_v1_1.zip --out independent_audit_output` from the extracted directory. These reproducibility files do **not** constitute independent adjudication of the labels or external replication.