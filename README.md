# Curio App

A Python 3.11 web app built with FastAPI and LangChain/LangGraph (Google Gemini), using Chroma for vector storage, Tavily for web search, and SQLite for persistence.

## Tech stack

| Area | Packages |
| --- | --- |
| Web server | `fastapi`, `uvicorn`, `jinja2`, `python-multipart` |
| Config | `python-dotenv` |
| LLM / agents | `langchain`, `langchain-core`, `langchain-google-genai`, `langgraph`, `langgraph-checkpoint-sqlite` |
| Documents / RAG | `langchain-text-splitters`, `langchain-chroma`, `chromadb`, `pypdf`, `docx2txt` |
| Web search | `langchain-tavily`, `tavily-python` |
| Database | `sqlalchemy` |

Exact versions are pinned in `requirements.txt`.

## Environment setup (macOS, Apple Silicon)

This project uses **conda** (via Miniforge) to manage the Python environment.

### 1. Install conda (Miniforge)

conda was not installed on this machine at first, so `conda create` failed with:

```
zsh: command not found: conda
```

Fix: install Miniforge, a small conda distribution that uses the `conda-forge` channel by default:

```sh
brew install --cask miniforge
```

It installs to `/opt/homebrew/Caskroom/miniforge/base`.

> **Note on slow downloads:** Homebrew downloads the Miniforge installer (~87 MB) from GitHub release servers, which were very slow (~50–75 KB/s) even on a fast connection, while other servers downloaded at several MB/s. If this happens again, the same installer can be downloaded directly from a mirror, e.g.
> `https://mirrors.tuna.tsinghua.edu.cn/github-release/conda-forge/miniforge/LatestRelease/Miniforge3-MacOSX-arm64.sh`
> and installed with `bash Miniforge3-MacOSX-arm64.sh`.

### 2. Hook conda into zsh

macOS uses **zsh** by default, so conda must be initialized **for zsh**:

```sh
/opt/homebrew/Caskroom/miniforge/base/bin/conda init zsh
source ~/.zshrc
```

> **Gotcha:** running plain `conda init` (with no shell name) set up **bash** instead (it modified `~/.bash_profile`). zsh never reads that file, so `conda activate` kept failing with:
>
> ```
> CondaError: Run 'conda init' before 'conda activate'
> ```
>
> Always use `conda init zsh`. The bash change is harmless; undo it with `conda init --reverse bash` if you like.

### 3. Create and activate the environment

```sh
conda create -n curio python=3.11 -y
conda activate curio
python --version   # Python 3.11.18
```

The environment lives at `/opt/homebrew/Caskroom/miniforge/base/envs/curio`.

### 4. Install dependencies

With the `curio` environment active:

```sh
pip install -r requirements.txt
```

### 5. Environment variables

Secrets go in a `.env` file in the project root (loaded with `python-dotenv`). It is git-ignored and must never be committed. Expected keys:

```
GOOGLE_API_KEY=your-gemini-api-key
TAVILY_API_KEY=your-tavily-api-key
```

## Daily workflow

```sh
cd ~/Documents/curio-app
conda activate curio
```

To leave the environment: `conda deactivate`.

## Progress log

- Set up a git repository on `main`.
- Added `requirements.txt` with pinned versions of the FastAPI, LangChain/LangGraph, Chroma, and Tavily dependencies.
- Installed conda through Homebrew's Miniforge cask.
- Initialized conda for zsh (after fixing the `conda init` bash/zsh mix-up).
- Created the `curio` conda environment with Python 3.11.18.
- Added this README and a `.gitignore`.
