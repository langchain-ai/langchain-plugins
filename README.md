# LangChain Plugins

The official marketplace of **LangChain ecosystem plugins** for your coding agent.
Add it once, then install skills and MCP servers that help you build with
LangChain, LangGraph, and Deep Agents — and observe and evaluate your apps with
LangSmith.

Works with **[dcode]**, **Claude Code**, and **OpenAI Codex**.

## What's inside

| Plugin                 | What you get                                                                                                                                   | Use it when                                                          |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **`langchain-skills`** | Skills for building agents with LangChain, LangGraph, and Deep Agents — models, tools, RAG, streaming, middleware, persistence, HITL, and more | You're writing or debugging LangChain / LangGraph / Deep Agents code |
| **`langsmith-skills`** | Skills for tracing, building datasets, and running evaluations with LangSmith                                                                  | You're debugging a run or setting up evals                           |
| **`langchain-mcp`**    | Live **LangChain Docs** and **API Reference** MCP servers                                                                                      | You want your agent to look up current docs and API signatures       |
| **`langsmith-mcp`**    | The **LangSmith** MCP server — query your traces, datasets, prompts, and experiments from your agent                                           | You want your agent to read your LangSmith workspace                 |

## Install

### 1. Add the marketplace

**dcode**

```
dcode plugin marketplace add langchain-ai/langchain-plugins
```

**Claude Code**

```
/plugin marketplace add langchain-ai/langchain-plugins
```

**OpenAI Codex**

```
codex plugin marketplace add langchain-ai/langchain-plugins
```

### 2. Install the plugins you want

Plugin IDs use the form `plugin-name@langchain-plugins`. Install any subset:

**dcode**

```
dcode plugin install langchain-skills@langchain-plugins
dcode plugin install langsmith-skills@langchain-plugins
dcode plugin install langchain-mcp@langchain-plugins
dcode plugin install langsmith-mcp@langchain-plugins
```

Then run `/reload` or start a new session.

**Claude Code**

```
/plugin install langchain-skills@langchain-plugins
/plugin install langsmith-skills@langchain-plugins
/plugin install langchain-mcp@langchain-plugins
/plugin install langsmith-mcp@langchain-plugins
```

**OpenAI Codex** (note: Codex uses `add`, not `install`)

```
codex plugin add langchain-skills@langchain-plugins
codex plugin add langsmith-skills@langchain-plugins
codex plugin add langchain-mcp@langchain-plugins
codex plugin add langsmith-mcp@langchain-plugins
```

## Using the plugins

**Skills** activate automatically when your request matches what a skill covers —
ask your agent to "build a LangGraph agent" or "help me set up a LangSmith eval"
and the relevant skill kicks in. You can also invoke one explicitly. With
[dcode], run `/skill:langchain-skills@langchain-plugins:langchain-rag`.

**MCP servers** become available once their plugin is enabled:

| Server                | Gives your agent                                               | Sign-in                       |
| --------------------- | -------------------------------------------------------------- | ----------------------------- |
| `langchain-docs`      | Live LangChain / LangGraph / LangSmith documentation           | None                          |
| `langchain-reference` | Up-to-date API reference lookups                               | None                          |
| `langsmith`           | Read access to your traces, datasets, prompts, and experiments | **LangSmith account** (OAuth) |

The **LangSmith** server signs in with OAuth — there are no API keys to paste.
If your LangSmith workspace is in the EU, APAC, or AWS regions, point the server
at your regional host per the
[LangSmith Remote MCP docs](https://docs.langchain.com/langsmith/langsmith-remote-mcp).

## Requirements

- A supported agent CLI: [dcode], Claude Code, or OpenAI Codex.
- A [LangSmith account](https://smith.langchain.com) — only needed for the
  `langsmith-mcp` plugin.

## Staying current

The skill plugins track their upstream LangChain releases and are refreshed
automatically, so installing from this marketplace keeps you on the latest
published versions. Run your agent's marketplace **update** command periodically
to pick up new releases:

```
dcode plugin marketplace update langchain-plugins
/plugin marketplace update langchain-plugins           # Claude Code
codex plugin marketplace upgrade langchain-plugins     # OpenAI Codex
```

[dcode]: https://docs.langchain.com/oss/python/deepagents/code/overview
