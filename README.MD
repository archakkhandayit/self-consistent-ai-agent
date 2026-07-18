# Self-Consistent AI Agent

A CLI-based AI application that improves response reliability by querying multiple LLM providers in parallel and generating a final consensus answer.

## How It Works

1. The user enters a query.
2. The query is sent simultaneously to multiple AI models.
3. Responses are collected using `Promise.allSettled()`, allowing the application to continue even if one provider fails.
4. Successful responses are normalized into a structured format.
5. A GPT model analyzes all candidate responses, identifies the most reliable one, and generates a final consensus answer.
6. The application outputs the synthesized response along with the provider considered most accurate.

## Interface

* CLI (Command Line Interface)
* No graphical user interface is used.

## Models / Providers

* Google Gemini (`gemini-3.1-flash-lite`)
* Groq (`llama-3.1-8b-instant`)
* Mistral (`mistral-medium-2508`)
* OpenAI GPT (used as the consensus model)

## Self-Consistency Flow

```text
User Query
     │
     ▼
Gemini ─┐
Groq ───┼──► Promise.allSettled()
Mistral ┘
              │
              ▼
   Filter Successful Responses
              │
              ▼
     GPT Consensus Model
              │
              ▼
        Final Answer
```

This approach increases robustness by comparing responses from multiple LLMs instead of relying on a single model, reducing the impact of individual model errors or biases.
