# Examina CLI

Local command-line tool for AI-powered exam preparation. Run offline with vector store for semantic search.

## Architecture

```
examina (core)        - Lightweight business logic
    ↓ used by
examina-cloud         - Web platform (FastAPI + React + PostgreSQL)
examina-cli           - Local CLI tool (this repo)
```

## Features

- **Local Vector Store** - ChromaDB for semantic search
- **Offline Mode** - Study without internet
- **Exercise Analysis** - Extract knowledge items from PDFs
- **Concept Mapping** - Visualize knowledge dependencies
- **FSRS Scheduling** - Spaced repetition for retention
- **Quiz Generation** - Practice with AI-generated questions
- **Solution Separation** - Split exercises from solutions
- **Deduplication** - Merge duplicate knowledge items

## Installation

```bash
# Clone the repo
git clone https://github.com/madebymlai/examina-cli.git
cd examina-cli

# Install dependencies (includes heavy ML deps)
pip install -r requirements.txt

# Install core library
pip install git+https://github.com/madebymlai/examina.git
```

## Usage

```bash
# Initialize database
python cli.py init

# List available courses
python cli.py courses --degree "Computer Science"

# Course info
python cli.py info --course MATH101

# Import and analyze PDFs
python cli.py ingest --course MATH101 --pdf /path/to/exam.pdf
python cli.py analyze --course MATH101

# Study commands
python cli.py learn --course MATH101 --loop "Linear Algebra Basics"
python cli.py practice --course MATH101 --topic "Derivatives"
python cli.py quiz --course MATH101 --questions 10

# Visualization
python cli.py concept-map --course MATH101
python cli.py concept-graph --course MATH101

# Progress tracking
python cli.py progress --course MATH101
python cli.py suggest --course MATH101

# Utilities
python cli.py search --course MATH101 --tag "integration"
python cli.py deduplicate --course MATH101 --dry-run
python cli.py separate-solutions --course MATH101
python cli.py rate-limits --provider deepseek
```

## Commands

| Command | Purpose |
|---------|---------|
| `init` | Initialize database and load course catalog |
| `courses` | List courses by degree |
| `info` | Show course details |
| `ingest` | Import PDF exercises |
| `analyze` | Extract knowledge items from exercises |
| `learn` | Study a core loop |
| `practice` | Practice specific topics |
| `quiz` | Take a quiz |
| `prove` | Prove theorems interactively |
| `progress` | View learning progress |
| `suggest` | Get study suggestions |
| `concept-map` | Generate concept dependency map |
| `concept-graph` | Visualize knowledge graph |
| `search` | Search exercises and topics |
| `deduplicate` | Merge duplicate knowledge items |
| `separate-solutions` | Split exercises from solutions |
| `rate-limits` | View/reset LLM rate limits |

## Structure

```
examina-cli/
├── cli.py              # Main CLI entry point
├── config.py           # Configuration
├── storage/
│   ├── database.py     # SQLite database
│   ├── file_manager.py # PDF storage
│   └── vector_store.py # ChromaDB embeddings
├── scripts/            # Utility scripts
└── requirements.txt    # Dependencies
```

## Dependencies

Heavy dependencies (why this is separate from core):
- `chromadb` - Vector database
- `sentence-transformers` - Embedding models
- `faiss-cpu` - Similarity search
- `click` - CLI framework
- `rich` - Terminal formatting
- `pymupdf`, `pdfplumber` - PDF processing

## Related

- [examina](https://github.com/madebymlai/examina) - Core library
- [examina-cloud](https://github.com/madebymlai/examina-cloud) - Web platform

## License

MIT License
