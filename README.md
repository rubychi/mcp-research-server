# MCP: Research (Server)

This project is a hands-on implementation from the [MCP: Build Rich-Context AI Apps with Anthropic](https://www.deeplearning.ai/short-courses/mcp-build-rich-context-ai-apps-with-anthropic/).

It demonstrates how to use the Model Context Protocol (MCP) to build AI applications that can access tools, data, and prompts from external sources in a standardized way.

For the client, see [mcp-research-client](https://github.com/rubychi/mcp-research-client).

## Overview

The Model Context Protocol (MCP) is an open protocol developed by Anthropic that standardizes how large language models (LLMs) access external tools and data. MCP uses a client-server architecture, making it easy to integrate new tools and connect to external systems such as arXiv, GitHub, Google Docs, or local files.

This project provides an MCP server that exposes tools and resources for searching and retrieving academic papers from arXiv, as well as prompt templates for LLMs.

## Features

- **Standardized Tool Access:** Exposes tools for searching arXiv and extracting paper information.
- **Resource Endpoints:** Provides resources for listing available topics and retrieving detailed paper information.
- **Prompt Templates:** Supplies prompts for LLMs to synthesize and summarize research topics.
- **Client-Server Architecture:** Built using the FastMCP server from the `mcp` Python package.
- **Docker & Procfile Support:** Ready for deployment in various environments.

## Project Structure

```
.
├── research_server.py      # MCP server exposing tools/resources/prompts
├── pyproject.toml          # Project metadata and dependencies
├── Dockerfile              # Containerization support
├── Procfile                # For deployment (e.g., Heroku)
├── uv.lock                 # Dependency lock file
├── .python-version         # Python version specifier
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.11.11
- [uv](https://github.com/astral-sh/uv) (for dependency management)
- Docker (optional, for containerized deployment)

### Installation

1. **Clone this repository:**
   ```bash
   git clone git@github.com:rubychi/mcp-research-server.git
   ```

2. **Create a virtual environment:**
   ```bash
   uv venv .venv
   ```

3. **Activate the environment:**
   ```bash
   source .venv/bin/activate
   ```

4. **Run the MCP server:**
   ```bash
   python research_server.py
   ```
   The server will start on port 8001 by default (or use the `PORT` environment variable).

5. **(Optional) Run with Docker:**
   ```bash
   docker build -t mcp-research .
   docker run -p 8001:8001 mcp-research
   ```

### Usage

- Use the MCP server as a backend for MCP-compatible clients (e.g., Claude Desktop, MCP Inspector, or your own client).
- The server exposes the following tools and resources:
  - `search_papers(topic, max_results)`: Search arXiv for papers on a topic.
  - `extract_info(paper_id)`: Retrieve detailed info for a specific paper.
  - `papers://folders`: List all available research topics.
  - `papers://{topic}`: Get detailed information about papers on a specific topic.
  - `generate_search_prompt(topic, num_papers)`: Generate a prompt for LLMs to synthesize research.

- Paper data is stored in the `papers/` directory, which is created automatically as you use the tools.

## Configuration

- The server port can be set via the `PORT` environment variable.
- No additional configuration is required for basic usage.

## References

- [Course: MCP: Build Rich-Context AI Apps with Anthropic (DeepLearning.AI)](https://www.deeplearning.ai/short-courses/mcp-build-rich-context-ai-apps-with-anthropic/)
- [Anthropic](https://www.anthropic.com/)
- [DeepLearning.AI](https://www.deeplearning.ai/)
