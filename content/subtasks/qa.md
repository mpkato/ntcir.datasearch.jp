---
title: 'QA Subtask'
date: 2019-12-07T22:26:38+09:00
---

In this subtask, given a question and a dataset, 
a system is expected to generate an answer to the question by extracting a part of the dataset.

More specifically, participants are given a question and a dataset (ID).
For example,

```
Question: What is the population in Tokyo in 2020?
Dataset:  000002505731
```

A system is expected to generate `13,510,000` as the answer to the given question,
which is included in the dataset.

# Questions

A question list will be released around the registration due.
We may not be able to provide questions for training.

# Dataset Collections

Participants are expected to find answers from:
- English
  - `data_search_e_collection.jsonl.bz2` (metadata) 
  - `data_search_e_data.tar.bz2` (data files) 
- Japanese
  - `data_search_j_collection.jsonl.bz2` (metadata) 
  - `data_search_j_data.tar.bz2` (data files) 

These files are available at [Data Search Test Collection](/data/).

# Evaluation

Generated answers are evaluated in two ways, as was done in reading comprehension tasks:
- **Exact match**
  - The fraction of answers that exactly match the ground truth answers.
- **Macro-averaged F1 score**
  - Let X be a set of words in the generated answer and Y be a set of words in the ground truth answer.
    Precision is defined as P = |X &cap; Y| / |X|, while recall is defined as R = |X &cap; Y| / |Y|.
    F1 score of an answer is computed as 2PR / (P + R).
    Macro-averaged F1 score is the average of the F1 scores over all of the answers.

Exact match will be used as the primary evaluation metric.

# Submission

<a name="submission"></a>

Each team is allowed to submit a run per day.
Runs should be generated automatically.

## Run file format

The first line of the run file should describe your algorithm,
which will be used when the organizers report participants' results:

`<SYSDESC>[REPLACE ME]</SYSDESC>`

e.g. `<SYSDESC>BERT-based approach<SYSDESC>`

The other lines in the file should be of the form:

`[QUESTION_ID][TAB][ANSWER]`

e.g.
```
DS2-QA-J-1001	2010
DS2-QA-J-1002	Tokyo
...
```

where each field should be separated by a TAB character (\t or U+0009), and

- `[QUESTION_ID]` is the ID of a question to which the answer is given.
- `[ANSWER]` should be a string and is expected to be the answer to the question.

Note that the run files should contain the results 
for **all the test questions**.

