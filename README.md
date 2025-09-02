# 🚀 crewAI: Orchestrating Autonomous AI Agent Teams

<p align="center"><img src="./docs/images/crewai_logo.png" alt="crewAI Logo" width="500"></p>

## Short Description
crewAI is an innovative open-source framework designed to empower developers and AI enthusiasts to build, orchestrate, and manage intelligent, autonomous AI agents. It facilitates the creation of collaborative "crews" where specialized agents work together seamlessly, leveraging advanced AI capabilities to solve complex problems, automate workflows, and generate high-quality, thought-out results.

## ✨ Key Features
*   **Agent Orchestration:** Define roles, goals, and tools for each agent, then watch them collaborate within a sophisticated task management system.
*   **Role-Playing & Specialization:** Agents assume distinct personas and responsibilities, promoting efficient division of labor and expertise.
*   **Flexible Process Flows:** Supports both sequential and hierarchical task execution, allowing for adaptive problem-solving strategies.
*   **Advanced Tool Integration:** Seamlessly integrate custom or third-party tools, enabling agents to interact with external systems and data.
*   **Memory Management:** Implement diverse memory types (short-term, contextual, entity, external) to enhance agent recall and learning across tasks and sessions.
*   **Retrieval Augmented Generation (RAG):** Empower agents with knowledge bases for informed decision-making and reduced hallucinations.
*   **CLI & Developer Tools:** Accelerate development with command-line interface tools for quick setup, deployment, and management of crews and flows.
*   **Observability & Evaluation:** Gain deep insights into agent behavior, task execution, and crew performance with built-in tracing, logging, and evaluation metrics.
*   **Human-in-the-Loop:** Integrate human input and supervision at critical junctures for guided collaboration and ethical oversight.

## Who is this for?
crewAI is ideal for:
*   **Developers & AI Engineers:** Rapidly prototype, deploy, and scale complex AI applications.
*   **Researchers:** Experiment with multi-agent systems and study emergent behaviors.
*   **Businesses:** Automate intricate operational workflows, from content generation to customer support, with intelligent, collaborative AI.
*   **Innovators:** Build the next generation of AI assistants and autonomous systems.

## Technology Stack & Architecture
crewAI is primarily built with **Python**, leveraging cutting-edge Large Language Models (LLMs) and potentially integrates with vector databases for Retrieval Augmented Generation (RAG). Its modular design allows for flexibility in LLM providers and tool integrations, fostering a robust and extensible ecosystem.

## 📊 Architecture & Database Schema

```mermaid
graph TD
    A[User Input] -- "Task Request" --> B(CrewAI Framework);
    B -- "Initial Setup" --> C[Crew Definition];
    C -- "Orchestrates" --> D[Manager Agent];
    D -- "Delegates Tasks" --> E[Worker Agents];
    E -- "Executes Task" --> F{LLM / Tools / Memory};
    F -- "Accesses Data" --> G[Knowledge Base (RAG)];
    G --> F;
    E -- "Generates Intermediate Output" --> D;
    D -- "Consolidates" --> B;
    B -- "Final Result" --> H[Output to User];

    subgraph Agent Capabilities
        F --> I[Tools: Search, Automation, File I/O, etc.];
        F --> J[LLM: Reasoning, Generation];
        F --> K[Memory: Short-Term, Contextual, Entity, External];
    end
```

## ⚡ Quick Start Guide

To get started with `crewAI`, follow these simple steps:

1.  **Installation:**
    ```bash
    pip install crewai
    ```

2.  **Set up your Environment:**
    Ensure you have your API keys for your chosen LLM provider (e.g., OpenAI) set as environment variables.
    ```bash
    export OPENAI_API_KEY='YOUR_API_KEY'
    ```
    Or, use a `.env` file.

3.  **Create your first Crew:**
    Define your agents and tasks, then create a crew to kick off the process.

    ```python
    from crewai import Agent, Task, Crew, Process
    from crewai_tools import SerperDevTool

    # Initialize tool
    search_tool = SerperDevTool()

    # Define your agents with roles and goals
    researcher = Agent(
        role='Senior Researcher',
        goal='Uncover groundbreaking insights from the web',
        backstory='A meticulous researcher passionate about discovering hidden truths and delivering precise information.',
        verbose=True,
        allow_delegation=False,
        tools=[search_tool]
    )

    writer = Agent(
        role='Content Writer',
        goal='Craft compelling narratives from research findings',
        backstory='A gifted storyteller, able to transform complex data into engaging and accessible content.',
        verbose=True,
        allow_delegation=False
    )

    # Define tasks
    research_task = Task(
        description='Investigate the latest advancements in AI and their real-world applications.',
        agent=researcher,
        expected_output='A detailed report of AI advancements and applications.'
    )

    write_task = Task(
        description='Write a blog post about the findings from the research, highlighting key benefits and future implications.',
        agent=writer,
        context=[research_task],
        expected_output='A captivating blog post, approximately 500 words.'
    )

    # Instantiate your crew
    tech_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, write_task],
        process=Process.sequential,
        verbose=True
    )

    # Kickoff the crew
    print("🚀 CrewAI is starting up...")
    result = tech_crew.kickoff()
    print("\n\n########################")
    print("## Here is the result ##")
    print("########################\n")
    print(result)
    ```

## 📜 License
This project is licensed under the **MIT License**. See the `LICENSE` file for details.