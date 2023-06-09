# LGRe: Latent Graph Recurrent Network for Document Ranking
Paper at [DASFAA 2021](https://link.springer.com/chapter/10.1007/978-3-030-73197-7_6)

If you use this work, please cite as: [bibtex](https://citation-needed.springer.com/v2/references/10.1007/978-3-030-73197-7_6?format=bibtex&flavour=citation)

```
@InProceedings{LGRe,
author="Dong, Qian
and Niu, Shuzi",
title="Latent Graph Recurrent Network for Document Ranking",
booktitle="Database Systems for Advanced Applications",
year="2021",
publisher="Springer International Publishing",
pages="88--103"
}
```
## Getting started

This code is tested on Python 3.6. Install dependencies using the following command:

```
pip install -r requirements.txt
```
We follow CEDR's data processing practices, and use [Robust04](https://trec.nist.gov/data/t13_robust.html) for example. After download this dataset, put it in `data/robust04`.
Many of files for training and evaluation are available in `data/robust`.

**qrels**: a standard TREC-style query relevant file. Used for identifying relevant items for
training pair generation and for validation(`data/robust/qrels`).

**train_pairs**: a tab-deliminted file containing pairs used for training. The training process
will only use query-document pairs found in this file(`data/robust/*.pairs`).
File format:

```
[query_id]	[doc_id]
```

**valid_run**: a standard TREC-style run file for re-ranking items for validation(`data/robust/*.run`).

**datafiles**: Files containing the text of queries and documents needed for training, validation,
or testing. Should be in tab-delimited format as follows, where `[type]` is either `query` or `doc`,
`[id]` is the identifer of the query or document (e.g., `132`, `clueweb12-0206wb-59-32292`), and
`[text]` is the textual content of the query or document (no tabs or newline characters,
tokenization done by `BertTokenizer`).

```
[type]  [id]  [text]
```

Queries for WebTrack and Robust are available in `data/robust/queries.tsv`.
Document text can be extracted from an index using `extract_docs_from_index.py` (be sure to use an
index that has appropriate pre-processing). The script supports [Indri](http://www.lemurproject.org/indri/)
indices. See instructions below for help installing [pyndri](https://github.com/cvangysel/pyndri).

Examples:

```
IndriBuildIndex data/robust-manifest.json
awk '{print $3}' data/robust/*.run | python extract_docs_from_index.py indri data/robust_idx > data/robust/documents.tsv
```

## Training LGRe
To train LGRe, first download [pre-trained Vanilla BERT](https://macavaney.us/cedr-models.tar) and placed in `data/cedr-models`, then use the following command:

```
python train.py --fold n
```
Our experiment was conducted on two GTX1080Ti.
# Acknowledgement
Some snippets of the codes are borrowed from 
[NPRF](https://github.com/ucasir/NPRF),
[Capreolus](https://github.com/capreolus-ir/capreolus),
[dl4marco-bert](https://github.com/nyu-dl/dl4marco-bert),
[SIGIR19-BERT-IR](https://github.com/AdeDZY/SIGIR19-BERT-IR),
[CEDR](https://github.com/Georgetown-IR-Lab/cedr).
