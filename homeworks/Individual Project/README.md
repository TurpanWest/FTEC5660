# FTEC5660 Reproducibility Assignment: nanobot Agent

This repository contains the reproduction work for the **nanobot** project, an ultra-lightweight agentic framework. 

**Original Project:** [HKUDS/nanobot](https://github.com/HKUDS/nanobot)

---

## Installation

**Important:** Since this assignment involves code modifications, please **install from source** using the steps below. Do not use `pip install nanobot-ai`.

### Prerequisites
*   Python 3.10+
*   Git

### Steps

1.  **Clone this repository** (if you haven't already):
    ```bash
    git clone https://github.com/TurpanWest/FTEC5660.git
    cd FTEC5660/homeworks/Individual%20Project/nanobot
    ```

2.  **Install in editable mode**:
    ```bash
    pip install -e .
    ```

3.  **Initialize the system**:
    ```bash
    nanobot onboard
    ```

---

## Configuration

To reproduce my results using **DeepSeek** (as documented in the report), please configure `~/.nanobot/config.json`.

1.  Open or create the config file:
    ```bash
    # Windows
    notepad %USERPROFILE%\.nanobot\config.json
    
    # Mac/Linux
    nano ~/.nanobot/config.json
    ```

2.  **Add your API Key**. 
    *Note: I used DeepSeek via an OpenAI-compatible endpoint. You can also use OpenRouter.*

    ```json
    {
      "providers": {
        "openai": {
          "base_url": "https://api.deepseek.com",
          "apiKey": "sk-YOUR_DEEPSEEK_KEY_HERE"
        }
      },
      "agents": {
        "defaults": {
          "model": "deepseek-chat",
          "provider": "openai"
        }
      }
    }
    ```

---

## Running the Agent (CLI Mode)

You can reproduce the modification directly in your terminal.

1.  **Start the Agent**:
    ```bash
    nanobot agent
    ```

2.  **Verify the Modification**:
    The agent has been modified to enforce a **Structured Planning Step**. To see this in action:
    
    *   **Input:** Ask a complex question, e.g., *"Plan a romantic dinner for two with $50."*
    *   **Observation:** The agent will output a `[PLANNING]` block (analyzing the request and tools) *before* giving the final answer.

    *(Note: In the original codebase, the agent would typically skip planning and provide the menu directly.)*

---

## 🧪 Reproduction Summary

### 1. What I Reproduced
*   **Tool Use**: Financial analysis using external search/APIs.
*   **Code Execution**: Generating and running local Python scripts (Fibonacci sequence).
*   **Memory**: Long-term entity recall (Name/Major) after distraction.

### 2. My Modification
*   **Modified File**: `nanobot/agent/context.py`
*   **Method**: User Message Injection (appending constraints to `_build_user_content`).
*   **Impact**: Forces the LLM to adhere to a "Chain of Thought" process, improving interpretability.