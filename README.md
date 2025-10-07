# 🚀 CrewAI: Orchestrate Your Autonomous AI Crew

<p align="center"><img src="./docs/images/crewai_logo.png" alt="CrewAI Logo" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/crewAI/stargazers"><img src="https://img.shields.io/github/stars/grewal16/crewAI?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/crewAI/network/members"><img src="https://img.shields.io/github/forks/grewal16/crewAI?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/crewAI/issues"><img src="https://img.shields.io/github/issues/grewal16/crewAI?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE"><img src="https://img.shields.io/github/license/grewal16/crewAI?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
CrewAI is an innovative open-source framework designed to empower developers to build and manage highly intelligent, collaborative AI agent systems. It transforms complex workflows into orchestrated "crews" of autonomous agents that work together, leveraging specialized tools, memory, and knowledge to achieve predefined goals. From multi-stage reasoning to human-in-the-loop interactions, CrewAI provides a robust and flexible architecture for creating next-generation AI applications.

## ✨ Key Features
*   **Intelligent Agent Orchestration:** Define autonomous agents with distinct roles, goals, and backstories, then orchestrate them into collaborative crews.
*   **Flexible Task Management:** Assign tasks with customizable outputs, callbacks, and conditional logic, enabling dynamic workflows.
*   **Dynamic Tool Integration:** Seamlessly integrate a rich ecosystem of tools for web scraping, data access, code interpretation, AI/ML, and more.
*   **Advanced Memory & Knowledge:** Equip agents with various memory types (short-term, long-term, contextual, entity) and knowledge bases (RAG, documents, databases).
*   **Multi-Model LLM Support:** Utilize a wide range of Large Language Models, including OpenAI, Anthropic, Google Gemini, Ollama, and custom solutions.
*   **Observable Workflows:** Gain deep insights into agent reasoning, tool usage, and collaboration through detailed logging and tracing capabilities.
*   **Human-in-the-Loop:** Incorporate human intervention at critical junctures for validation, refinement, or direct input.
*   **Command-Line Interface (CLI):** Accelerate development with CLI commands for scaffolding projects, deploying crews, and managing configurations.
*   **Experimental Evaluation Module:** Test and refine agent performance with built-in evaluation metrics for reasoning, goal achievement, and tool usage.
*   **Enterprise-Ready Features:** Support for advanced features like RBAC, agent repositories, hallucination guardrails, and integrations for business systems.

## Who is this for?
CrewAI is perfect for:
*   **AI Developers & Engineers:** Building sophisticated multi-agent AI systems and exploring collaborative AI.
*   **Researchers:** Experimenting with agentic workflows, emergent behavior, and advanced reasoning.
*   **Businesses & Startups:** Automating complex processes, enhancing decision-making, and creating intelligent assistants.
*   **MLOps Professionals:** Deploying, monitoring, and scaling AI agent applications with robust infrastructure.
*   **Anyone looking to harness the power of autonomous AI** to solve real-world problems.

## Technology Stack & Architecture
CrewAI is built predominantly in **Python**, leveraging its rich ecosystem for AI development.

*   **Core Language:** Python
*   **LLM Providers:** OpenAI, Anthropic, Google Gemini, Ollama, and extensible custom LLM integrations.
*   **Data Models:** Pydantic for robust data validation and settings management.
*   **Vector Databases:** ChromaDB and Qdrant for efficient RAG (Retrieval Augmented Generation) and memory management.
*   **Workflow Orchestration:** Custom agent and crew management logic with support for Langgraph adapters.
*   **Event Handling:** An event-driven architecture for observability, logging, and custom callbacks.
*   **CLI:** Click for command-line interface development.
*   **Dependency Management:** Poetry (as indicated by `pyproject.toml`).

## 📊 Architecture & Database Schema
CrewAI's architecture revolves around the intelligent orchestration of specialized agents, enabling complex problem-solving through collaborative task execution.

```mermaid
graph TD
    A[User Input] --> B{Kickoff Crew};
    B --> C[Crew Orchestrator];
    C --> D{Manager Agent};
    D -- Delegates Tasks --> E[Specialized Agents];
    E -- Execute Task --> F{Tools};
    E -- Store/Retrieve --> G[Memory/Knowledge Base];
    G -- RAG/Embeddings --> H[Vector Database (ChromaDB/Qdrant)];
    F --> E;
    H --> E;
    E -- Collaborate/Delegate --> D;
    D -- Final Output --> I[Result];
    I --> A;
```

**High-Level Flow:**
1.  **User Input:** The process begins with a user providing a prompt or task.
2.  **Kickoff Crew:** The `Crew` is initialized with defined agents, tasks, and a process flow.
3.  **Crew Orchestrator:** The central `Crew` manages the overall execution, adhering to a defined process (e.g., Sequential, Hierarchical).
4.  **Manager Agent (Hierarchical Process):** A dedicated agent in a hierarchical crew is responsible for planning, delegating tasks to specialized agents, and ensuring overall progress. In a sequential process, agents pass results directly.
5.  **Specialized Agents:** Individual `Agents` with unique roles, goals, and capabilities (defined by their LLM, tools, and memory) take on specific tasks.
6.  **Tools:** Agents interact with external APIs, databases, or custom functionalities through `Tools` to gather information or perform actions.
7.  **Memory/Knowledge Base:** Agents leverage various `Memory` types (Short-term, Long-term, Contextual, Entity) and `Knowledge Bases` (built on RAG) for persistent learning and contextual retrieval.
8.  **Vector Database:** Underpins the RAG and advanced memory functionalities, storing embeddings for efficient semantic search.
9.  **Collaboration/Delegation:** Agents collaborate by sharing information or delegating sub-tasks, guided by the `Crew Orchestrator`.
10. **Result:** The `Crew` synthesizes the final output from completed tasks and provides it back to the user.

## ⚡ Quick Start Guide
To get started with CrewAI, follow these simple steps:

1.  **Install CrewAI:**
    ```bash
    pip install crewai
    ```
    or, if using Poetry:
    ```bash
    poetry add crewai
    ```

2.  **Set Up Your Environment Variables:**
    Create a `.env` file in your project root and add your LLM API keys (e.g., `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`).

3.  **Define Your Agents:**
    ```python
    from crewai import Agent

    researcher = Agent(
        role='Senior Research Analyst',
        goal='Uncover groundbreaking technologies',
        backstory='A meticulous analyst with a passion for innovation.',
        verbose=True,
        allow_delegation=False
    )

    writer = Agent(
        role='Technical Writer',
        goal='Compose engaging technical articles',
        backstory='A skilled writer crafting clear and compelling narratives.',
        verbose=True,
        allow_delegation=True
    )
    ```

4.  **Define Your Tasks:**
    ```python
    from crewai import Task

    research_task = Task(
        description='Identify the top 3 emerging AI technologies in 2024.',
        agent=researcher,
        expected_output='A detailed report on 3 technologies, their applications, and market potential.'
    )

    write_task = Task(
        description='Write a blog post based on the research findings.',
        agent=writer,
        context=[research_task], # Pass output of research_task as context
        expected_output='A 800-word engaging blog post, formatted in markdown.'
    )
    ```

5.  **Assemble Your Crew and Kickoff:**
    ```python
    from crewai import Crew, Process

    my_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, write_task],
        process=Process.sequential, # Or Process.hierarchical
        verbose=2 # Outputs more details during execution
    )

    result = my_crew.kickoff()
    print("## Crew Work Results:")
    print(result)
    ```

## 📜 License
This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.