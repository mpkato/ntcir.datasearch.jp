---
title: 'NTCIR-15 Data Search'
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

NTCIR-15 Data Search is a shared task on ad-hoc retrieval for governmental
statistical data. The first round of Data Search focuses on the retrieval of
a statistical data collection published by the Japanese government
([e-Stat](https://www.e-stat.go.jp/)),
and one published by the US government ([Data.gov](https://data.gov/)).

---

## Contact
data-search-org@googlegroups.com or [@NTCIRDataSearch](https://twitter.com/NTCIRDataSearch) 


## Schedule

|                  |                                      |
| ---------------- | ------------------------------------ |
| **Feb 29, 2020** | Data collection and queries released<br> - <span class="markerline">[Released on Feb 29, 2020](#data)</span>|
| **Apr 30, 2020** | Registration due                     |
| <span class="markerline">**Jul 10, 2020** (Extended)</span><br><del>**Jun 12, 2020**</del> | Run submission due                   |
| **Aug 20, 2020** | Evaluation results released          |

<div style="height: 1em"></div>

## Registration

Please visit http://research.nii.ac.jp/ntcir/ntcir-15/howto.html,
and take a look at *What participants must do*.
Then, go to http://ntcir.nii.ac.jp/NTCIR15Regist/ for registration.
The registration is necessary for participants to submit their runs.

---

# Task

<a name="task"></a>

We provide queries and data collections.
Participants' systems are expected to generate a ranked list of statistical data _sets_ for each query.
The ranked lists will be evaluated in a similar way to traditional ad-hoc retrieval tasks.

To prepare queries, we first obtained topics of statistical data search.
Then, queries were manually generated for each topic.

There are two subtasks in the NTCIR-15 Data Search task, namely,

- **Japanese subtask**
  - **Data collection**: A statistical data collection from [e-Stat](https://www.e-stat.go.jp/)
  - **Topics**: Japanese topics extracted from Yahoo Chiebukuro (a community question-answering Web service)
  - **Queries**: Japanese queries generated for each Japanese topic
- **English subtask**
  - **Data collection**: A statistical data collection from [Data.gov](https://data.gov/)
  - **Topics**: Translated Japanese topics with named entities replaced with US entities
  - **Queries**: English queries generated for each English topic

## Data collection

The two data portal Web sites, e-Stat and Data.gov,
provide an introduction page for each statistical data.
Hence, we retrieved the statistical data as well as the introduction pages,
and extracted metadata from each introduction page.
As a set of statistical data is introduced by the same metadata,
there can be one-to-many relationship between metadata and statistical data.
Thus, we define a **data set** as a pair of metadata and a set of statistical data,
and use it as a _retrieval unit_ in our task.
Examples of data sets are shown below.

**SAMPLE (Japanese)**

```
{
    "id": "000031519435",
    "url": "https://www.e-stat.go.jp/stat-search/files?page=1&toukei=00200231&result_page=1&layout=dataset&stat_infid=000031519435",
    "attribution": "出典：政府統計の総合窓口(e-Stat)（https://www.e-stat.go.jp/）",
    "title": "地方公共団体の議会の議員及び長の所属党派別人員調 地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在） 選挙執行件数 | ファイルから探す | 統計データを探す | 政府統計の総合窓口",
    "description": "地方公共団体の議会の議員及び長の所属党派別人員調 / 地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在）",
    "data": [
        {
            "data_format": "xls",
            "data_url": "https://www.e-stat.go.jp/stat-search/file-download?statInfId=000031519435&fileKind=0",
            "data_filename": "a0abc17d8ce4715933c69132418dc7337e76c5aad06beb9f5d69b0f1c1870ff9-05%E9%81%B8%E6%8C%99%E5%9F%B7%E8%A1%8C%E4%BB%B6%E6%95%B0%E8%AA%BF.xls"
        }
    ],
    "data_fields": {
        "提供統計名": "地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在）",
        "統計表名": "選挙執行件数",
        "担当機関": "総務省",
        "データセットの概要": "",
        "政府統計名": "地方公共団体の議会の議員及び長の所属党派別人員調",
        "公開年月日時分": "2017-01-06 11:34",
        "集計地域区分": "該当なし"
    }
}
```

**SAMPLE (English)**

```
{                                                                                                                                                          
    "id": "0063664a-d0d7-4ce2-9462-0463a89fc274",
    "url": "https://catalog.data.gov/dataset/0063664a-d0d7-4ce2-9462-0463a89fc274",
    "attribution": "CRED REA Fish Team Stationary Point Count Surveys at Sarigan, Marianas Archipelago, 2005 (https://catalog.data.gov/dataset/0063664a-d0d7-4ce2-9462-0463a89fc274) is licensed under U.S. Government Work (http://www.usa.gov/publicdomain/label/1.0/)"
    "title": "CRED REA Fish Team Stationary Point Count Surveys at Sarigan, Marianas Archipelago, 2005",
    "description": "Stationary Point Counts at 4 stations at each survey site were surveyed as part of Rapid Ecological Assessments (REA) conducted at 3 sites around Sarigan in the Marianas Archipelago (MA) during 3 September - 1 October 2005 in the NOAA Oscar Elton Sette (OES 0511) Reef Assessment and Monitoring Program (RAMP) Cruise. Raw survey data included species level abundance estimates.",
    "data": [
        {
            "data_format": "excel",
            "data_organization": "National Oceanic and Atmospheric Administration, Department of Commerce",
            "data_url": "https://data.nodc.noaa.gov/coris/data/NOAA/nmfs/pifsc/cred/REAFish/CNMI_2005/CRED_REA_FISH_SAIPAN_2005.xls",
            "data_filename": "076342d026a0feec762ce5cb18e047db61e24db557958f75ca7aaa668b5e1342-CNMI_2005/CRED_REA_FISH_SAIPAN_2005.xls"
        }
    ],
    "data_fields": {
        "Resource Type": "Dataset",
        "Metadata Date": "June 20, 2018",
        "Metadata Created Date": "February 7, 2018",
        "Metadata Updated Date": "February 27, 2019",
        ...
        "metadata_sources": [
            "https://catalog.data.gov/harvest/object/fc5a39b7-4c9f-49b8-af95-2812d9b3264c"
        ]
    }
}
```

The metadata of data sets will be provided by a single JSON file,
while the statistical data are stored as individual files.
As seen in the examples, the `data` field indicate statistical data contained in the data set.

Note that e-Stat releases their contents under a license compatible with [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/),
and Data.gov releases many of their data as [U.S. Government Works](https://www.usa.gov/government-works) or under [CC0 1.0 Universal (CC0 1.0)
Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/).
We included only these data in our data collection.

## Topics

We crawled question-answers pairs including links to [e-Stat](https://www.e-stat.go.jp/)
from a Japanese community question-answering service, [Yahoo! Chiebukuro](https://chiebukuro.yahoo.co.jp/).
We manually examined each question and extracted questions that indicate information needs for data search.
The extracted questions are used as topics, and are referred to for generating queries.

**SAMPLE (Japanese)**

```
1. 都道府県別の有効求人倍率をおしえてください。
2. 世界の都市人口ランキングのようなページがあったら教えてください。
3. 各県別で、そこに住む人の平均通勤時間がわかる統計はありませんか。
```

We manually translate Japanese topics into English topics.
If a Japanese topic contains entities specific to the Japanese culture,
they are replaced with other appropriate entities specific to U.S.
For example, `What is the population in Tokyo?` can be translated into
`What is the population in New York?`.

**SAMPLE (English)**

```
1. What is the jobs-to-applicants ratio in each state?
2. May I know a webpage that introduces population ranking of the world cities?
3. Is there any statistics that show the average commute time per state?
```

## Queries

Since it is not obvious how topics can be transformed to queries,
and we are also interested in query formulation for data search,
we gathered queries for data search by using a crowd-sourcing service.
Ten workers were given a topic and asked to input a query per topic for data search.
This query generation task was conducted in both Japanese and English, in separate tasks.

**SAMPLE (Japanese)**

```
1. 有効求人倍率　都道府県
2. 都市人口　ランキング
3. 都道府県別　平均通勤時間　比較　情報
```

**SAMPLE (English)**

```
1. jobs to applicants ratio state
2. city population ranking
3. states average commute time comparison information
```

We built a unigram language model for each topic based on ten generated queries,
and selected a query per topic with the lowest perplexity with respect to the language model.
Note that data distributed to participants include only queries but not their topics.
Thus, search systems cannot access to the topics for which queries are generated.

# Data & Tool

<a name="data"></a>

## Data

All the data are available at [NTCIR-15 Data Search Test Collection](/data/) (see README.md).
Relevance judgments for training queries was also released on May 13, 2020.

<br>

### Test collection statistics

|                               |                                  |
| ----------------------------- | -------------------------------: |
| **Japanese Collection**       | 1,338,402 (~100GB, compressed)   |
| **Japanese Training Queries** | 96                               |
| **Japanese Test Queries**     | 96                               |
| **English Collection**        | 46,615 (~445GB, compressed)      |
| **English Training Queries**  | 96                               |
| **English Test Queries**      | 96                               |

<br>

## Tool

A tool for producing baseline runs.

[![mpkato/ntcir-datasearch - GitHub](/ntcir-datasearch.svg)](https://github.com/mpkato/ntcir-datasearch)


# Submission

<a name="submission"></a>

Each team is allowed to submit up to 10 runs.
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
which may be used when the organizers report participants' results:

`<SYSDESC>[REPLACE_ME]</SYSDESC>`

e.g. `<SYSDESC>BM25 and BERT<SYSDESC>`

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

Registered teams can upload their runs at [NTCIR-15 Data Search Submission Form](https://forms.gle/fdTuHRCc9NZvfDLX9).
Please submit a single zip file `[GROUP_ID].zip` that contains up to 10 run files.
Although you can submit runs multiple times,
only the latest submission is accepted as the official submission from your team.
Note that any submissions from non-registered teams or those after the deadline will be ignored.


# Evaluation

<a name="evaluation"></a>

Runs will be evaluated in terms of effectiveness metrics
including nDCG (normalized discounted cumulative gain), nERR (normalized expected reciprocal rank), and Q-measure.

We will conducted relevance judgments by using crowd-sourcing services.
The relevance of each data will be evaluated at a three point scale: irrelevant, partially relevant, and highly relevant.
Three assessors will be assigned to each data.

# Organizers

<a name="organizers"></a>

- Makoto P. Kato (University of Tsukuba)
- Hiroaki Ohshima (University of Hyogo)
- Ying-Hsang Liu (Australian National University)
- Hsin-Liang Chen (Missouri University of Science and Technology)
