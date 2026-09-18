div align="center">

LocalGPT is the open-source API layer that turns local models into production AI applications.




</div>

Running a model locally is only the first step. To build useful AI applications you need a set of higher-level building blocks. LocalGPT provides that layer as an open-source API following the Claude API model — so you can build private AI products without rebuilding the same backend primitives from scratch, and without depending on cloud APIs.



Your app / agent / workflow / UI
              |
        LocalGPT API
              |
OpenAI-compatible inference server (Ollama, llama.cpp, vLLM, …)              

LocalGPT does not run models itself. It connects to any OpenAI-compatible inference server via OPENAI_API_BASE. If it implements /v1/chat/completions and /v1/models, it works.

LocalGPT ships a built-in workbench UI for testing and demos, available at /ui. The API is the actual product.

What LocalGPT gives you

Standard messages API (streaming, async, token counting)

File and artifact ingestion

Retrieval with citations and agentic RAG

Built-in tools mirroring the Claude API (web search, web fetch, code execution)

Custom tools and MCP connectors

Structured access to databases and CSVs

Embeddings and orchestration

Quickstart

For Docker, full installation options, and model configuration see the full Quickstart guide.

Prerequisites: You need a running OpenAI-compatible LLM server. Ollama is the easiest starting point.

1. Install LocalGPT

# macOS
brew install private-gpt

# Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

uv tool install --python 3.11 \
  --find-links https://wheels.privategpt.dev/packages/ \
  "private-gpt[core]"

# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

uv tool install --python 3.11 `
  --find-links https://wheels.privategpt.dev/packages/ `
  "private-gpt[core]"

2. Start your LLM server

# Example with Ollama
ollama pull qwen3.5:35b         # LLM (~24 GB)
ollama pull mxbai-embed-large   # Embeddings (~670 MB)
ollama serve

3. Run LocalGPT

# macOS / Linux
OPENAI_API_BASE=http://localhost:<llm-port>/v1 \
  OPENAI_EMBEDDING_API_BASE=http://localhost:<embedding-port>/v1 \
  private-gpt serve

# Windows (PowerShell)
$env:OPENAI_API_BASE = "http://localhost:<llm-port>/v1"
$env:OPENAI_EMBEDDING_API_BASE = "http://localhost:<embedding-port>/v1"
private-gpt serve

4. Open the UI

Go to http://localhost:8080/ui. The API is at http://localhost:8080 and follows the Anthropic API spec.

<img src="./fern/docs/assets/ui.png"/>

The UI is useful for:

Sending messages.

Selecting models from /v1/models.

Uploading documents.

Testing retrieval with citations.

Enabling tools per chat.

Configuring databases, MCP connectors, skills, and custom tools.

Inspecting requests and responses through the API Debugger.

This UI is a demonstrator, not the core product. Developers are expected to build their own applications on top of the API. That said, the UI is intentionally polished enough for demos, videos, internal pilots, and quick local usage.

Integrations








Claude Desktop / Cowork


Microsoft Excel Claude add-in


Microsoft Word Claude add-in


n8n


OpenCode


LocalGPT Workbench

LocalGPT works natively as the local backend for the tools developers and end users already use.

Integration Guide

What it enables

Claude Code

Use your local models as the backend for agentic coding in the terminal

Claude Desktop / Cowork

Connect the Claude desktop app and Cowork to your private models

Claude for Microsoft 365

Run private AI inside Word, Excel, Outlook, and PowerPoint

OpenCode

Local AI coding assistant in the terminal

Any tool that works with a local OpenAI-compatible provider will also work with LocalGPT. The list below is non-exhaustive.

Tool

Link

n8n

n8n.io

OpenClaw

openclaw.ai

Hermes Agent

hermes-agent.dev

VS Code

code.visualstudio.com

Cline

cline.bot

Claude API compatibility

LocalGPT follows the Claude API as the reference for modern AI application APIs. The goal is full coverage where it makes sense for a local, open-source layer.

Area

Capability

Claude API

LocalGPT

Models

Model selection

✅

✅

Messages

Messages API

✅

✅

Messages

Streaming

✅

✅

Messages

Batch / async processing

✅

✅ async

Messages

Token counting

✅

✅

Knowledge

Files / artifacts

✅

✅

Knowledge

PDF and document ingestion

✅

✅

Knowledge

Retrieval with citations

✅

✅

Knowledge

Embeddings

✅

✅

Tools

Tool use

✅

✅

Tools

Tools in streaming

✅

✅

Tools

Built-in web search

✅

✅

Tools

Web extraction / fetch

✅

✅

Tools

Custom tools

✅

✅

Data

Database querying

Via tools

✅ built-in

Data

CSV / tabular analysis

Via tools / code

✅ built-in

Agents

MCP in the API

✅

✅

Agents

Remote MCP servers

✅

✅

Agents

Skills

✅

⚙️ basic

Output

Structured outputs

✅

✅ inference-dependent

Models

Vision

✅

✅ model-dependent

Optimization

Prompt caching

✅

❌

Reasoning

Extended thinking

✅

✅

Platform

Token-based auth

✅

✅

Platform

OAuth / organizations

✅

❌

✅ Supported · ⚙️ Partial / in progress · ❌ Not supported

Contributions are especially welcome in ⚙️ areas.

Why LocalGPT? A brief history

LocalGPT started as a proof of concept in 2023: a script that let you chat with your documents, fully offline, with no data leaving your machine. It went viral on GitHub, crossed 50K stars, and became one of the most-watched AI repos of that year.

That early version made one thing clear: there was serious demand for private, local AI that worked without cloud dependencies.

LocalGPT 1.0 is the evolution of that idea — rebuilt from the ground up as a proper API layer for private AI applications.



How LocalGPT compares

vs Ollama, LM Studio, LocalAI, vLLM, llama.cpp

These projects make it possible to run and serve models locally. They answer: how do I run a model?

LocalGPT answers the next question: how do I build a useful AI application on top of that model?

Ollama / LM Studio / LocalAI / vLLM / llama.cpp  =  local inference layer
LocalGPT                                        =  local AI application API layer

Use them together. Run your model with whichever inference server you prefer, then point LocalGPT at it.

vs Onyx, Open WebUI

Both are valuable, but they are app-first experiences focused on chat and enterprise search. LocalGPT is API-first. It provides the standardized local backend underneath those products — not the final product itself.

Onyx / Open WebUI  =  self-hosted AI applications
LocalGPT         =  API layer for building self-hosted AI applications

Community and contributing

Discord — questions, show-and-tell, and release discussions

Documentation — full reference, guides, and API docs

Community Forks — interesting forks and derivatives by the community

Pull requests are welcome. If your PR doesn't fit the upstream roadmap, you can add your fork to the Community Forks page instead.
