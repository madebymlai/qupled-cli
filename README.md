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
- **Adaptive Learning** - Personalized study paths
- **Spaced Repetition** - SM2 algorithm for retention

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
# Import a course PDF
python cli.py import /path/to/course.pdf --course-code MATH101

# Start a study session
python cli.py study MATH101

# Take a quiz
python cli.py quiz MATH101

# View learning path
python cli.py learn MATH101

# Check mastery
python cli.py stats MATH101
```

## Structure

```
examina-cli/
├── cli.py              # Main CLI entry point
├── vector_store.py     # ChromaDB vector store
├── storage/            # Database and embeddings
├── examples/           # Example scripts
└── scripts/            # Utility scripts
```

## Dependencies

Heavy dependencies (why this is separate from core):
- `chromadb` - Vector database
- `sentence-transformers` - Embedding models
- `faiss-cpu` - Similarity search
- `click` - CLI framework
- `rich` - Terminal formatting

## Related

- [examina](https://github.com/madebymlai/examina) - Core library
- [examina-cloud](https://github.com/madebymlai/examina-cloud) - Web platform

## License

MIT License
