# Minority Language AI Interactive Learning Platform – The Case of Siouguluan Amis Language

This project provides an interactive **Chinese -> Amis** translation interface. It uses `Gradio` for the web UI, Chinese embedding models for semantic representation, and `FAISS` for nearest-neighbor retrieval from a bilingual dictionary.

## Features
- Real-time translation from Chinese input
- Semantic embeddings via `jinaai/jina-embeddings-v2-base-zh`
- Fast vector search with `FAISS`
- Word-level segmentation with `jieba`
- Pinyin fallback with `pypinyin` when confidence is low
- One-command startup with Docker

## How It Works
1. Load dictionary data from `doc/dict-zh-amis.xlsx`.
2. Compute embeddings for Chinese entries and build a `FAISS` index.
3. Save generated artifacts:
   - `doc/zh_embeddings.index`
   - `doc/amis_mappings.pkl`
4. For user input, run sentence-level retrieval and optionally word-level retrieval.
5. If no confident match is found, return pinyin-based fallback output.

## Project Structure
```text
AI-Project/
├─ app.py                     # Gradio entry point
├─ src/
│  ├─ gen_dict.py             # Build dictionary embeddings and index
│  ├─ get_model.py            # Load tokenizer/model and path settings
│  └─ translate.py            # Translation pipeline
├─ doc/
│  └─ dict-zh-amis.xlsx       # Chinese-Amis dictionary
├─ requirements.txt
├─ dockerfile
└─ compose.yaml
```

## Requirements
- Python 3.10+ (recommended)
- Docker / Docker Compose (recommended)

## Quick Start (Docker, Recommended)
```bash
docker compose up -d --build
```
Then open: `http://localhost:7860`

Stop and clean:
```bash
docker compose down -v --rmi all
```

## Local Run (Without Docker)
```bash
pip install -r requirements.txt
python app.py
```

## Notes
- The current path settings in code are container-based (`/app/...`), defined in `src/get_model.py`.
- If you run locally, make sure these paths are valid on your machine, or update them accordingly.

## Research / Training Reference
- Colab: https://colab.research.google.com/drive/1vrkRt4QuIxehGeQKRRDML92yEOJFdjR5?usp=sharing

## Team
- CS 4 [Yu-Zhi Pan](https://github.com/YCNeo718)
- CS 3 [Rong-Rong Huang](https://github.com/Zhong220)

