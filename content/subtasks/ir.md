---
title: 'IR Subtask'
date: 2019-12-07T22:26:38+09:00
---

In this subtask, given a query and a dataset collection, 
a system is expected to generate a ranked list of datasets.
Ranked lists will be evaluated in a similar way to traditional ad-hoc retrieval tasks.


# Queries

A new query list will be provided to participants in Data Search 2.

Queries and qrels in NTCIR-15 Data Search can be used as training data in this round.
More specifically, we recommend to use the following files for training in Data Search 2:

- English
  - `data_search_2_e_train_topics.tsv` (training and test queries used in NTCIR-15 Data Search)
  - `data_search_2_e_train_qrels.txt` (qrels for training and test queries in NTCIR-15 Data Search)
- Japanese
  - `data_search_2_j_train_topics.tsv` (training and test queries used in NTCIR-15 Data Search)
  - `data_search_2_j_train_qrels.txt` (qrels for training and test queries in NTCIR-15 Data Search)

Note that `data_search_2_*_train_topics.tsv` is a union of `data_search_*_train_topics.tsv`
and `data_search_*_test_topics.tsv`,
and `data_search_2_*_train_qrels.txt` is a union of `data_search_*_train_qrels.txt`
and `data_search_*_all_qrels.txt`.

These files are available at [Data Search Test Collection](/data/).


# Dataset Collections

Participants are expected to retrieve datasets from:
- English
  - `data_search_e_collection.jsonl.bz2` (metadata) 
  - `data_search_e_data.tar.bz2` (data files) 
- Japanese
  - `data_search_j_collection.jsonl.bz2` (metadata) 
  - `data_search_j_data.tar.bz2` (data files) 

These files are available at [Data Search Test Collection](/data/).


# Evaluation

Runs will be evaluated in terms of effectiveness metrics
including nDCG (normalized discounted cumulative gain), nERR (normalized expected reciprocal rank), and Q-measure.
nDCG@10 will be used as the primary evaluation metric.

We will conducted relevance judgments by using crowd-sourcing services.
The relevance of each data will be evaluated at a three point scale: irrelevant, partially relevant, and highly relevant.
Three assessors will be assigned to each data.

# Submission

<a name="submission"></a>

Each team is allowed to submit up to 10 runs.
**You cannot submit 10 English and 10 Japanese runs.**
Runs should be generated automatically.

## Run file name

Please submit a single file whose name should be the form of `[GROUP_ID].zip`.
`[GROUP_ID]` should be replaced with the group ID you decided at the NTCIR registration. 
For example, if you group ID is `TOKYO`, then the file name must be `TOKYO.zip`.

The single zip file `[GROUP_ID].zip` can contain up to 10 run files.
Each run file should be named as follows:

`[GROUP_ID]-[LANGUAGE]-[PRIORITY]`

where

- `[GROUP_ID]` is your group ID.
- `[LANGUAGE]` is either `J` (Japanese subtask) or `E` (English subtask).
- `[PRIORITY]` is an integer between 1 and 10, indicating which runs should be prioritized in the pooling for relevance assessments.

e.g. `TOKYO-E-1` or `TOKYO-J-10`

Run file names should NOT have any suffix such as `.txt` or `.run`.
Note that we try, but may not be able to evaluate all the runs due to a budget constraint,
and evaluate only runs selected by the priority.

## Run file format

The format is the same as those used in the NTCIR WWW tasks. 

The first line of the run file should describe your ranking algorithm,
which will be used when the organizers report participants' results:

`<SYSDESC>[SYSDESC][TAB][TYPE]</SYSDESC>`

- `[SYSDESC]`: a short string that explains the ranking algorithm
- `[TAB]`: a special character, \t, or a unicode character (U+0009)
- `[TYPE]`: a comma-separated string that systematically classifies the ranking algorithm.
It is defined as `[TYPE] := [DATA],[NEURAL],[ENTITY],[NUMBER]`, where
  - `[DATA]`: 'Y' (Yes) or 'N' (No) indicating whether the data files are used.
  - `[NL]`: 'Y' (Yes) or 'N' (No) indicating whether neural language models (e.g. BERT, RoBERT, GPT, and T5) are used.
  - `[ENTITY]`: 'Y' (Yes) or 'N' (No) indicating whether entities are treated differently from the other tokens.
  - `[NUMBER]`: 'Y' (Yes) or 'N' (No) indicating whether numbers are treated differently from the other tokens.

e.g. `<SYSDESC>BM25 and BERT	Y,Y,N,N<SYSDESC>`
(This ranking algorithm uses the data files and a neural language model)

e.g. `<SYSDESC>BM25 and BERT	Y,N,Y,N<SYSDESC>`
(This ranking algorithm uses the data files and estimates the relevance mainly based on entities)

The other lines in the file should be of the form:

`[TOPIC_ID] 0 [DATASET_ID] [RANK] [SCORE] [RUN_NAME]`

e.g.
```
DS-J-1001 0 000031519435 1 7.3 TOKYO-J-2
DS-J-1001 0 000031519438 2 3.5 TOKYO-J-2
...
```

where each field should be separated by a whitespace, and

- `[TOPIC_ID]` is the ID of a query for which data sets were retrieved.
- `[DATASET_ID]` is the ID of a data set retrieved for the query.
- `[RANK]` is the rank of the data set, which should start from 1.
- `[SCORE]` is the score of the data set.
- `[RUN_NAME]` should be exactly the same as the run file name.

Note that the run files should contain the results 
for all the **test queries**, not for any training queries.
Also note that `[RANK]` and `[SCORE]` fileds are not used in the evaluation:
only the order of `[DATASET_ID]` in the run file is used when effectiveness measures are computed.
You can include up to 1,000 datasets per query.

## Submission Form

Registered teams can upload their runs at [NTCIR-16 Data Search 2: IR Subtask Submission Form](https://forms.gle/4h8YGhMSpksAHWPS9).
Please submit a single zip file `[GROUP_ID].zip` that contains up to 10 run files.
**Although you can submit runs multiple times,
only the latest single submission is accepted as the official submission from your team.**
Note that any submissions from non-registered teams or those after the deadline will be ignored.

