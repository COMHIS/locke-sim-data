# locke-sim-data
This repository provides the official annotated dataset for the NLP4DH 2026 paper: "[Matching Meaning at Scale: Evaluating Semantic Search for 18th-Century Intellectual History through the Case of Locke](https://arxiv.org/pdf/2605.09236)".

🕵 [Interactive Demo](https://receptionreader.com/semantic) — Explore flexible and multilingual semantic search across 18th-century historical texts.

## Introduction
While digitized corpora have transformed the study of intellectual transmission, current methods rely heavily on lexical text reuse detection, capturing verbatim quotations but fundamentally missing paraphrases and complex implicit engagement. This paper evaluates semantic search in 18th-century intellectual history through the reception of John Locke's foundational work. Using expert annotation grounded in a semantic taxonomy, we examine whether an off-the-shelf semantic search pipeline can surface meaning-level correspondences overlooked by lexical methods. Our results demonstrate that semantic search retrieves substantially more implicit receptions than lexical baselines. However, linguistic diagnostics also reveal a "lexical gatekeeping" effect, where retrieval remains partially constrained by surface vocabulary overlap. These findings highlight both the potential and the limitations of semantic retrieval for analyzing the circulation of ideas in large historical corpora.

In this repository, we share the annotated dataset used in the paper, which includes manual annotation results for three rounds of evaluation, along with bibliographic metadata for the final set of hits. The dataset is intended to support further research on semantic search evaluation and intellectual history analysis.


## Contents

The dataset is provided as CSV files. The first two files contain manual annotation results for semantic-search candidates, while the four `3rd_*` files split into two different pipelines: the `*_reuse_*` files contain direct lexical reuse retrieval results, and the `*_semantic_*` files contain unique semantic-search candidate results with manual annotations and bibliographic metadata.

Taken together, these files support the analyses reported in Sections 5.1 and 5.4, Figure 5, and Figures 6 and 7 of the paper.

- `1st_annotation_quotes_1000_R22993_34459614_meta_with_results.csv`: manual annotation results for the first exploratory 1,000 unique semantic hit candidates for Locke quotes.
- `2nd_top_200_sampled_annotation_quotes_R22993_34459614_meta_with_results.csv`: manual annotation results for a sampled top-200 subset of hit candidates, focusing on the three most representative quotes: 0, 33, and 464. 50 candidates for each quote were annotated.
- `3rd_quote_33_reuse_hits_w_estc_unique_work.csv`: all lexical reuse matches for quote 33, with ESTC work metadata.
- `3rd_quote_33_semantic_hits_w_estc_unique_work.csv`: top-200 unique semantic hit candidates for quote 33, with ESTC work metadata.
- `3rd_quote_464_reuse_hits_w_estc_unique_work.csv`: lexical reuse matches for quote 464, with ESTC work metadata.
- `3rd_quote_464_semantic_hits_w_estc_unique_work.csv`: top-200 unique semantic hit candidates for quote 464, with ESTC work metadata.


## Dataset format

### Annotation files

The files `1st_annotation_quotes_1000_R22993_34459614_meta_with_results.csv` and `2nd_top_200_sampled_annotation_quotes_R22993_34459614_meta_with_results.csv` share the same columns:

- `hitIndex`: index of the retrieved hit in the ranked result list.
- `hitDocId`: ECCO identifier of the document containing the hit.
- `hitStart`: start character offset of the hit span in the hit document.
- `hitEnd`: end character offset of the hit span in the hit document.
- `score`: similarity score assigned to the hit by the model.
- `quoteIndex`: index of the source Locke quote.
- `quoteStart`: start character offset of the quote span in the source document.
- `quoteEnd`: end character offset of the quote span in the source document.
- `quoteDocId`: EEBO identifier of the source quote document.
- `workCount`: number of lexically reused works associated with the quote.
- `quoteMeta`: metadata tag for the quote, used for grouping or filtering.
- `hitMeta`: metadata tag for the hit, used for grouping or filtering.
- `quoteText`: text of the original Locke quote.
- `hitText`: matched passage text by the model.
- `result`: manual annotation label for the pair. Labels are encoded by the first letter of each class: `P` = `Paraphrase`, `M` = `Meaning Match`, `T` = `Topical`, `N` = `No Match`, and `D` = `Don't Know`.
- `annotator`: identifier of the annotator who assigned the label.

The files `3rd_quote_33_reuse_hits_w_estc_unique_work.csv` and `3rd_quote_464_reuse_hits_w_estc_unique_work.csv` list lexical reuse matches retrieved directly from the reuse pipeline to be compared with the semantic-search results in the third round. They do not include manual annotations. Their columns are:

- `quoteIndex`: index of the source Locke quote.
- `quoteText`: text of the source quote.
- `hitDocId`: ECCO identifier of the matched document.
- `hitText`: matched passage text by the model.
- `hitStart`: start character offset of the hit span.
- `hitEnd`: end character offset of the hit span.
- `simScore`: similarity score assigned by the model.
- `hitResult`: label assigned to the hit, such as `Reuse`.
- `estc_id`: ESTC identifier of the matched work.
- `main_category`: broad subject category of the work.
- `full_title`: full bibliographic title.
- `work_id`: unique work identifier for different publications of the same work.
- `publication_year`: year of publication.
- `language`: language of the work.
- `publication_place`: place of publication.
- `primary_author`: primary author of the work.

The files `3rd_quote_33_semantic_hits_w_estc_unique_work.csv` and `3rd_quote_464_semantic_hits_w_estc_unique_work.csv` contain unique semantic hit candidates together with manual annotations and bibliographic metadata. Their columns are:

- `quoteIndex`: index of the source Locke quote.
- `quoteText`: text of the source quote.
- `hitDocId`: ECCO identifier of the matched document.
- `hitText`: matched passage text by the model.
- `hitStart`: start character offset of the hit span.
- `hitEnd`: end character offset of the hit span.
- `simScore`: semantic similarity score assigned by the model.
- `hitResult`: label assigned to the hit, such as `Paraphrase`, `Meaning Match`, `Topical`, `No Match`, or `Don't Know`.
- `estc_id`: ESTC identifier of the matched work.
- `main_category`: broad subject category of the work.
- `full_title`: full bibliographic title.
- `work_id`: unique work identifier for different publications of the same work.
- `publication_year`: year of publication.
- `language`: language of the work.
- `publication_place`: place of publication.
- `primary_author`: primary author of the work.

### Access the page images

To inspect the ECCO page image for a specific hit, open the page-view API with the hit document ID and character offsets:

```text
https://onko-sivu.2.rahtiapp.fi/ecco?docId=<hitDocId>&offsetStart=<hitStart>&offsetEnd=<hitEnd>
```

For example, the hit 0177400800 at offsets 390967-391346 can be viewed at:

```text
https://onko-sivu.2.rahtiapp.fi/ecco?docId=0177400800&offsetStart=390967&offsetEnd=391346
```

The selected span is highlighted in the page image, so readers can read the matched passage with the surrounding ECCO context.


## License
This work is licensed under the Creative Commons Attribution-NonCommercial 4.0 International License.


## Citation
If you use this dataset, please cite the associated paper. BibTeX will be provided upon publication.


## Contact
For questions, please open an issue or contact the authors at yu.wu@helsinki.fi.
