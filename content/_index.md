---
title: 'Introduction'
date: 2019-07-13T22:26:38+09:00
---

NTCIR-15 Data Search is a shared task on ad-hoc retrieval for governmental
statistical data. The first round of Data Search focuses on the retrieval of
a statistical data collection published by the Japanese government
([e-Stat](https://www.e-stat.go.jp/)),
and one published by the US government ([Data.gov](https://data.gov/)).

---

## Schedule

|                      |                                      |
| -------------------- | ------------------------------------ |
| **Feb 29, 2020** --- | Data collection and queries released |
| **Apr 30, 2020** --- | Registration due                     |
| **Jun 12, 2020** --- | Run submission due                   |
| **Aug 20, 2020** --- | Evaluation results released          |

---

# Task

<a name="task"></a>

We will provide queries and a data collection.
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
    "domain": "www.e-stat.go.jp",
    "dataurl": "https://www.e-stat.go.jp/stat-search/file-download?statInfId=000031519435&fileKind=0",
    "title": "地方公共団体の議会の議員及び長の所属党派別人員調 地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在） 選挙執行件数 | ファイルから探す | 統計データを探す | 政府統計の総合窓口",
    "url": "https://www.e-stat.go.jp/stat-search/files?page=1&toukei=00200231&result_page=1&layout=dataset&stat_infid=000031519435",
    "timestamp": "2018/09/05 08:23:05",
    "subtitle": "地方公共団体の議会の議員及び長の所属党派別人員調 / 地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在）",
    "data_fields": {
        "提供統計名": "地方公共団体の議会の議員及び長の所属党派別人員調等（H20.12.31現在）",
        "統計表名": "選挙執行件数",
        "担当機関": "総務省",
        "データセットの概要": "",
        "政府統計名": "地方公共団体の議会の議員及び長の所属党派別人員調",
        "公開年月日時分": "2017-01-06 11:34",
        "集計地域区分": "該当なし"
    },
    "id": "000031519435",
    "filename": ["a0abc17d8ce4715933c69132418dc7337e76c5aad06beb9f5d69b0f1c1870ff9-05%E9%81%B8%E6%8C%99%E5%9F%B7%E8%A1%8C%E4%BB%B6%E6%95%B0%E8%AA%BF.xls"]
}
```

**SAMPLE (English)**

```
{
    ... (Released later) ...
}
```

The metadata of data sets will be provided by a single JSON file,
while the statistical data are stored as individual files.
As seen in the examples, the "filename" field indicate statistical data contained in the data set.

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
we gather queries for data search by using a crowd-sourcing service.
Workers are given a topic and asked to input a query for data search.
This query generation task is conducted in both Japanese and English, in separate tasks.

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

Note that data distributed to participants include only queries but not their topics.
Thus, search systems cannot access to the topics for which queries are generated.

# Data

<a name="data"></a>

## Training Data

We plan to distribute around over 100 queries as training queries,
for which relevance judgments will be also available.

## Test Data

We plan to distribute around over 100 queries as test queries,
for which participants are expected to produce ranked lists of data sets.

# Evaluation

<a name="evaluation"></a>

Submitted system results (called _runs_) will be evaluated in terms of effectiveness metrics
including nDCG (normalized discounted cumulative gain), ERR (expected reciprocal rank), and Q-measure.

We will conducted relevance judgments by using crowd-sourcing services.
The relevance of each data will be evaluated at a three point scale: irrelevant, partially relevant, and highly relevant.
Three assessors will be assigned to each data.

# Organizers

<a name="organizers"></a>

- Makoto P. Kato (University of Tsukuba)
- Hiroaki Ohshima (University of Hyogo)
- Ying-Hsang Liu (Australian National University)
- Hsin-Liang Chen (Missouri University of Science and Technology)
