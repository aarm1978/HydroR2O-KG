# HydroR2O-KG

**HydroR2O-KG** is a research prototype that integrates a Large Language Model (LLM) with a domain-specific Knowledge Graph (KG) to support structured synthesis and querying of hydrological literature. The system combines symbolic knowledge extracted from peer-reviewed studies with generative capabilities from GPT-based models to enable transparent, evidence-grounded responses to hydrology-specific queries.

## ⚙️ Requirements

Before running the notebooks, ensure you have the following installed:

- [Ollama](https://ollama.com/) with **Llama 3.1 70B** model
- [Neo4j](https://neo4j.com/) desktop or server, with a database named `hydrologykg`
- [MinerU](https://github.com/opendatalab/MinerU.git) for converting PDF papers into Markdown
- OpenAI API access (with GPT-4.1 and GPT-4o availability)

All Python dependencies are listed in [`requirements.txt`](./requirements.txt).

## 🔐 Environment Configuration

Create a `.env` file in the root directory with the following fields:

```env
# OpenAI API Key
OPENAI_API_KEY=your_openai_api_key_here

# Neo4j connection settings
NEO4J_URI=bolt://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_neo4j_password_here
NEO4J_DB=hydrologykg
```

## 📂 Folder Structure

```
.
├── Houston_pdfs/             # Folder where manually downloaded PDFs are stored
├── Paper_KGs/                # Output folder for paper-specific KGs
├── extracted_results_with_context.json
├── entity_examples.json
├── ontology.txt
├── entities.json
├── relationships.json
├── metadata.json
├── requirements.txt
├── .env
└── *.ipynb                   # Jupyter notebooks listed below
```

## 🧪 Notebooks Overview

| Notebook | Description |
|----------|-------------|
| `01_create_SQL_DB.ipynb`              | Downloads and processes the full WOS dataset from the Miao et al. paper into a local SQLite DB. |
| `02_augment_SQL_DB.ipynb`            | Adds study area, timeframe, and hydrology relevance using Llama 3.1 70B via Ollama. |
| `03_select_papers.ipynb`             | Filters 153 region-specific papers (e.g., Houston, Galveston Bay) and exports structured metadata. |
| `04_convert_to_markdown.ipynb`       | Converts PDFs to Markdown using MinerU. |
| `05_extract_structured_content.ipynb`| Extracts 19 thematic categories per paper using GPT-4o. |
| `06_extract_entities_and_relationships.ipynb` | Extracts ontology-aligned entities and relationships using few-shot prompting and OpenAI API. |
| `07_load_to_neo4j.ipynb`             | Loads all entity-relation triples into Neo4j and generates vector embeddings for semantic search. |
| `08_rag_response.ipynb`              | Implements a RAG pipeline to answer user queries by retrieving semantically similar nodes/edges and prompting GPT-4o with contextual support. |

## 📘 Notes

- PDFs of selected papers must be downloaded manually and placed in `Houston_pdfs/`, each named by `IDPaper`. For example, paper `753` should be saved as `753.pdf`.
- **Do not upload** any non-Open Access PDFs or copyrighted content to the repository.
- The RAG responses generated in `08_rag_response.ipynb` are designed for experimental use only.

## 📎 Citation

If you use or extend this project, please cite:

**HydroR2O-KG: Hydrological Research-to-Operations Knowledge Graph**  
Andrés Ramírez Molina and Saide Zand  
GitHub repository: [https://github.com/aarm1978/HydroR2O-KG](https://github.com/aarm1978/HydroR2O-KG)

BibTeX:

```bibtex
@misc{ramirez2024hydror2okg,
  author       = {Andrés Ramírez Molina and Saide Zand},
  title        = {HydroR2O-KG: Hydrological Research-to-Operations Knowledge Graph},
  year         = {2024},
  url          = {https://github.com/aarm1978/HydroR2O-KG},
  note         = {GitHub repository}
}
```

## 📫 Contact

For questions or feedback, please open an issue or contact [Andrés Ramírez Molina](https://github.com/aarm1978).
```

