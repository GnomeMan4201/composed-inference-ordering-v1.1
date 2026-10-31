# Composed inference and evidence-ordering pilot (v1.1)

> **Public archive uploaded and verified (October 31, 2026):** [`Research_v1_1.zip`](https://github.com/GnomeMan4201/composed-inference-ordering-v1.1/blob/main/Research_v1_1.zip) is the complete publication bundle. Archive SHA-256: `598527528087ca10efdd09523c27f242861062d75e01432d0c4df377e8428c0e`. Its Git blob SHA-1 matches the public repository metadata. The original results ZIP inside it remains byte-identical to the original Chromebook archive.

**Status:** Self-conducted exploratory study. Not peer reviewed; case labels and perceived implications are author-assigned, not independently human-adjudicated. No causal sentence-order effect or general RAG verifier performance is established.

This repository hosts the corrected publication candidate and a downloadable ZIP containing the full experiment and offline verification materials. The ZIP is a publication assembly; it does not alter the frozen study. The internal `materials/evidence_inference_results_v1_1.zip` remains byte-identical to the Chromebook archive.

## Contents

**At repository root:** the [updated manuscript](DEVTO_Manuscript_Publication_Candidate_v1_1.md), this README, the [derived trial matrix](materials/trial_matrix_v1_1.csv), and [`Research_v1_1.zip`](Research_v1_1.zip). The following paths are **inside the downloaded ZIP** after extraction:

- `materials/evidence_inference_results_v1_1.zip`: frozen prompt manifest, full raw model outputs, failure and event records, original script, protocol and decision ledger. Original SHA-256: `b117050aa57dd573ac8bec20211ae706a7bd957ecda60ff051a5a15b836b543e`.
- `materials/independent_audit_v1_1.py`: read-only standard-library verification script; no API calls.
- `materials/derived_audit_v1_1.json`, `materials/trial_matrix_v1_1.csv`: derivative analysis, not original observations.
- `materials/REPRODUCIBILITY_AND_REVIEW_NOTES_v1_1.md`: audit boundaries, source references, and review questions.
- `DEVTO_Manuscript_Publication_Candidate_v1_1.md`: the archival manuscript snapshot inside the ZIP (it contains the pre-upload link placeholder); **use the updated root-level manuscript** for publishing.
- `SHA256SUMS_PUBLICATION.txt`: SHA-256 checksums of all files in this publication package, calculated after assembly.

## Offline reproduction (Python 3.9+, stdlib only)

Download and extract `Research_v1_1.zip`, then run this from the extracted directory:

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

Pattern-based screening found no API key patterns, bearer credentials, or email addresses in the source ZIP files; this is not an exhaustive confidentiality audit. The source archive is now public. This study must not be described as externally reviewed or preregistered with an independently trusted timestamp. The root-level manuscript links to the uploaded archive; the archived manuscript snapshot still contains the old placeholder.