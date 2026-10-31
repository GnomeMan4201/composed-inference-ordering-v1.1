# Composed inference and evidence-ordering pilot (v1.1)

> **Repository upload status (October 31, 2026):** The original evidence ZIP and full publication bundle have **not yet been uploaded**. This repository currently contains the manuscript and a derived trial matrix only. Do not treat the public release or reproduction materials as complete until `Composed_Inference_Publication_v1_1.zip` is present. The manuscript deliberately retains an artifact-link placeholder pending that upload.

**Status:** Self-conducted exploratory study. Not peer reviewed; case labels and perceived implications are author-assigned, not independently human-adjudicated. No causal sentence-order effect or general RAG verifier performance is established.

This package is a publication assembly, not an alteration of the frozen experiment. The original results archive at `materials/evidence_inference_results_v1_1.zip` remains byte-identical to the Chromebook archive.

## Contents

- `materials/evidence_inference_results_v1_1.zip`: frozen prompt manifest, full raw model outputs, failure and event records, original script, protocol and decision ledger. Original SHA-256: `b117050aa57dd573ac8bec20211ae706a7bd957ecda60ff051a5a15b836b543e`.
- `materials/independent_audit_v1_1.py`: read-only standard-library verification script; no API calls.
- `materials/derived_audit_v1_1.json`, `materials/trial_matrix_v1_1.csv`: derivative analysis, not original observations.
- `materials/REPRODUCIBILITY_AND_REVIEW_NOTES_v1_1.md`: audit boundaries, source references, and review questions.
- `DEVTO_Manuscript_Publication_Candidate_v1_1.md`: detailed article. The public artifact link is a *placeholder* until an actual GitHub URL is confirmed.
- `SHA256SUMS_PUBLICATION.txt`: SHA-256 checksums of all files in this publication package, calculated after assembly.

## Offline reproduction (Python 3.9+, stdlib only)

```bash
python3 materials/independent_audit_v1_1.py --archive materials/evidence_inference_results_v1_1.zip --out independent_check
```

The verifier writes derived files to `independent_check`; it does not modify the raw ZIP or contact any network. For reproducibility claims, inspect the verifier itself and compare the original response text, trial IDs, prompt hashes, and event pairs. The post-run fenced-JSON decoding is *exploratory* and does not change the original strict format counts.

## Result boundary

- Original: 36 completed responses, 1 earlier HTTP 429 attempt; 19 accepted strict-format outputs, 17 fenced-format rejections.
- Original strict primary: 6 of 6 evaluable explicit-judge responses match the author-assigned labels. This is not externally verified accuracy.
- Separately labeled post-run format-normalized reading: 12/12 explicit-judge responses match author labels, 0/8 explicit-judge flips, 1/8 open-audit flips.
- The one open-audit endorsement in `shared-host:paragraph_reverse` conflicts with the separate explicit judge. No causal ordering claim follows from one response per condition.

## Original discussion

- https://dev.to/gnomeman4201/comment/3j7d4
- https://dev.to/rudratosh/comment/3j8ao
- https://dev.to/squeaky_spirit/comment/3jaca
- https://dev.to/gnomeman4201/comment/3jbo7
- https://dev.to/squeaky_spirit/comment/3jaol
- https://dev.to/squeaky_spirit/comment/3jbof

## Security and publication

Automated search found no API key patterns, bearer credentials, or email addresses in the source ZIP files; this is a screening check, not an exhaustive confidentiality audit. Examine files before public release. This package must not be described as externally reviewed or preregistered with an independently trusted timestamp. Do not publish the DEV.to article with an unresolved artifact placeholder.