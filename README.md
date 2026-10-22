# IELTS Writing Scoring Benchmark: five platforms on 97 official responses

[简体中文](README.zh-CN.md)

This dataset records the overall Band that five IELTS Writing scoring platforms gave to 97 IELTS Writing responses whose official overall Band has been published by IELTS.org, the Official IELTS Practice Materials or Cambridge IELTS. Every per-response score is here, so every figure in our [benchmark article](https://ieltswritingpractice.app/blog/ielts-writing-scoring-accuracy-benchmark/) can be checked and recomputed.

It is published by [IELTS Writing Practice](https://ieltswritingpractice.app/), which is one of the five platforms compared. We publish the raw scores so that readers do not have to take our summary on trust.

## Results on all 97 responses

| Platform | Mean absolute error | Signed bias | Within 0.5 Band | Within 1.0 Band | More than 1.0 Band off |
|---|---|---|---|---|---|
| IELTS Writing Practice | 0.53 | -0.27 | 74.2% (72/97) | 93.8% (91/97) | 6 |
| IELTSWritingChecker.org | 0.57 | -0.38 | 70.1% (68/97) | 86.6% (84/97) | 13 |
| ChatGPT | 0.88 | -0.85 | 46.4% (45/97) | 76.3% (74/97) | 23 |
| Engnovate | 0.94 | -0.86 | 39.2% (38/97) | 73.2% (71/97) | 26 |
| Writing9 | 1.72 | -1.58 | 19.6% (19/97) | 35.1% (34/97) | 63 |

The difference between IELTS Writing Practice and IELTSWritingChecker.org is within sampling noise: IELTS Writing Practice's mean absolute error minus IELTSWritingChecker.org's is -0.036 Band, with a 95% paired-bootstrap interval of -0.119 to +0.046. Both are clearly closer to the official Band than ChatGPT, Engnovate and Writing9. Breakdowns by task, module, source and the Cambridge IELTS 20 and 21 subset, plus every pairwise comparison, are in [`results/metrics.md`](results/metrics.md).

## Contents

| Path | What it is |
|---|---|
| `data/scores.csv` | One row per response: source, locator, official Band and each platform's Band |
| `scripts/compute_metrics.py` | Recomputes every metric from the CSV (Python 3, standard library only) |
| `results/metrics.md`, `results/metrics.json` | Output of the script |

To reproduce the results:

```bash
python3 scripts/compute_metrics.py
```

## Columns in `data/scores.csv`

| Column | Meaning |
|---|---|
| `response_id` | Stable identifier for the response |
| `source` | Publication containing the response and its official Band |
| `locator` | Where to find the response in that publication |
| `source_url` | Official download link, where the publisher provides one |
| `module` | Academic or General Training |
| `task` | Task 1 or Task 2 |
| `recent_cambridge_20_21` | `yes` for the 32 responses from Cambridge IELTS 20 and 21 |
| `official_band` | Published official overall Band (the reference score) |
| `ielts_writing_practice`, `ieltswritingchecker_org`, `chatgpt`, `engnovate`, `writing9` | Overall Band returned by each platform |
| `writing9_displayed` | Writing9's score as recorded, with `<4` where it displayed a score below 4; `<4` is scored as 3.5 in the `writing9` column |

## The 97 responses

| Source | Responses |
|---|---|
| IELTS.org Academic Writing sample tasks (2023) | 12 |
| IELTS.org General Training Writing sample tasks (2023) | 11 |
| IELTS.org computer-delivered Academic Writing samples | 4 |
| Official IELTS Practice Materials Volume 1 | 10 |
| Official IELTS Practice Materials Volume 2 | 10 |
| Cambridge IELTS 18 Academic | 2 |
| Cambridge IELTS 19 Academic | 8 |
| Cambridge IELTS 19 General Training | 8 |
| Cambridge IELTS 20 Academic | 8 |
| Cambridge IELTS 20 General Training | 8 |
| Cambridge IELTS 21 Academic | 8 |
| Cambridge IELTS 21 General Training | 8 |
| **Total** | **97** (Task 1: 51, Task 2: 46; Academic: 54, General Training: 43) |

The responses, questions, task visuals and examiner comments belong to their publishers and are not included. Use the `source` and `locator` columns to find each one.

## Method

- **Reference score.** Each response's published official overall Band. Criterion scores are not compared.
- **Collection.** The dataset holds one recorded score per response per platform, given for the response together with its question; all scores were collected no later than 30 August 2026. The Task 1 visual was supplied wherever the platform accepted it. The overall Band each platform returned was recorded unchanged. Question and response texts were transcribed from the sources, so small transcription differences between platforms are possible.
- **Matching.** The Writing9 and Engnovate scores were recorded in a sheet ordered by source, with book, test and task given only for Cambridge IELTS 20 and 21. The other rows were matched to response IDs by that source order, which the person who recorded the sheet confirmed is the order of the source materials; every row's task and official Band agree with the match.
- **Writing9.** Its public workflow did not accept the Academic Task 1 visual. When it displayed `<4`, the score is recorded as 3.5, the top of the displayed range.
- **Measures.** Signed error = platform Band minus official Band. Mean absolute error is the mean of the absolute errors and signed bias is the mean signed error. Within 0.5 and within 1.0 are inclusive. Pairwise differences use a paired bootstrap with 10,000 resamples and a fixed seed.

## Limitations

- 97 responses is a small sample. Differences smaller than about 0.1 Band of mean absolute error cannot be told apart reliably; see the intervals in `results/metrics.md`.
- Each platform scored each response once. Repeated scoring can give different results.
- The scores show each platform as it was up to 30 August 2026. All five products, including IELTS Writing Practice, may have changed since.
- Older published responses may appear in model training data. The Cambridge IELTS 20 and 21 subset reduces this risk but cannot rule it out.
- Automated scores are estimates, not official IELTS results.

## Licence and citation

The data (`data/`, `results/`) is released under [CC BY 4.0](LICENSE-DATA) and the code under the [MIT licence](LICENSE-CODE). Please cite:

> IELTS Writing Practice (2026). *IELTS Writing Scoring Benchmark: five platforms on 97 official responses* (version 1, scores collected by 30 August 2026). https://ieltswritingpractice.app/blog/ielts-writing-scoring-accuracy-benchmark/

Questions and corrections: support@ieltswritingpractice.app
