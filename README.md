# Jarvis

Jarvis is an LLM chat application built to explore **stateful, multi-turn conversations**, **graph-based LLM orchestration**, and **interactive chat UIs**.  
The project serves as a hands-on environment for learning **LangGraph**, while revisiting **backend API design with FastAPI** and **frontend application architecture with React**.

Jarvis is intentionally scoped as a learning and experimentation platform rather than a polished consumer chat product.

**jarvis_be** = Backend - FastAPI, Python, LangGraph.

**jarvis_fe** = Frontend - React, TypeScript.

## Motivation & Learning Goals

Jarvis was started to better understand how real-world LLM chat systems work beyond simple request/response interactions.

The project focuses on three primary learning areas:

- **LLM orchestration**  
  Designing multi-step conversational workflows, managing execution state, and coordinating reasoning using LangGraph.

- **Frontend application development**  
  Building a React-based chat UI that supports streaming responses, thread navigation, and long-running conversations.

- **Backend APIs**  
  Designing REST APIs with FastAPI to support conversation lifecycles, persistence, and real-time interaction.

In addition, Jarvis is motivated by practical gaps encountered in existing LLM chat tools—particularly around **conversation navigation** and **usability in long threads**.

---

## High-Level Architecture

Jarvis consists of four main layers:

- **React Frontend (TypeScript)**  
  Manages the chat interface, thread navigation, and incremental rendering of streamed responses.  

- **FastAPI Backend**  
  Exposes APIs for managing projects, threads, messages, and streaming LLM responses.

- **LangGraph Orchestration Layer**  
  Models conversational workflows as a graph of nodes, enabling multi-step reasoning, tool execution, and checkpointed execution state.

- **Persistence Layer (SQLite)**  
  Stores threads, messages, project configuration, and workflow checkpoints to support long-running conversations across sessions.

---

## Conversation & State Structure

Jarvis explicitly structures conversational state to support long-running chats and future extensibility.

Core concepts:

- **Thread**  
  Represents an individual conversation and is the primary unit of interaction.  
  Threads can exist independently and persist their own message history and execution state.

- **Project**  
  Acts as an organizational layer for grouping threads.  
  Threads within a project share a common set of **project-level instructions**, which are automatically included in LLM requests.

- **Message**  
  A single user or assistant turn within a thread.

Current behavior:
- Threads do **not** share memory or conversation history
- The only shared project-level context is the project’s instructions
- Cross-thread memory is an explicit future consideration

---

## Workflow Orchestration (LangGraph)

Jarvis uses **LangGraph** to manage conversational workflows following a ReAct-style pattern.

This enables:
- Explicit modeling of conversational steps as graph nodes
- Multi-step reasoning and action execution
- Persistent execution state across turns via checkpointing
- Clear separation between preparation, reasoning, and response generation

---

## Frontend Focus & Streaming Interaction

Areas of focus include:
- Rendering streamed responses incrementally in the UI
- Managing thread-based conversations within and across projects
- Designing UI patterns for long-running and non-linear chats
- Iterating on component structure, state management, and UX clarity

Streaming is integrated end-to-end (LLM → backend → UI) and treated as part of the application flow rather than a standalone feature.

---

## Conversation Navigation (In Progress)

A major motivation for Jarvis is improving usability in long-running conversations.

Actively designing features:
- Conversation navigation with chapter-style anchors
- Search and retrieval within long chat threads
- Spawning new conversations from selected portions of existing chats

---

## Project Status & Roadmap

Jarvis is an active project.

Planned areas of exploration:
- Conversation navigation and retrieval
- Branching and spawned conversations
- Multi-modal support (e.g., images and other non-text inputs)
- External integrations (e.g., Google Docs, email APIs)
- Additional LLM provider support
- Continued iteration on frontend architecture and UX
