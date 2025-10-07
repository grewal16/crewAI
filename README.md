# 🚀 CrewAI: Orchestrate Autonomous AI Agents

<p align="center"><img src="./docs/images/crewai_logo.png" alt="CrewAI Logo" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/crewAI/stargazers"><img src="https://img.shields.io/github/stars/grewal16/crewAI?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/crewAI/network/members"><img src="https://img.shields.io/github/forks/grewal16/crewAI?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/crewAI/issues"><img src="https://img.shields.io/github/issues/grewal16/crewAI?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE"><img src="https://img.shields.io/github/license/grewal16/crewAI?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description

Unleash the power of collaborative AI with **CrewAI**, a groundbreaking open-source framework designed for orchestrating intelligent, role-playing AI agents. Mimic human teamwork by allowing agents to communicate, delegate, and execute complex tasks autonomously. Build sophisticated AI applications that go beyond single-agent capabilities, from automated content creation to dynamic customer support, all within a structured, observable, and extensible ecosystem.

## ✨ Key Features

*   **Intelligent Agent Orchestration:** Define specialized AI agents with unique roles, goals, and backstories that collaborate to tackle complex objectives.
*   **Advanced Memory System:** Equip your agents with a multi-layered memory architecture, including contextual, entity, short-term, and long-term memory, ensuring they learn and adapt over time.
*   **Robust Tool Integration:** Empower agents with a wide array of tools to interact with the real world, from custom functions to external APIs for data retrieval, automation, and more.
*   **Flexible RAG Capabilities:** Integrate Retrieval Augmented Generation (RAG) using vector databases like ChromaDB and Qdrant to provide agents with up-to-date and relevant knowledge.
*   **Structured Workflows (Flows):** Design, visualize, and persist intricate multi-agent workflows, supporting both sequential and hierarchical processes.
*   **Comprehensive Observability:** Monitor every action, thought, and output of your agents with detailed tracing and evaluation tools, allowing for continuous refinement and debugging.
*   **Built for Scale & Enterprise:** Features like Role-Based Access Control (RBAC), webhook integrations (Slack, Salesforce, GitHub), and hallucination guardrails make CrewAI production-ready.
*   **Developer-Friendly CLI:** Quickly scaffold, deploy, and manage your agent crews and flows with an intuitive command-line interface.

## Who is this for?

CrewAI is meticulously crafted for **developers, AI engineers, data scientists, and organizations** eager to transcend the limitations of single-agent AI. Whether you're automating intricate business processes, building next-generation conversational AI, developing research assistants, or exploring cutting-edge multi-agent systems, CrewAI provides the robust foundation and flexibility you need. It's for innovators who demand intelligent, autonomous, and collaborative solutions.

## Technology Stack & Architecture

CrewAI is a Python-first framework, prioritizing flexibility and robust engineering. It leverages Pydantic for structured data validation and works seamlessly with a variety of Large Language Models (LLMs), including OpenAI, Ollama, and Google Gemini. Its core architecture is event-driven, facilitating clear communication and detailed observability for agent actions and interactions. For persistent knowledge and contextual retrieval, CrewAI integrates with vector databases like ChromaDB and Qdrant.

## 📊 Architecture & Database Schema

CrewAI's architecture is designed for clear agent orchestration and data flow. The visual below outlines the high-level components and their interactions:

```mermaid
graph TD
    A["User Input/Trigger"] --> B(CrewAI Framework);
    B --> C{Orchestrate Crew};
    C --> D[Define Agents: "Role", "Goal", "Backstory", "LLM", "Memory", "Tools"];
    C --> E[Define Tasks: "Description", "Expected Output", "Agent Assignment"];
    C --> F[Define Flow/Process: "Sequential", "Hierarchical"];
    D & E & F --> G{Execute Tasks by Agents};
    G -- Use Tools --> H[External Tools/APIs];
    G -- Access Knowledge --> I[Knowledge Bases/RAG];
    G -- Recall Context --> J[Memory (Short-term, Long-term, Entity)];
    G --> K["Task Output"];
    K --> L{Evaluate/Refine};
    L -- Re-plan --> G;
    L -- Finalize --> M["Crew Output"];
    M --> N["User/System"];
```

## ⚡ Quick Start Guide

Get your first intelligent crew up and running in minutes!

1.  **Installation:**

    ```bash
    pip install crewai
    ```

2.  **Set up your LLM API Key:**
    Export your API key (e.g., OpenAI, Anthropic, Google Gemini):

    ```bash
    export OPENAI_API_KEY='YOUR_API_KEY'
    ```

3.  **Create your first Crew:**
    Define your agents, their tasks, and orchestrate them into a crew.

    ```python
    from crewai import Agent, Task, Crew, Process
    from crewai_tools import SerperDevTool

    # Initialize tools
    search_tool = SerperDevTool()

    # Define your agents
    researcher = Agent(
        role='Senior Research Analyst',
        goal='Uncover groundbreaking insights from web searches',
        backstory='A seasoned analyst who excels at synthesizing complex information.',
        tools=[search_tool],
        verbose=True,
        allow_delegation=False
    )

    writer = Agent(
        role='Content Creator',
        goal='Craft compelling narratives based on research findings',
        backstory='A creative writer who transforms data into engaging stories.',
        verbose=True,
        allow_delegation=False
    )

    # Define your tasks
    task1 = Task(
        description='Identify the latest trends in AI agents.',
        expected_output='A detailed report on the top 3 emerging trends, including their potential impact.',
        agent=researcher
    )

    task2 = Task(
        description='Write a blog post summarizing the research findings from the previous task.',
        expected_output='A 500-word blog post in an engaging and accessible tone.',
        agent=writer,
        context=[task1]
    )

    # Instantiate your crew
    tech_crew = Crew(
        agents=[researcher, writer],
        tasks=[task1, task2],
        process=Process.sequential, # Can be hierarchical
        verbose=2 # Show more details about the execution
    )

    # Kickoff the crew!
    result = tech_crew.kickoff()
    print("## Here is the result of the Crew's work:")
    print(result)
    ```

For more in-depth guides and examples, check out the `docs/` folder!

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.