# CrewAI Agent Research & Writing Workflow

This project demonstrates a multi-agent research workflow built with CrewAI. It uses a research agent to gather information from the web and a writing agent to turn those findings into a polished blog post.

The workflow is implemented in the notebook [crewAI.ipynb](crewAI.ipynb) and is designed for topics such as AI trends, industry analysis, and market research summaries.

## Features

- Research agent for web-based topic exploration
- Search integration via Serper Dev Tool
- Groq-powered LLM support
- Content writer agent that transforms research into readable blog content
- Multi-task Crew orchestration with CrewAI

## Project Structure

- [crewAI.ipynb](crewAI.ipynb) — main notebook containing the CrewAI workflow
- [README.md](README.md) — project documentation

## Tech Stack

- Python
- CrewAI
- CrewAI Tools
- Groq / LangChain Groq integration
- Serper API for search

## Prerequisites

Before running the project, make sure you have:

- Python 3.9+
- Jupyter Notebook or Google Colab
- A Groq API key
- A Serper API key

## Installation

Install the required libraries:

```bash
pip install crewai crewai_tools langchain_groq
```

You may also install the dependencies used in the notebook environment if needed:

```bash
pip install crewai crewai_tools
pip install langchain_groq
```

## Environment Setup

Set your API keys before running the workflow.

### Option 1: Environment variables

```bash
export GROQ_API_KEY="your_groq_key"
export SERPER_API_KEY="your_serper_key"
```

On Windows PowerShell:

```powershell
$env:GROQ_API_KEY="your_groq_key"
$env:SERPER_API_KEY="your_serper_key"
```

### Option 2: Notebook secret / userdata

The notebook example uses Google Colab userdata secrets:

```python
from google.colab import userdata

GROQ_API_KEY = userdata.get('GROQ_API_KEY')
serper_API_KEY = userdata.get('serper')
```

## How It Works

The workflow creates two agents:

1. Researcher Agent
   - Analyzes the topic
   - Searches for reliable sources
   - Produces a structured research brief

2. Content Writer Agent
   - Converts the research into a blog post
   - Keeps facts and citations intact
   - Writes in a readable markdown format

The project then creates two tasks and runs them in a Crew:

```python
crew = Crew(
    agents=[reseacher, content_writer],
    tasks=[reseach_task, writing_task],
    verbose=True
)

result = crew.kickoff(inputs={"topic": topic})
print(result)
```

## Example Usage

Open the notebook and update the topic variable:

```python
topic = "medical industry using gen Ai"
```

Then run all the cells in order. The workflow will:

- search the web
- collect relevant sources
- summarize findings
- generate a blog post draft

## Important Notes

- The notebook uses `ChatGroq` with a Groq model such as `groq/gemma2-9b-it`.
- The search tool uses `SerperDevTool(api_key=serper_API_KEY, n_results=10)`.
- Some examples set an environment variable named `GROQ` in addition to `GROQ_API_KEY`.
- The `kickoff` call should be passed with `inputs={"topic": topic}` to match the notebook pattern.

## Troubleshooting

### Missing API key errors

Make sure your keys are loaded correctly and that the names match what the code is using.

### Search tool errors

Verify that your Serper API key is valid and has access to the Serper Dev search service.

### LLM connection issues

Confirm that your Groq API key is active and that the chosen model name is supported.

## License

This project is provided for educational and experimental use.

## Acknowledgements

- CrewAI
- CrewAI Tools
- Groq
- Serper

You can use this notebook as a starting point for custom research agents, content generation workflows, and topic analysis pipelines.
