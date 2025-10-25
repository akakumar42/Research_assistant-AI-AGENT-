# Research Assistant — AI Agent

A compact research-assistant agent built with LangChain integrations for web search and Wikipedia queries, plus a small persistence utility for saving results. This repository is intended as a developer-oriented reference implementation and a minimal starting point for building an LLM-powered research workflow.

## Highlights
- LLM-driven agent using Claude via [`main.llm`](main.py).
- Tooling for web search and Wikipedia via [`tools.search_tool`](tools.py) and [`tools.wiki_tool`](tools.py).
- Simple file persistence helper: [`tools.save_to_txt`](tools.py).
- Structured output model defined as [`main.ResearchResponse`](main.py) and parsed by [`main.parser`](main.py).
- Entrypoint and orchestrator: [`main.agent_executor`](main.py) in [main.py](main.py).

## Repository layout
- [main.py](main.py) — Application entry; wires the LLM, prompt, tools, and agent executor.
- [tools.py](tools.py) — Implements the search, Wikipedia, and save utilities.
- [requirements.txt](requirements.txt) — Python dependencies.
- [.env](.env) — Environment variables (API keys). Not checked into source control.
- [.gitignore](.gitignore) — Ignored files configuration.

## Quickstart (developer)
1. Create and activate a Python 3.11+ venv (recommended).
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Populate `.env` with required API keys (e.g., Anthropic/Claude keys).
4. Run the agent:
   ```bash
   python main.py
   ```
   The program prompts for a research query and will run the configured tools and return structured output.

## Design & Components
- LLM: instantiated as [`main.llm`](main.py) (Anthropic/Claude in this workspace).
- Prompting: uses a Chat prompt template and a Pydantic parser to enforce structured outputs via [`main.ResearchResponse`](main.py).
- Tools: implemented in [tools.py](tools.py):
  - [`tools.search_tool`](tools.py) — DuckDuckGo search wrapper.
  - [`tools.wiki_tool`](tools.py) — Wikipedia query wrapper.
  - [`tools.save_to_txt`](tools.py) — Appends research output to a text file.
- Agent: uses LangChain's tool-calling agent pattern orchestrated by [`main.agent_executor`](main.py).

## Development notes
- The Pydantic model ensures outputs are easily consumable programmatically. Adjust [`main.ResearchResponse`](main.py) if you need different output fields.
- The save utility appends to a default `research_output.txt`; update the filename or formatting in [`tools.save_to_txt`](tools.py) to suit your needs.
- Keep secrets in `.env` and ensure `.gitignore` includes it (already present).

## Testing & Iteration
- Start small prompts to validate LLM/tool interactions.
- Inspect raw agent output (the code prints raw responses on parse errors) to tweak prompt/formatting.
- Consider adding unit tests around parsing and tool wrappers to validate behavior.

## Contributing
- Fork, branch, and submit PRs. Keep changes focused and add tests for any logic you introduce.

## Files & Symbols (quick links)
- [main.py](main.py)
  - [`main.llm`](main.py)
  - [`main.parser`](main.py)
  - [`main.ResearchResponse`](main.py)
  - [`main.agent_executor`](main.py)
  - [`main.agent`](main.py)
- [tools.py](tools.py)
  - [`tools.search_tool`](tools.py)
  - [`tools.wiki_tool`](tools.py)
  - [`tools.save_to_txt`](tools.py)
- [requirements.txt](requirements.txt)
- [.env](.env)
- [.gitignore](.gitignore)
- [README.md](README.md)

License: Add a license file if you plan to publish or share this project publicly.