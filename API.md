# API Documentation

## Overview

This document provides a concise reference for the public API of **my-agent-demo**. The project is a minimal example of an autonomous AI agent built on top of OpenAI's GPT models. The primary entry points are the `Agent` class and its configuration class `AgentConfig`. Additionally, the `run_agent.py` script demonstrates how to use the agent in an interactive loop.

---

## Classes

### `AgentConfig`

```python
class AgentConfig:
    def __init__(
        self,
        temperature: float = 0.7,
        model: str = "gpt-4o-mini",
        max_tokens: int = 1024,
        timeout: int = 30,
        **kwargs,
    ) -> None:
        """Configuration container for the :class:`Agent`.

        Parameters
        ----------
        temperature: float, optional
            Sampling temperature. Higher values (e.g., 0.9) make output more random,
            while lower values (e.g., 0.2) make it more deterministic. Default is 0.7.
        model: str, optional
            The OpenAI model name to use. Defaults to ``"gpt-4o-mini"``.
        max_tokens: int, optional
            Maximum number of tokens to generate for a single response. Default is 1024.
        timeout: int, optional
            HTTP request timeout in seconds. Default is 30.
        **kwargs: Any
            Additional keyword arguments are passed directly to the underlying OpenAI client.
        """
        ...
```

**Usage Example**

```python
from agent import AgentConfig

config = AgentConfig(
    temperature=0.5,
    model="gpt-4o-mini",
    max_tokens=500,
)
```

---

### `Agent`

```python
class Agent:
    def __init__(self, config: AgentConfig) -> None:
        """Create a new autonomous agent.

        Parameters
        ----------
        config: AgentConfig
            Configuration object that controls model behaviour.
        """
        ...

    def ask(self, prompt: str) -> str:
        """Send a prompt to the LLM and return the raw response.

        The method also handles any tool calls that the model requests (e.g.,
        ``get_directory_files`` or ``read_file``) and returns the final answer
        after the tools have been executed.
        """
        ...

    def chat(self, messages: List[Dict[str, str]]) -> str:
        """Perform a multi‑turn conversation.

        ``messages`` follows the OpenAI chat format, e.g.:
        ``[{"role": "user", "content": "Hello"}]``.
        """
        ...
```

**Usage Example**

```python
from agent import Agent, AgentConfig

config = AgentConfig(temperature=0.6)
agent = Agent(config)

answer = agent.ask("What is the capital of France?")
print(answer)  # → "Paris"
```

---

## Functions (Utility Tools)

The agent can invoke a set of *tool* functions that interact with the repository. These functions are defined in the `tools/` package (if present) and are automatically exposed to the model.

| Function | Description | Example Call |
|----------|-------------|--------------|
| `get_directory_files(path: str) -> List[str]` | Returns a list of file names in the given directory. | `get_directory_files(".")` |
| `read_file(filepath: str) -> str` | Reads the contents of a file and returns it as a string. | `read_file("README.md")` |
| `create_file(filepath: str, content: str) -> None` | Creates a new file with the supplied content. | `create_file("notes.txt", "Important notes")` |
| `update_file(filepath: str, old: str, new: str) -> None` | Replaces ``old`` with ``new`` in the specified file. | `update_file("README.md", "old text", "new text")` |
| `search_code(query: str) -> List[str]` | Performs a simple keyword search across the codebase. | `search_code("AgentConfig")` |

These utilities are thin wrappers around the repository's GitHub‑like API and are primarily intended for demonstration purposes.

---

## Scripts

### `run_agent.py`

A convenience script that launches an interactive REPL where the user can type natural‑language commands. The script creates an ``Agent`` instance with default configuration and continuously prompts the user for input.

**Typical usage**:

```bash
python run_agent.py
```

The script will display a prompt ``You:``. Type a request such as:

```
You: List all Python files in the repository.
```

The agent will call the appropriate tool (e.g., ``search_code``) and print the result.

---

## Testing

The repository includes a minimal test suite under the ``tests/`` directory. The primary test file ``test_agent.py`` checks that the ``Agent`` can be instantiated and that basic tool calls succeed.

Run the test suite with:

```bash
pytest -q
```

---

## License

The code in this repository is released under the **MIT License**. See the [LICENSE](../LICENSE) file for details.

---

## Contact & Support

For questions, suggestions, or contributions, please reach out to the author:

- **Email**: <your.email@example.com>
- **GitHub**: https://github.com/yourusername/my-agent-demo

---
