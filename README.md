# langchain-rag-demo

A hands-on Jupyter notebook that builds a RAG pipeline over a PDF using **LangChain**, **Chroma**, local **Hugging Face** embeddings, and **Google Gemini** for generation.

**YouTube walkthrough:** [Watch the tutorial](https://youtu.be/S52GEPIYb40)

The sample document (`resistor.pdf`) covers resistor types, color codes, and applications. You can swap in any PDF of your own.

## What it does

1. Loads a PDF with `PyPDFLoader`
2. Splits text into overlapping chunks
3. Embeds chunks with `sentence-transformers/all-MiniLM-L6-v2`
4. Stores vectors in Chroma and retrieves relevant context for a question
5. Answers with Gemini, grounded only on retrieved context

## Stack

| Piece | Choice |
| --- | --- |
| LLM | Google Gemini (`gemma-4-31b-it` via LangChain) |
| Embeddings | Hugging Face `all-MiniLM-L6-v2` |
| Vector store | Chroma |
| Framework | LangChain |
| Package manager | [uv](https://github.com/astral-sh/uv) |

## Prerequisites

- Python **3.13+**
- [uv](https://docs.astral.sh/uv/) (recommended) or pip
- A [Google AI Studio](https://aistudio.google.com/apikey) API key

## Setup

```bash
# Clone the repo
git clone https://github.com/Tech-Watt/langchain-rag-demo.git
cd langchain-rag-demo

# Install dependencies
uv sync

# Configure your API key
cp .env.example .env
# Edit .env and set GOOGLE_API_KEY
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
# Then open .env and paste your key
```

## Run the notebook

```bash
uv run jupyter notebook rag.ipynb
```

Or open `rag.ipynb` in VS Code / Cursor and select the project’s `.venv` as the kernel.

Run the cells in order. The final cell asks: *“what are the types of resistors?”* and prints a context-grounded answer.

## Project layout

```
langchain-rag-demo/
├── rag.ipynb          # Full RAG walkthrough
├── resistor.pdf       # Sample knowledge source
├── .env.example       # API key template (safe to commit)
├── pyproject.toml     # Dependencies
└── uv.lock            # Locked versions
```

## Customize

- **Your own PDF** — change `dataPath` in the notebook to another `.pdf` in the project root.
- **Chunking** — adjust `chunk_size` / `chunk_overlap` on `RecursiveCharacterTextSplitter`.
- **Model** — change the `model` argument on `ChatGoogleGenerativeAI`.
- **Prompt** — edit `system_prompt` to change how the assistant uses context.

## Security

- Never commit `.env`. It is listed in `.gitignore`.
- Only `.env.example` (with a placeholder) should be in the repo.
- If an API key was ever shared or committed, revoke it in Google AI Studio and create a new one.

## License

Use and modify freely for learning and demos. Add a formal license file if you publish this as an open-source project.
