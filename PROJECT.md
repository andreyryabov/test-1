# Jokes + UI Components Assistant

## Overview
A simple agentic system with a main agent that tells jokes and a specialist that generates interactive UI components using NiceGUI. The main agent routes UI requests to the UI Widgets agent.

- Project name: `jokes-ui-assistant`
- Default agent: Main (Jester)
- MCP servers: Python MCP (for NiceGUI compilation, file I/O, HTML/iframe output)

## Agents
- Main (Jester) — Tells jokes directly; detects UI requests and delegates to UI Widgets.
- UI Widgets — Generates NiceGUI components and displays them via an iframe.

## Models
- Main: openai/responses/gpt-5-mini (fast routing and jokes)
- UI Widgets: openai/responses/gpt-5 (stronger code generation)

## MCP Servers
- Python MCP: execute_python_code, read/write files, install packages, generate HTML, compile NiceGUI widgets

## Handoff Logic
- If the user asks for UI components (widgets, forms, tables, dashboards), Main hands off to UI Widgets.
- Otherwise, Main responds directly with jokes.

## Mermaid Architecture Diagram
```mermaid
flowchart LR
  subgraph Users["User"]
    U["User"]
  end

  subgraph Agents["Agents"]
    direction TB
    Main["Main (Jester)<br/>(gpt-5-mini)"]
    Widgets["UI Widgets<br/>(gpt-5)<br/>compile_nicegui"]
  end

  subgraph MCP["MCP Servers"]
    PythonMCP["(Python MCP)<br/>(exec, read_file, html, nicegui)"]
  end

  U --> Main
  Main -->|"handoff when UI requested"| Widgets
  Widgets --> PythonMCP

  style Users fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
  style Agents fill:#fff3e0,stroke:#e65100,stroke-width:2px
  style MCP fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
  style Main fill:#fff9c4,stroke:#f9a825,stroke-width:2px
  style Widgets fill:#ffe0b2,stroke:#f57c00,stroke-width:2px
```

## Usage
- Tell jokes: "Tell me a tech pun" or "Give me 3 dad jokes about coffee".
- Generate UI: "Create a small NiceGUI with a button and a counter", "Build a form with a dropdown and a table".
