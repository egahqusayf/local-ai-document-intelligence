# Local AI Document Intelligence

A Windows-friendly, local-first application for asking grounded questions across one or more PDF documents. The system retrieves relevant passages, generates an answer, and displays the original filename, page number, relevance score, and excerpt as verifiable evidence.

## Repository contents

This repository contains two main files:

```text
local-ai-document-intelligence/
|-- README.md
`-- Local_AI_Document_Intelligence.zip
```

The complete application source code, sample documents, setup scripts, tests, figures, and documentation are stored inside:

```text
Local_AI_Document_Intelligence.zip
```

## Download and extract the project

Before installing or running the application, download and extract the ZIP file.

### Option 1 — Download from GitHub

1. Open this repository.
2. Click `Local_AI_Document_Intelligence.zip`.
3. Click **Download raw file**.
4. Save the ZIP file to your computer.
5. Right-click the downloaded ZIP file.
6. Select **Extract All**.
7. Choose a destination folder.
8. Open the extracted project folder.

After extraction, the folder should contain files such as:

```text
local-ai-document-intelligence/
|-- app.py
|-- src/
|-- sample_docs/
|-- tests/
|-- docs/
|-- .streamlit/
|-- setup_windows.bat
|-- run_app.bat
|-- run_app_light.bat
|-- run_app_dark.bat
|-- run_tests.bat
|-- requirements.txt
`-- requirements-lite.txt
```

> Do not run the application directly from inside the ZIP archive. Extract the project first so Python, the virtual environment, sample documents, and configuration files can be accessed correctly.

### Option 2 — Clone the repository

Clone this repository using Git:

```powershell
git clone <REPOSITORY-URL>
cd <REPOSITORY-FOLDER>
```

Extract `Local_AI_Document_Intelligence.zip`, then enter the extracted project directory:

```powershell
cd Local_AI_Document_Intelligence
```

## Quick start for Windows

After extracting the ZIP file:

1. Install **Python 3.11 or 3.12**.
2. Enable **Add Python to PATH** during installation.
3. Open the extracted project folder.
4. Double-click `setup_windows.bat`.
5. Wait until the virtual environment and dependencies are installed.
6. Double-click `run_app.bat`.
7. Select the preferred display mode.
8. Streamlit will open the application in your browser.

The setup script first attempts to install the complete semantic-search dependencies. If that installation fails, it automatically attempts the lightweight TF-IDF profile.

## Project preview

The following preview images are included inside the extracted ZIP project.

### Grounded question answering

```text
docs/figures/ui_answer_mockup.png
```

### Multi-PDF indexing

```text
docs/figures/ui_index_mockup.png
```

### System architecture

```text
docs/figures/architecture.png
```

## Main features

- Upload and index multiple text-based PDF files.
- Page-aware PDF extraction using PyMuPDF.
- Overlapping chunks that retain filename and page metadata.
- Multilingual semantic retrieval using Sentence Transformers.
- Automatic TF-IDF fallback when the embedding model is unavailable.
- Extractive answering that works without a language model.
- Optional private answer generation through a local Ollama model.
- Source viewer with relevance score, filename, page number, and excerpt.
- Conversation history and Markdown export.
- Bundled sample PDF and automated core tests.
- Windows setup and launch scripts.
- Light and Dark display modes.

## Why this project matters

This project is designed around traceability rather than answer generation alone.

Every retrieved chunk remains associated with its original PDF file and page number. This allows users to inspect the supporting evidence before trusting the generated answer.

The application also remains functional when semantic embeddings or Ollama are unavailable. Users can continue using TF-IDF retrieval and Extractive answering on computers with limited resources.

## Project structure

After extracting the ZIP file, the project structure is:

```text
local-ai-document-intelligence/
|-- app.py
|-- src/
|   |-- answer_engine.py
|   |-- exporter.py
|   |-- models.py
|   |-- ollama_client.py
|   |-- pdf_processor.py
|   `-- retriever.py
|-- sample_docs/
|-- tests/
|-- docs/
|   `-- figures/
|       |-- ui_answer_mockup.png
|       |-- ui_index_mockup.png
|       `-- architecture.png
|-- .streamlit/
|   |-- config.toml
|   |-- config_light.toml
|   `-- config_dark.toml
|-- setup_windows.bat
|-- run_app.bat
|-- run_app_light.bat
|-- run_app_dark.bat
|-- run_tests.bat
|-- requirements.txt
`-- requirements-lite.txt
```

## Windows installation

### Automatic setup

Make sure the project ZIP has already been extracted.

Then:

1. Open the extracted project folder.
2. Double-click `setup_windows.bat`.
3. Wait for the setup process to finish.
4. Double-click `run_app.bat`.
5. Choose the preferred display mode.
6. The application will open in the default browser.

The setup script performs the following operations:

- Checks whether Python is available.
- Creates a virtual environment in `.venv`.
- Upgrades `pip`.
- Installs dependencies from `requirements.txt`.
- Falls back to `requirements-lite.txt` when the full installation fails.

### PowerShell setup

Open PowerShell inside the extracted project folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

When PowerShell blocks virtual-environment activation:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### Lightweight installation

Use the lightweight dependency profile when the computer has limited memory, storage, or processing capability:

```powershell
pip install -r requirements-lite.txt
streamlit run app.py
```

The lightweight profile does not install Sentence Transformers. TF-IDF retrieval, Extractive answering, PDF upload, source viewing, and Markdown export remain available.

## Optional Ollama setup

Extractive mode works without Ollama.

To enable local generative answers:

1. Install Ollama for Windows.
2. Open PowerShell.
3. Download a local model.

```powershell
ollama pull llama3.2:3b
ollama list
ollama run llama3.2:3b
```

Start the Ollama server when necessary:

```powershell
ollama serve
```

Inside the application:

1. Select **Ollama** as the answer mode.
2. Enter the exact installed model name.
3. Keep the default local URL:

```text
http://localhost:11434
```

## How to use

1. Extract `Local_AI_Document_Intelligence.zip`.
2. Install the project dependencies.
3. Start the application.
4. Open **Index documents**.
5. Upload one or more text-based PDF files, or use the bundled sample.
6. Select the retrieval engine and chunk settings.
7. Click **Build document index**.
8. Open **Ask documents**.
9. Enter a specific question.
10. Click **Search and answer**.
11. Review the generated answer.
12. Expand **View retrieved sources**.
13. Verify the filename, page number, relevance score, and evidence excerpt.
14. Export the conversation to Markdown when required.

## Retrieval modes

### Auto

Attempts to load semantic retrieval first. If the embedding model cannot be loaded, the system automatically falls back to TF-IDF.

### Sentence Transformers

Uses multilingual embeddings to retrieve passages based on semantic meaning.

### TF-IDF

Uses lightweight keyword and phrase matching. This mode is suitable for computers with limited resources.

## Answer modes

### Extractive

Selects high-scoring sentences directly from the retrieved evidence.

Advantages:

- Does not require Ollama.
- Uses fewer computer resources.
- Produces answers close to the original text.
- Is easier to verify against the document.

### Ollama

Sends the retrieved evidence to a local language model to generate a more natural answer.

Advantages:

- Runs locally.
- Supports replaceable local models.
- Uses retrieved evidence as the answer context.
- Retains source citation labels such as `[S1]` and `[S2]`.

## Testing

After extracting and installing the project, run:

```powershell
python -m unittest discover -s tests -v
```

Alternatively, double-click:

```text
run_tests.bat
```

The end-to-end test creates a PDF in memory and validates:

- PDF extraction.
- Text chunking.
- TF-IDF retrieval.
- Answer generation.
- Source citation using `[S1]`.

## Ollama timeout

The Ollama client uses separate connection and response timeouts:

```python
timeout=(10, read_timeout)
```

The first value is the connection timeout. The second value is the maximum waiting time for the model response.

For slower CPU-only computers:

- Increase the read timeout.
- Use a smaller Ollama model.
- Reduce the number of evidence sources.
- Reduce the chunk size.
- Run the model once before using it in the application.

## Troubleshooting

### Python is not recognized

Reinstall Python and enable:

```text
Add Python to PATH
```

Check the installation:

```powershell
python --version
```

### Virtual environment is missing

Run:

```text
setup_windows.bat
```

### PDF contains no selectable text

The PDF may be an image-only scanned document. Convert it into a searchable PDF using OCR before uploading it.

### Semantic model cannot be loaded

Use:

```text
Auto
```

or:

```text
TF-IDF
```

### Ollama connection refused

Make sure Ollama is running:

```powershell
ollama serve
```

Check the port:

```powershell
Test-NetConnection localhost -Port 11434
```

### Ollama read timeout

Increase the timeout value, reduce the number of sources, or use a smaller model.

### Streamlit port is already in use

Run the application on another port:

```powershell
streamlit run app.py --server.port 8502
```

## Limitations

- No OCR for image-only PDFs.
- The document index is stored in memory and rebuilt after restart.
- Chunking is based on words and pages rather than document headings.
- No cross-encoder reranker.
- No highlighted evidence inside a PDF viewer.
- Ollama responses are currently non-streaming.
- No authentication or multiuser support.
- No persistent vector database.

## Roadmap

- OCR support.
- Persistent vector storage.
- Cross-encoder reranking.
- Highlighted evidence inside a PDF viewer.
- Streaming local generation.
- Metadata filters.
- Retrieval evaluation dashboard.
- FastAPI backend layer.
- Authentication.
- Docker packaging.

## Technology stack

- Python
- Streamlit
- PyMuPDF
- Scikit-learn
- NumPy
- Sentence Transformers
- Requests
- Ollama

## Privacy

The application is designed to process documents locally.

PDF content, extracted text, retrieval indexes, questions, answers, and evidence remain on the user's computer while the application is running.

Users should still avoid exposing Streamlit to a public network without authentication and should verify retrieved evidence before using answers for important decisions.

## Documentation

The complete project documentation is included inside the extracted ZIP folder.

Look for the documentation files inside:

```text
docs/
```

The documentation explains:

- Project background and objectives.
- Functional and nonfunctional requirements.
- Interface features.
- System architecture.
- PDF extraction and chunking.
- Information retrieval.
- Answer generation and citation.
- Source-code structure.
- Windows installation.
- Ollama configuration.
- Testing.
- Troubleshooting.
- Privacy and security.
- Limitations and roadmap.

## License

This project is provided as a portfolio and educational software project.

Review and add an appropriate license file before redistributing or using the application commercially.