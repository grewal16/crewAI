# 🚀 crewAI

<p align="center"><img src="./docs/images/crewai_logo.png" alt="crewAI Logo" width="300"></p>

## Short Description
crewAI is a powerful and intuitive open-source framework meticulously designed for orchestrating intelligent, autonomous AI agents. It empowers developers to build sophisticated multi-agent systems that seamlessly collaborate, execute dynamic tasks, and integrate with diverse tools, transforming complex workflows into efficient, automated processes.

## ✨ Key Features
*   **Intelligent Agent Orchestration:** Define agents with distinct roles, goals, and backstories to foster specialized collaboration.
*   **Flexible Process Management:** Supports both sequential and hierarchical task execution, allowing for intricate workflow designs.
*   **Extensible Tool Integration:** Connects with a rich ecosystem of tools for diverse functionalities including web scraping, data access, automation, and more.
*   **Advanced Memory Management:** Implement contextual, entity, short-term, and long-term memory to enable deeper, more persistent agent intelligence.
*   **Retrieval Augmented Generation (RAG):** Integrate custom knowledge bases to ground agents' responses in specific, factual data, minimizing hallucinations.
*   **LLM Agnostic:** Compatible with various Large Language Models (LLMs) such as OpenAI, Anthropic, Google Gemini, Ollama, and custom models.
*   **Robust Guardrails:** Incorporate built-in hallucination detection and configurable output formatting to ensure reliable and aligned agent behavior.
*   **Comprehensive Observability & Evaluation:** Gain deep insights into agent performance, trace execution, and evaluate outcomes for continuous improvement.
*   **Developer-Friendly CLI:** Streamline project setup, deployment, and management with an intuitive command-line interface.

## Who is this for?
crewAI is built for visionaries who want to push the boundaries of AI. This includes:
*   **AI Engineers & Developers:** Crafting next-generation multi-agent applications.
*   **Researchers:** Exploring complex agentic collaboration patterns and workflows.
*   **Data Scientists:** Automating intricate analytical tasks and data pipelines.
*   **Organizations:** Seeking to deploy robust, scalable, and intelligent automation solutions in production environments.

## Technology Stack & Architecture
crewAI is built on a robust and modern stack, primarily leveraging Python for its flexibility and extensive AI/ML ecosystem.

*   **Core Language:** Python
*   **Data Validation & Modeling:** Pydantic
*   **Vector Databases (for RAG):** ChromaDB, Qdrant
*   **Memory Persistence:** SQLite
*   **LLM Integrations:** OpenAI, Anthropic, Google (Gemini models), Ollama, and custom LLMs.
*   **Tooling:** Integrates with a wide range of external tools, often via Langchain/Langgraph adapters.
*   **CLI:** Built with a user-friendly command-line interface for efficient development.

## 📊 Architecture & Database Schema

The core architecture of crewAI centers around a collaborative multi-agent system, dynamically orchestrating tasks to achieve complex goals.

```mermaid
graph TD
    A[User Goal/Input] --> B(The Crew: Orchestrates);
    B -- Defines & Manages --> C(Agents: Roles & Goals);
    C -- Assigns & Executes --> D[Tasks: Steps to Goal];
    D -- Utilize --> E(Tools: External Capabilities);
    C -- Accesses --> F(Memory: Contextual, Entity, Long/Short Term);
    C -- Consults --> G(Knowledge Bases: RAG);
    E, F, G --> H(LLMs: Reasoning & Generation);
    H --> D;
    D --> B;
    B --> I(Final Output/Result);
```

This diagram illustrates the flow: User inputs a goal, which is picked up by the **Crew**. The Crew orchestrates **Agents** (each with specific roles and goals) to perform **Tasks**. These Tasks may **Utilize Tools** for external interactions, and Agents can **Access Memory** (contextual, short-term, long-term) and query **Knowledge Bases (RAG)** for information. All these components interact with **LLMs** for reasoning and generation, ultimately leading to a **Final Output**.

## ⚡ Quick Start Guide

Get your first crewAI project up and running in minutes!

1.  **Installation:**

    ```bash
    pip install crewai
    ```
    or, if you prefer poetry:
    ```bash
    poetry add crewai
    ```

2.  **Basic Usage Example:**
    Set your OpenAI API key or configure another LLM of your choice.

    ```python
    import os
    from crewai import Agent, Task, Crew, Process
    from langchain_openai import ChatOpenAI

    # Set up your environment variables
    # os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"

    # Define your LLM (using OpenAI as an example)
    llm = ChatOpenAI(model="gpt-4o")

    # Define your agents
    researcher = Agent(
        role='Senior Research Analyst',
        goal='Uncover groundbreaking insights on a given topic',
        backstory='An expert in data analysis and market trends, capable of distilling complex information into actionable insights.',
        llm=llm,
        verbose=True,
        allow_delegation=False
    )

    writer = Agent(
        role='Content Strategist',
        goal='Craft compelling and engaging narratives based on research findings',
        backstory='A skilled storyteller with a knack for transforming dry data into captivating articles and reports.',
        llm=llm,
        verbose=True,
        allow_delegation=False
    )

    # Define your tasks
    research_task = Task(
        description='Investigate the latest AI advancements, focusing on generative models and their real-world applications.',
        agent=researcher,
        expected_output='A detailed report on AI advancements, including key technologies and applications.'
    )

    write_report_task = Task(
        description='Compose an engaging and informative report on AI advancements for a tech-savvy audience, drawing from the research findings.',
        agent=writer,
        context=[research_task],
        expected_output='A comprehensive, well-structured report with an introduction, key findings, and a conclusion.'
    )

    # Instantiate your crew
    project_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, write_report_task],
        process=Process.sequential, # Can also be Process.hierarchical
        verbose=True,
    )

    # Kickoff the crew
    print("🚀 Kicking off the AI Research & Report Crew...\n")
    result = project_crew.kickoff(inputs={'topic': 'Artificial Intelligence'})
    print("\n--- Final Report ---\n")
    print(result)
    ```

## 📜 License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.