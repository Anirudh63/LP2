# MeetingMind

Enterprise Meeting Intelligence

MeetingMind is an AI-powered meeting intelligence system designed to turn conversations into structured, searchable, and actionable organizational knowledge.

Instead of treating every meeting transcript as an isolated document, MeetingMind extracts decisions, action items, owners, and deadlines, while connecting them with relevant information from previous meetings.

## What I'm Building

Meetings generate a huge amount of information, but most of it becomes difficult to retrieve once the call ends.

MeetingMind explores how an AI system can:

- Extract meaningful decisions from messy conversations
- Identify action items and assign owners
- Detect deadlines and follow-ups
- Preserve speaker context during retrieval
- Search across an organization's meeting history
- Connect current discussions with decisions from previous meetings
- Automatically push useful information into existing workflows

The goal is to build something closer to an **organizational memory layer** rather than another meeting summarizer.

## The Journey So Far

### Lab 001 — Speaker-Aware Retrieval

Meetings aren't ordinary documents. Who said something matters.

MeetingMind uses speaker-aware chunking to preserve conversational context during retrieval and make relevant information easier to trace back to the original discussion.

### Lab 002 — Decisions & Action Items

Instead of simply summarizing a transcript, MeetingMind extracts structured information such as:

- Decisions
- Action items
- Owners
- Deadlines
- Follow-ups

This turns an unstructured conversation into information that can actually be acted upon.

### Lab 003 — Cross-Meeting Memory

A meeting shouldn't exist in isolation.

Using RAG with FAISS, MeetingMind can retrieve relevant information from previous meetings and provide context for current discussions.

This allows the system to connect today's conversation with decisions and discussions from the past.

### Lab 004 — Workflow-Based Reasoning

Meeting intelligence involves multiple steps rather than a single LLM call.

MeetingMind uses LangGraph to build a structured pipeline that can:

1. Process meeting transcripts
2. Extract decisions and action items
3. Assign owners
4. Detect deadlines
5. Search previous meetings
6. Identify relevant follow-ups
7. Generate summary emails

### Lab 005 — Organizational Knowledge Base

MeetingMind uses Pinecone for vector search with metadata filtering based on:

- Organization
- Team
- Date

This creates a searchable knowledge layer over an organization's meeting history.

The goal:

> Ask a question about what happened, and retrieve the relevant context.

### Lab 006 — Connecting With Existing Workflows

Information is only useful when it reaches people where they already work.

MeetingMind integrates with Slack and Notion through webhooks to automatically push meeting summaries and action items into existing team workflows.

## Architecture

```text
Meeting Transcript
        │
        ▼
Speaker-Aware Chunking
        │
        ▼
      RAG
   ┌────┴────┐
   ▼         ▼
 FAISS    Pinecone
   │         │
   └────┬────┘
        ▼
   LangGraph
   Pipeline
        │
   ┌────┼─────────────┐
   ▼    ▼             ▼
Decisions  Actions   Follow-ups
   │        │             │
   └────────┼─────────────┘
            ▼
     FastAPI Backend
            │
       ┌────┴────┐
       ▼         ▼
     Slack     Notion
