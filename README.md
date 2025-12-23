# QueryBridge  
### A Million-Scale Dataset for Knowledge-Graph Question Answering (KGQA)

🌐 **Dataset Website:** https://aorogat.github.io/QueryBridge/  
🤗 **Hugging Face Dataset:** aorogat/QueryBridge  
📄 **Conference:** CIKM 2025  

---

## Overview

**QueryBridge** is a large-scale, research-grade dataset designed to address the long-standing **data scarcity problem in Knowledge-Graph Question Answering (KGQA)**.

The dataset contains **1,004,534 natural language questions**, each paired with an **executable SPARQL query** over **DBpedia**. Every question is enriched with **structural metadata**, **semantic tags**, and **verified answers**, enabling both **end-to-end** and **component-level** evaluation of KGQA systems.

QueryBridge is generated using the **Maestro** framework, ensuring reproducibility, structural diversity, and scalability.

---

## Key Contributions

- **Million-scale benchmark** (1.0M+ NL–SPARQL pairs)
- **Executable SPARQL queries** with verified answers
- **Deep semantic annotation** linking natural language tokens to SPARQL components
- **Rich query-shape taxonomy** (Star, Chain, Tree, Cycle, Set-shape, etc.)
- **Explicit complexity metadata** enabling controlled experiments
- **Native Hugging Face integration** for efficient loading and filtering

---

## Dataset Schema

Each record in QueryBridge includes the following core fields:

| Field | Description |
|------|------------|
| `questionString` | Raw natural language question |
| `questionStringTagged` | Token-level semantic alignment (NL ↔ SPARQL) |
| `query` | Executable SPARQL query |
| `shapeType` | Structural query pattern |
| `questionComplexity` | Normalized complexity score |
| `answerCardinality` | Number of gold answers |
| `answers` | Verified answer set |

---

## Usage via Hugging Face

QueryBridge is distributed using the 🤗 `datasets` library.

```python
from datasets import load_dataset

# Load the full dataset (≈1M question–SPARQL pairs)
dataset = load_dataset("aorogat/QueryBridge")

# Inspect dataset fields
print(dataset["train"].column_names)

# Filter by query structure
star_queries = dataset["train"].filter(
    lambda ex: ex["shapeType"] == "STAR"
)

# Access semantic supervision
sample = dataset["train"][0]
print(sample["questionStringTagged"])
print(sample["query"])
```

The Hugging Face interface supports streaming, caching, and integration with PyTorch, TensorFlow, and JAX pipelines.

---

## Research Applications

QueryBridge supports a broad range of research tasks:

- End-to-end KGQA (NL → SPARQL → Answers)
- Semantic parsing and structured query generation
- Entity and relation linking
- Multi-hop and compositional reasoning
- LLM-based KGQA and agent-based pipelines
- Controlled ablation and complexity studies

---

## Benchmark Generation with Maestro

QueryBridge is generated using **Maestro**, a reproducible framework for automatic benchmark construction over knowledge graphs.

Maestro follows a deterministic three-stage pipeline:

1. **Seed Selection** – Representative sampling of entities and classes  
2. **Query Shape Instantiation** – Structural patterns such as Star, Chain, Tree, Cycle  
3. **Lexicalization** – Mapping graph patterns to natural language questions  

This design enables QueryBridge to be **regenerated**, **extended**, or **ported** to other knowledge graphs.

---

## Citation

If you use **QueryBridge**, **Maestro**, or any derived resources, please cite the following publications.

### QueryBridge

```bibtex
@inproceedings{orogat2025querybridge,
  title     = {QueryBridge: One Million Annotated Questions with SPARQL Queries},
  author    = {Orogat, Abdelghny and El-Roby, Ahmed},
  booktitle = {Proceedings of the 34th ACM International Conference on Information and Knowledge Management (CIKM)},
  year      = {2025},
  doi       = {10.1145/3746252.3761623}
}
```

### Maestro

```bibtex
@article{orogat2023maestro,
  title   = {Maestro: Automatic Generation of Comprehensive Benchmarks for Question Answering Over Knowledge Graphs},
  author  = {Orogat, Abdelghny and El-Roby, Ahmed},
  journal = {Proceedings of the ACM on Management of Data},
  year    = {2023},
  doi     = {10.1145/3589322}
}
```

---

## License

QueryBridge is released for **research and academic use**.  
Please consult the dataset website for licensing and usage terms.

---

## Authors

- **Abdelghny Orogat** – Carleton University  
- **Ahmed El-Roby** – Carleton University  

---

## Contact

For questions, feedback, or collaboration inquiries:

**Abdelghny Orogat**  
Carleton University, Ottawa, Canada
