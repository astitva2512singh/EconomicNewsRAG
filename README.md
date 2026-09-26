# AI-Driven Macroeconomic News Intelligence System

This project turns financial news and selected macroeconomic indicators into timely, ranked intelligence for monitoring emerging-market regime shifts. It combines data ingestion, natural-language processing, retrieval-augmented generation (RAG), and a lightweight analyst-facing interface.

## Project goals

- Collect and normalize daily financial news and macroeconomic time series.
- Filter, tag, embed, and rank news by relevance, recency, source quality, and macroeconomic context.
- Retrieve grounded evidence for a country, topic, or macro-risk question.
- Present concise signals with source attribution and a clear explanation of supporting evidence.

## Expected results

The finished system should provide a searchable news corpus, topic/country tags, daily ranked signals, retrieval-quality evaluation, and a user interface that cites the underlying articles and indicators.

## Repository layout

```text
.
├── README.md
├── requirements.txt                 # Python package versions
├── .env.example                     # Names only for required API keys; no real secrets
├── .gitignore                       # Ignore .env, data, vector stores, and local artifacts
├── configs/
│   ├── sources.yaml                 # News feeds and macro-series metadata
│   ├── pipeline_config.yaml         # Chunking, ranking, and refresh settings
│   └── evaluation_config.yaml       # Retrieval and signal-quality criteria
├── data/
│   ├── raw/                         # Original news/API responses and macro downloads
│   ├── interim/                     # Normalized articles and cleaned time series
│   ├── processed/                   # Chunks, labels, and final feature tables
│   └── evaluation/                  # Curated question-answer and relevance sets
├── docs/
│   ├── architecture.md              # System components and data flow
│   ├── data_dictionary.md           # Source, field, and license documentation
│   ├── methodology.md               # NLP, ranking, and RAG choices
│   ├── evaluation.md                # Metrics and human-review protocol
│   └── results.md                   # Final system quality and examples
├── notebooks/
│   ├── 01_source_exploration.ipynb  # News and macro-series assessment
│   ├── 02_nlp_experiments.ipynb     # Tagging, embeddings, and ranking experiments
│   └── 03_rag_evaluation.ipynb      # Retrieval and answer-grounding review
├── src/
│   ├── ingestion/
│   │   ├── fetch_news.py            # News collection and normalization
│   │   └── fetch_macro.py           # Macro-series retrieval and cleaning
│   ├── processing/
│   │   ├── clean_text.py            # Deduplication and text preparation
│   │   ├── tag_articles.py          # Country, topic, and risk tagging
│   │   └── build_chunks.py          # Retrieval chunk creation
│   ├── retrieval/
│   │   ├── index.py                 # Vector-index build/update entry point
│   │   ├── retrieve.py              # Evidence retrieval and reranking
│   │   └── rag.py                   # Grounded answer orchestration
│   ├── signals/
│   │   ├── rank.py                  # Recency, relevance, and impact ranking
│   │   └── detect_regimes.py        # Macro-signal generation logic
│   ├── evaluation/
│   │   └── evaluate.py              # Retrieval and grounding measurements
│   └── ui/
│       └── app.py                   # Streamlit analyst interface
├── vector_store/                    # Local retrieval index; excluded from Git
├── outputs/
│   ├── signals/                     # Daily ranked signal tables
│   ├── figures/                     # Trend and evaluation charts
│   └── reports/                     # Generated summaries with citations
└── tests/
    ├── test_processing.py           # Cleaning, tagging, and chunking checks
    ├── test_retrieval.py            # Retrieval relevance checks
    └── test_signals.py              # Ranking and signal-rule checks
```

## Data sources and attribution

Use licensed news sources or APIs and publicly available macroeconomic data providers. Keep credentials only in a local `.env` file, list required variable names in `.env.example`, and record each source's license, access terms, and refresh frequency in `docs/data_dictionary.md`.

Do not commit full copyrighted article content without permission. Store only the fields permitted by each source, preserve source URLs and publication metadata, and display citations in every generated analyst-facing answer.

## System workflow

1. Ingest news articles and macroeconomic series on a documented schedule.
2. Deduplicate, normalize, tag, and chunk article text.
3. Create embeddings and update the local vector index.
4. Rank candidate news using recency, topic relevance, source quality, and macro context.
5. Retrieve evidence for an analyst question, generate a grounded summary, and show the supporting sources.
6. Evaluate retrieval relevance, citation coverage, and unsupported-claim rate using a small human-reviewed set.

## Reproducibility checklist

- Pin libraries in `requirements.txt` and record model versions.
- Put source, chunking, ranking, and evaluation settings in `configs/`.
- Keep secrets, downloaded corpora, and vector indexes out of Git.
- Separate experimental notebooks from reusable modules in `src/`.
- Never present a generated summary without clear source attribution.

## Future deliverables

- An architecture diagram and data-flow explanation in `docs/architecture.md`.
- A small annotated evaluation set in `data/evaluation/`.
- A Streamlit analyst dashboard built from `src/ui/app.py`.
