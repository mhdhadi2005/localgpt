# LocalGPT

<div align="center">

**LocalGPT is an open-source API layer that turns local models into production AI applications.**

</div>

Running a model locally is only the first step. To build useful AI applications you need a set of higher-level building blocks. LocalGPT provides that layer as an open-source API following the Claude API model — so you can build private AI products without rebuilding the same backend primitives from scratch, and without depending on cloud APIs.

```text
Your app / agent / workflow / UI
              |
        LocalGPT API
              |
OpenAI-compatible inference server
 (Ollama, llama.cpp, vLLM, …)
```

LocalGPT does not run models itself. It connects to any OpenAI-compatible inference server via `OPENAI_API_BASE`. If it implements `/v1/chat/completions` and `/v1/models`, it works.

LocalGPT ships a built-in workbench UI for testing and demos, available at `/ui`. The API is the actual product.

## What LocalGPT gives you

- Standard messages API (streaming, async, token counting)
- File and artifact ingestion
- Retrieval with citations and agentic RAG
- Built-in tools mirroring the Claude API (web search, web fetch, code execution)
- Custom tools and MCP connectors
- Structured access to databases and CSVs
- Embeddings and orchestration

## Quickstart

For Docker, full installation options, and model configuration, see the full Quickstart guide.

**Prerequisites:** You need a running OpenAI-compatible LLM server. [Ollama](https://ollama.com/) is the easiest starting point.

### 1. Install LocalGPT

```bash
# Linux / macOS
curl -LsSf https://astral.sh/uv/install.sh | sh

uv tool install --python 3.11 \
  "private-gpt[core]"
```

```powershell
# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

uv tool install --python 3.11 `
  "private-gpt[core]"
```

> The current implementation still uses the `private-gpt` package/CLI internally.

### 2. Start your LLM server

```bash
# Example with Ollama
ollama pull qwen3.5:35b
ollama pull mxbai-embed-large
ollama serve
```

### 3. Run LocalGPT

```bash
# macOS / Linux
OPENAI_API_BASE=http://localhost:<llm-port>/v1 \
  OPENAI_EMBEDDING_API_BASE=http://localhost:<embedding-port>/v1 \
  private-gpt serve
```

```powershell
# Windows (PowerShell)
$env:OPENAI_API_BASE = "http://localhost:<llm-port>/v1"
$env:OPENAI_EMBEDDING_API_BASE = "http://localhost:<embedding-port>/v1"
private-gpt serve
```

### 4. Open the UI

Go to [http://localhost:8080/ui](http://localhost:8080/ui).

The API is available at `http://localhost:8080`.

<img src="./fern/docs/assets/ui.png" alt="LocalGPT UI" />

The UI is useful for:

- Sending messages
- Selecting models from `/v1/models`
- Uploading documents
- Testing retrieval with citations
- Enabling tools per chat
- Configuring databases, MCP connectors, skills, and custom tools
- Inspecting requests and responses through the API Debugger

## Integrations

LocalGPT works natively as the local backend for the tools developers and end users already use.

| Tool | Use case |
|---|---|
| Claude Code | Local AI coding assistant in the terminal |
| Claude Desktop / Cowork | Connect desktop workflows to your private models |
| Microsoft 365 | Run private AI inside Word, Excel, Outlook, and PowerPoint |
| OpenCode | Local AI coding assistant |
| VS Code | Developer workflow integration |
| Cline | AI-assisted development |

Any tool that works with a local OpenAI-compatible provider can also work with LocalGPT.

## Claude API compatibility

LocalGPT follows the Claude API as the reference for modern AI application APIs.

| Area | Capability | Claude API | LocalGPT |
|---|---|:---:|:---:|
| Models | Model selection | ✅ | ✅ |
| Messages | Messages API | ✅ | ✅ |
| Messages | Streaming | ✅ | ✅ |
| Messages | Batch / async processing | ✅ | ✅ async |
| Messages | Token counting | ✅ | ✅ |
| Knowledge | Files / artifacts | ✅ | ✅ |
| Knowledge | PDF and document ingestion | ✅ | ✅ |
| Knowledge | Retrieval with citations | ✅ | ✅ |
| Knowledge | Embeddings | ✅ | ✅ |
| Tools | Tool use | ✅ | ✅ |
| Tools | Tools in streaming | ✅ | ✅ |
| Tools | Built-in web search | ✅ | ✅ |
| Tools | Web extraction / fetch | ✅ | ✅ |
| Tools | Custom tools | ✅ | ✅ |
| Data | Database querying | Via tools | ✅ built-in |
| Data | CSV / tabular analysis | Via tools / code | ✅ built-in |
| Agents | MCP in the API | ✅ | ✅ |
| Agents | Remote MCP servers | ✅ | ✅ |
| Agents | Skills | ✅ | ⚙️ basic |
| Output | Structured outputs | ✅ | ✅ inference-dependent |
| Models | Vision | ✅ | ✅ model-dependent |
| Optimization | Prompt caching | ✅ | ❌ |
| Reasoning | Extended thinking | ✅ | ✅ |
| Platform | Token-based auth | ✅ | ✅ |
| Platform | OAuth / organizations | ✅ | ❌ |

✅ Supported · ⚙️ Partial / in progress · ❌ Not supported

## Why LocalGPT?

LocalGPT is built around the idea that local AI should be private, practical, and developer-friendly.

Its goal is to provide a reusable application API layer on top of local inference servers, so developers can build useful AI products without depending on cloud APIs.

## How LocalGPT compares

### vs Ollama, LM Studio, LocalAI, vLLM, llama.cpp

These projects make it possible to run and serve models locally. They answer: *how do I run a model?*

LocalGPT answers the next question: *how do I build a useful AI application on top of that model?*

```text
Ollama / LM Studio / LocalAI / vLLM / llama.cpp = local inference layer
LocalGPT                                       = local AI application API layer
```

Use them together. Run your model with whichever inference server you prefer, then point LocalGPT at it.

### vs Onyx, Open WebUI

Both are app-first experiences focused on chat and enterprise search. LocalGPT is API-first: it provides a standardized local backend layer for building self-hosted AI applications.

```text
Onyx / Open WebUI = self-hosted AI applications
LocalGPT          = API layer for building self-hosted AI applications
```

## Community and contributing

Contributions, bug reports, documentation improvements, and pull requests are welcome.

For technical documentation and project development, see the repository issues and source tree.
