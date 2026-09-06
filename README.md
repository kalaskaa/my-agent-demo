# my-agent-demo

## Overview

**my-agent-demo** is a lightweight demonstration of an autonomous AI agent built with OpenAI's GPT models. The project showcases how to structure prompts, manage state, and interact with external tools to perform tasks such as file manipulation, web requests, and data processing. It serves as both a learning resource and a starting point for building more complex agents.

## Installation

### Prerequisites

- **Python 3.9+**
- **Git**
- An **OpenAI API key** (sign up at https://platform.openai.com/ if you don't have one)

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/my-agent-demo.git
   cd my-agent-demo
   ```
2. Create a virtual environment and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows use `venv\\Scripts\\activate`
   ```
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Set your OpenAI API key as an environment variable:
   ```bash
   export OPENAI_API_KEY="your-api-key"
   # On Windows PowerShell:
   $env:OPENAI_API_KEY="your-api-key"
   ```

## Usage

The main entry point is the `run_agent.py` script. It demonstrates a simple conversation loop where the agent can execute tool calls defined in the repository.

```bash
python run_agent.py
```

### Example Interaction

```text
You: List the files in the current directory.
Agent: (calls the `get_directory_files` tool)
Agent: I found the following files: ['README.md', 'run_agent.py', 'requirements.txt']
```

You can also import the core classes in your own scripts:

```python
from agent import Agent, AgentConfig

config = AgentConfig(temperature=0.7)
agent = Agent(config)
response = agent.ask("What is the weather in London?")
print(response)
```

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes and ensure all tests pass.
4. Commit your changes with a clear commit message.
5. Push the branch to your fork and open a Pull Request.

### Code Style

- Use **black** for formatting:
  ```bash
  black .
  ```
- Follow **PEP 8** guidelines.
- Add or update tests in the `tests/` directory.

## License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

## Contact

- **Author**: Your Name (<your.email@example.com>)
- **GitHub**: https://github.com/yourusername/my-agent-demo
- **OpenAI Community**: https://community.openai.com/

Feel free to open an issue for bugs, feature requests, or general questions.