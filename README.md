# 🚀 crewAI

<p align="center"><img src="./docs/images/crewai_logo.png" alt="crewAI Logo" width="300"></p>

## Short Description
**crewAI** is an innovative open-source framework designed to orchestrate intelligent AI agents, enabling them to collaboratively solve complex problems. By defining roles, goals, and tools, developers can build powerful "crews" of agents that communicate, delegate tasks, and leverage external knowledge and tools to achieve a shared objective.

## ✨ Key Features
*   **Agentic Orchestration:** Define multi-agent systems with distinct roles, goals, and backstories for specialized expertise.
*   **Flexible Processes:** Supports both Sequential and Hierarchical task execution, allowing agents to delegate and manage sub-tasks effectively.
*   **Advanced Tooling:** Seamlessly integrate custom and pre-built tools (web scraping, search, file operations, database queries, AI/ML models) for comprehensive capabilities.
*   **Intelligent Memory & Knowledge:** Implement various memory types (short-term, long-term, contextual, entity) and integrate RAG-based knowledge bases (ChromaDB, Qdrant) for enhanced decision-making.
*   **LLM Agnostic:** Work with any Large Language Model, including OpenAI, Hugging Face, Gemini, Ollama, and more.
*   **Observability & Debugging:** Detailed event logging, tracing capabilities, and evaluation tools to monitor and refine agent performance.
*   **Human-in-the-Loop:** Configure tasks to require human input, allowing for guided execution and validation.
*   **Scalable & Deployable:** CLI tools for easy project creation, deployment, and management of agentic workflows.
*   **Enterprise-Ready:** Features like role-based access control (RBAC), hallucination guardrails, and robust integrations (Salesforce, HubSpot, GitHub, Slack) for production environments.

## Who is this for?
**crewAI** is built for developers, AI engineers, researchers, and businesses eager to push the boundaries of AI automation. If you're looking to:
*   Automate complex, multi-step workflows with autonomous AI.
*   Build AI applications that mimic human teamwork and specialization.
*   Create more reliable and auditable agentic systems.
*   Integrate AI seamlessly into existing business processes.
*   Experiment with advanced agent architectures and collaboration patterns.

...then **crewAI** is your definitive framework.

## Technology Stack & Architecture
**crewAI** is a Python-based framework leveraging modern AI and software engineering practices:

*   **Core Language:** Python
*   **Agent & Task Management:** Custom orchestration logic, influenced by concepts from Langchain and potentially LangGraph for advanced flows.
*   **LLMs:** Integrates with a wide array of LLMs via a flexible interface.
*   **Data Models:** Pydantic for robust data validation and serialization.
*   **Vector Databases:** ChromaDB and Qdrant for efficient RAG and knowledge retrieval.
*   **Cloud Storage:** S3 integration for file-based knowledge.
*   **CLI:** Built with `click` or similar for intuitive command-line interactions.
*   **Eventing System:** Custom event bus for logging, tracing, and callbacks.
*   **Testing:** Pytest and VCRpy for robust unit and integration testing.

## 📊 Architecture & Database Schema
```mermaid
graph TD
    A[User] --> B(Crew);
    B -- Orchestrates --> C[Agents];
    C -- Delegates/Executes --> D[Tasks];
    D -- Utilizes --> E[Tools];
    C -- Interacts with --> F[LLM Gateway];
    C -- Stores/Retrieves --> G[Memory];
    C -- Queries --> H[Knowledge Base];
    F -- Powers --> G;
    F -- Powers --> H;
    E -- Can access --> H;
    SubGraph Database Storage
        I[ChromaDB]
        J[Qdrant]
        K[SQLite]
        L[Cloud Storage (S3)]
        M[External DBs (e.g., MySQL)]
    End
    G -- Persists in --> I;
    G -- Persists in --> J;
    G -- Persists in --> K;
    H -- Retrieves from --> I;
    H -- Retrieves from --> J;
    H -- Retrieves from --> L;
    E -- Interacts with --> M;
```

## ⚡ Quick Start Guide
Get your first crew up and running in minutes:

1.  **Installation:**
    ```bash
    pip install crewai
    ```

2.  **Set up your LLM API Key:**
    Export your OpenAI API key (or equivalent for your chosen LLM):
    ```bash
    export OPENAI_API_KEY='YOUR_API_KEY'
    ```

3.  **Create your first Crew (e.g., a simple Research & Writer team):**
    ```python
    from crewai import Agent, Task, Crew, Process
    from langchain_openai import ChatOpenAI
    from langchain.tools import DuckDuckGoSearchRun

    # Initialize LLM
    openai_llm = ChatOpenAI(model_name="gpt-4", temperature=0.7)
    search_tool = DuckDuckGoSearchRun()

    # Define Agents
    researcher = Agent(
        role='Senior Researcher',
        goal='Uncover groundbreaking insights from the web',
        backstory='A meticulous researcher passionate about discovering new trends.',
        llm=openai_llm,
        tools=[search_tool],
        verbose=True
    )

    writer = Agent(
        role='Expert Writer',
        goal='Craft compelling and informative articles',
        backstory='A skilled communicator, known for transforming complex data into engaging narratives.',
        llm=openai_llm,
        verbose=True
    )

    # Define Tasks
    research_task = Task(
        description='Investigate the latest advancements in AI in 2024.',
        agent=researcher,
        expected_output='A detailed report on AI advancements, focusing on 3 key areas.'
    )

    write_task = Task(
        description='Write a compelling blog post based on the "AI Advancements Report".',
        agent=writer,
        context=[research_task],
        expected_output='A 500-word blog post, optimized for readability.'
    )

    # Form the Crew
    tech_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, write_task],
        process=Process.sequential, # Can be Process.hierarchical
        verbose=2 # Outputs agents' thought process
    )

    # Kickoff the Crew
    print("Crew starting to work on the tasks...")
    result = tech_crew.kickoff()
    print("\n########################")
    print("## Crew Finished Work ##")
    print("########################\n")
    print(result)
    ```

For more examples and advanced configurations, refer to the `docs/en/` directory.

## 📜 License
This project is licensed under the terms of the [LICENSE](LICENSE) file.