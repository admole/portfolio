---
title: "AI Chemistry Assistant with Scientific Tool Calling"
description: "An LLM powered chemistry assistant that is capable of calling molecular simulations through natural language."
date: "Jun 30 2023"
demoURL: "https://www.youtube.com/watch?v=NJFQGfBdixs"
repoURL: "https://github.com/admole/Wind-RL"
---


# AI Chemistry Assistant with Scientific Tool Calling

## Overview

This project explored the use of **Large Language Models (LLMs)** as intelligent interfaces for scientific computing by developing an AI-powered chemistry assistant capable of performing molecular simulations through natural language.

The assistant was built using **LangGraph** to orchestrate tool execution, allowing users to interact with computational chemistry software through a conversational interface. Given a chemistry-related request, the agent could generate molecular structures from SMILES strings, perform quantum chemistry calculations, and produce annotated molecular visualisations.

---

## The Challenge

Large Language Models are excellent at understanding natural language but cannot perform scientific calculations directly.

The objective of this project was to build an agent capable of:

* Understanding chemistry-related user queries
* Determining which computational tools were required
* Executing scientific workflows automatically
* Returning results in an intuitive format

Rather than acting as a chatbot alone, the LLM functioned as an **orchestrator**, coordinating specialised computational chemistry tools to answer user requests.

### Figure Placeholder

*Overall agent architecture*

---

## Agent Architecture

The assistant was implemented as a modular workflow using **LangGraph**.

Each user request passed through several stages:

```text
User Query
      ↓
Local LLM (Ollama)
      ↓
LangGraph Agent
      ↓
Tool Selection
      ↓
Scientific Computation
      ↓
Formatted Response
```

The graph-based architecture allowed individual tools to be invoked only when required while maintaining conversational context across interactions.

The system was designed to run entirely locally using **Ollama**, enabling private inference without reliance on external APIs.

### Figure Placeholder

*LangGraph workflow showing tool execution*

---

## Molecular Energy Calculator

The first tool performed basic quantum chemistry calculations from molecular input.

### Workflow

1. Accept a molecule as a **SMILES** string.
2. Generate a three-dimensional molecular geometry.
3. Perform an electronic structure calculation.
4. Return the calculated molecular energy.

Quantum chemistry calculations were performed using **PySCF**, allowing the assistant to provide physically meaningful energy values rather than relying on pre-computed data.

Example interaction:

```text
User:
Calculate the energy of ethanol.

Agent:
SMILES: CCO

Electronic Energy:
-154.012 Hartree
```

### Figure Placeholder

*Example molecular energy calculation*

---

## Molecular Visualisation

The second tool generated molecular structure images using **RDKit**.

For each calculation the workflow:

* Constructed the molecular structure
* Generated a 2D depiction
* Added molecular labels
* Included the calculated energy
* Exported the figure as an image

This allowed users to obtain both numerical and visual outputs from a single natural language request.

### Figure Placeholder

*Example annotated molecular visualisation*

---

## Workflow Orchestration

A key aspect of the project was allowing the LLM to determine which tools were required for each request.

For example:

```text
User:
Calculate the energy of benzene and show me the structure.

Agent:
✓ Parse molecule
✓ Generate structure
✓ Run PySCF calculation
✓ Create annotated image
✓ Return formatted results
```

This separation between reasoning and computation makes the system easily extensible, with additional scientific tools able to be integrated into the workflow without changing the user interface.

---

## Software Architecture

The project emphasised modularity and separation of responsibilities.

### LLM Layer

* Natural language understanding
* Conversation management
* Tool selection
* Response generation

### Scientific Tool Layer

* RDKit for molecular representations
* PySCF for quantum chemistry calculations
* Image generation and annotation

### Execution Layer

* LangGraph workflow orchestration
* Local inference using Ollama
* Robust error handling
* Validation of user inputs

This architecture keeps scientific computation deterministic while allowing the LLM to manage interaction and workflow execution.

---

## Technical Highlights

* Python
* LangGraph
* Large Language Models (LLMs)
* Ollama
* AI Agents
* Tool Calling
* RDKit
* PySCF
* Quantum Chemistry
* Molecular Visualisation
* Scientific Computing
* Workflow Orchestration

---

## Key Features

### Natural Language Interface

Users could request scientific calculations using conversational language without interacting directly with computational chemistry software.

### Automated Tool Selection

The LangGraph agent dynamically selected and executed the appropriate computational tools based on user intent.

### Local AI Inference

The entire application operated locally using Ollama, avoiding external APIs while improving privacy and reproducibility.

### Extensible Design

The modular workflow allows additional chemistry tools—such as geometry optimisation, frequency analysis or molecular property prediction—to be incorporated with minimal changes to the agent architecture.

### Figure Placeholder

*Example end-to-end conversation with the chemistry assistant*

---

## Impact

This project demonstrates how modern LLM frameworks can provide intuitive interfaces to established scientific software. By combining natural language reasoning with deterministic computational tools, the assistant bridges the gap between conversational AI and scientific simulation.

Although developed as a compact prototype, the architecture is readily extensible to more advanced scientific workflows and illustrates how AI agents can simplify access to domain-specific software while maintaining reproducible computational results.

