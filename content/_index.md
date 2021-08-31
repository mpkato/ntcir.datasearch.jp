---
title: 'NTCIR-16 Data Search 2'
description: 'A shared task on ad-hoc retrieval for governmental statistical data'
keywords: ['ntcir', 'ir', 'information retrieval', 'dataset', 'test collection']
date: 2019-12-07T22:26:38+09:00
---

<style type="text/css">
.markerline {
    background: linear-gradient(transparent 80%, #ffffa8 80%);
}
table {
    width: 100%;
}
td {
    vertical-align: top;
    padding: 0.25em 0;
}
</style>

NTCIR-16 Data Search 2 is a shared task on ad-hoc retrieval for governmental
statistical data. The second round of Data Search addresses the retrieval from
a dataset collection published by the Japanese government
([e-Stat](https://www.e-stat.go.jp/)),
and one published by the US government ([Data.gov](https://data.gov/)).
Furthermore, this round introduces two additional subtasks:
QA subtask and UI subtask.

---

## Contact
data-search-org@googlegroups.com or [@NTCIRDataSearch](https://twitter.com/NTCIRDataSearch) 


## Schedule

|                  |                                      |
| ---------------- | ------------------------------------ |
| **Jan 31, 2021** | [Dataset collections and training queries release](/data) |
| <del>**Aug 31, 2021**</del> **Sep 30, 2021** | Registration due and test queries release |
| <del>**Sep 30, 2021**</del> **Oct 31, 2021** | Submission due for the IR subtask |
| <del>**Nov 31, 2021**</del> **Nov 30, 2021** | Evaluation results release for the retrieval subtask |
| **Feb 1, 2022** | Submission due for the QA and UI subtasks |

<div style="height: 1em"></div>

## Registration

Please take a look at [What participants must do](http://research.nii.ac.jp/ntcir/ntcir-16/obligations.html).
Then, go to http://research.nii.ac.jp/ntcir/ntcir-16/howto.html and follow the registration instruction.
The registration is necessary for participants to submit their runs.

---

# Subtasks

<a name="tasks"></a>

For each subtask, we provide Japanese and English test collections.

- [IR Subtask](/subtasks/ir)
  - In this subtask, given a query and a dataset collection, 
a system is expected to generate a ranked list of datasets.

- [QA Subtask](/subtasks/qa)
  - In this subtask, given a question and a dataset, 
a system is expected to generate an answer to the question, mainly by extracting a part of the dataset.

- [UI Subtask](/subtasks/ui)
  - In this subtask, participants are expected to develop a search system 
    with an effective search interface for dataset search tasks.


# Organizers

<a name="organizers"></a>

- Makoto P. Kato (University of Tsukuba)
- Hiroaki Ohshima (University of Hyogo)
- Ying-Hsang Liu (Australian National University)
- Hsin-Liang Chen (Missouri University of Science and Technology)
