# ReAct AI Agents Using LangGraph and CrewAI

A practical AI Agent project that demonstrates how to build **ReAct (Reason + Act) AI Agents** using **LangGraph** and **CrewAI** with a **Groq LLM** and a custom **Calculator Tool**.

---

##  Project Overview

This project demonstrates how an AI Agent can solve a **multi-step problem** by:

1. Understanding the user's question
2. Reasoning about what needs to be done
3. Deciding when to use a tool
4. Calling the Calculator Tool
5. Receiving the tool result
6. Using the result for the next step
7. Producing the final answer

The project implements this ReAct approach using two different AI Agent frameworks:

* **LangGraph**
* **CrewAI**

---

##  Project Aim

The main aim of this project is:

> **To create ReAct AI Agents using LangGraph and CrewAI that can solve a multi-step mathematical problem by using a Calculator Tool step by step.**

The Agent is designed not to calculate the numbers directly. Instead, it uses the Calculator Tool whenever a calculation is required.

---

##  What is ReAct?

**ReAct = Reason + Act**

ReAct is an approach where an AI Agent:

```text
User Question
      ↓
    Reason
      ↓
    Action
      ↓
  Use Tool
      ↓
 Get Result
      ↓
 Reason Again
      ↓
 Next Action
      ↓
 Final Answer
```

This allows an AI Agent to combine **reasoning** with **actions using external tools**.

---

##  Problem We Are Solving

The example question used in this project is:

> **What is 15 percent of 240, and then what is that result divided by 3?**

The Agent solves the problem in two steps.

### Step 1

15% of 240:

```text
240 × 0.15 = 36
```

The Calculator Tool performs:

```text
multiply 240 0.15
```

Result:

```text
36
```

### Step 2

The Agent uses the previous result:

```text
36 ÷ 3 = 12
```

The Calculator Tool performs:

```text
divide 36 3
```

Result:

```text
12
```

### Final Answer

```text
12
```

---

#  Project Architecture

The project contains two implementations of a ReAct AI Agent.

```text
                         USER QUESTION
                              |
                              ↓
                        ┌───────────┐
                        │  ReAct    │
                        │  AI Agent │
                        └─────┬─────┘
                              |
                 ┌────────────┴────────────┐
                 ↓                         ↓
          ┌─────────────┐           ┌─────────────┐
          │  LangGraph  │           │   CrewAI    │
          └──────┬──────┘           └──────┬──────┘
                 |                         |
                 ↓                         ↓
              Reason                    Agent
                 |                         |
                 ↓                         ↓
              Action                    Task
                 |                         |
                 └──────────┬──────────────┘
                            ↓
                    Calculator Tool
                            ↓
                       Tool Result
                            ↓
                      Reason Again
                            ↓
                       Final Answer
```

---

#  Part 1: LangGraph ReAct Agent

In the LangGraph section, we build a ReAct Agent using a graph-based workflow.

### Main Components

* **Groq API** – provides access to the LLM
* **LLM** – understands the question and decides what to do
* **Calculator Tool** – performs multiplication and division
* **AgentState** – stores messages and the number of steps
* **Reason Node** – asks the LLM what to do next
* **Action Node** – executes the Calculator Tool
* **Route** – decides whether to continue or stop
* **LangGraph** – controls the complete workflow

### LangGraph Flow

```text
START
  ↓
REASON
  ↓
ACTION?
 ┌───────┴───────┐
 │               │
YES              NO
 │               │
 ↓               ↓
ACT             END
 │
 ↓
REASON
 │
 ↓
FINAL ANSWER
 │
 ↓
END
```

The notebook defines the graph as:

```text
START → reason → (act → reason)* → END
```

---

# Part 2: CrewAI ReAct Agent

The second part uses **CrewAI** to create a ReAct-based Math Assistant Agent.

The CrewAI implementation contains:
 
```text
CrewAI Project
     |
     ├── Agent
     |
     ├── Task
     |
     ├── Tool
     |
     └── Crew
```

### Agent

The project creates a:

**Math Assistant**

Its goal is to answer mathematical questions by calling the Calculator Tool step by step.

### Task

The task tells the Agent to:

1. Calculate 15% of 240
2. Use the result
3. Divide the result by 3
4. Return the final numeric answer

### Tool

The project provides a custom:

**Calculator Tool**

It supports:

```text
multiply X Y
divide X Y
```

### Crew

CrewAI's `Crew` organizes the Agent and Task.

The project uses:

```text
Process.sequential
```

This means the task is executed in a sequential workflow.

---

#  Technologies Used

| Technology          | Purpose                                            |
| ------------------- | -------------------------------------------------- |
| **Python**          | Main programming language                          |
| **LangGraph**       | Builds and controls the graph-based Agent workflow |
| **CrewAI**          | Builds and manages the AI Agent                    |
| **Groq**            | Provides the LLM service                           |
| **LLM**             | Understands the question and performs reasoning    |
| **Calculator Tool** | Performs mathematical calculations                 |
| **Pydantic**        | Defines and validates tool input                   |
| **ReAct**           | Reason + Act approach                              |

---


# API Key

This project uses a **Groq API key**.

The API key should **never be written directly inside the notebook or uploaded to GitHub**.

The project uses an environment variable:

```python
os.environ["GROQ_API_KEY"]
```

When running the notebook, provide your own API key securely.

### Important

Never commit:

```text
GROQ_API_KEY=your_real_api_key
```

to a public GitHub repository.

---

# Project Structure

Recommended repository structure:

```text
ai-agents-langgraph-crewai/
│
├── ReAct_AI_Agents_LangGraph_CrewAI.ipynb
│
└── README.md
```

---

# How to Run

## 1. Clone the repository

```bash
git clone https://github.com/<your-username>/ai-agents-langgraph-crewai.git
```

## 2. Open the notebook

Open:

```text
ReAct_AI_Agents_LangGraph_CrewAI.ipynb
```

using:

* Google Colab
* Jupyter Notebook
* JupyterLab

## 3. Install the required libraries

The notebook installs the required packages for the project.

## 4. Add your Groq API key

Enter your own Groq API key when prompted.

## 5. Run the notebook

Run the cells from top to bottom.

---

# Expected Result

For the example question:

```text
What is 15 percent of 240, and then what is that result divided by 3?
```

The expected final result is:

```text
15% of 240 = 36

36 ÷ 3 = 12

Final Answer = 12
```

---



---

## Project

**Project Name:**
**ReAct AI Agents Using LangGraph and CrewAI**



