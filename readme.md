# Looped

AI agent that tells you what's actually true inside your company — right now.
Internal knowledge is scattered across Google Docs, Confluence, Slack, and GitHub. Ask "how does our system work today?" and you get three docs that contradict each other, with no signal of which one is current.
Looped synthesizes fragmented internal documents into a single trusted answer — detecting conflicts, reasoning about freshness, and citing every claim so teams stop building on the wrong source of truth.

Note: Amazon Quick (launched April 2026) validates this problem space. Looped was designed independently in 2026 February as part of an AI PM program, with a focus on conflict detection and document trust layers — capabilities not present in general-purpose AI assistants.

## Core capabilities (MVP)
Natural language Q&A grounded in your internal docs
Conflict detection across document versions
Inline citations with freshness indicators
Explicit "I don't know" behavior when coverage is insufficient


## Problem

Internal knowledge is often fragmented across multiple documents, versions, tools, and teams. When someone asks, "How does our system work today?", there may be several scattered or conflicting documents with no clear signal of which one reflects the current state.

As a result, users often spend unnecessary time searching across documents, checking with senior teammates, or scheduling verification meetings just to confirm whether a source is still accurate.

Looped is designed to solve this problem by helping users get accurate, trustworthy knowledge based on what is true right now.

## Target Users

### 1. New Joiners

New engineers, product managers, or team members need to ramp up quickly on how systems work today.

They may find multiple versions of a design doc and have no easy way to know which one reflects the current state. What should be a quick self-serve lookup can turn into a meeting with a senior teammate.

### 2. Cross-Functional Collaborators

People from adjacent teams often need to understand how another system works before making requests or decisions.

For example, a category manager working on merchandising may need to understand why a product is ranked at the top of a search results page. Without access to decision history or system context, they may propose an approach that was already evaluated and declined months ago.

### 3. SMEs and Knowledge Owners

Senior engineers, tech leads, and domain owners repeatedly answer the same verification questions:

- "Is this still how it works?"
- "Which document is current?"
- "Why did we reject this approach before?"

Looped helps reduce repeated clarification work by making source-of-truth knowledge easier to discover, verify, and reuse.

## Why This Problem Matters

This is not just a search problem. It is a trust problem.

Existing knowledge tools can retrieve relevant documents, but they often do not resolve whether a document is current, whether multiple sources conflict, or why a past decision was made.

When users cannot trust documentation, they default to asking SMEs directly. This creates repeated verification meetings, duplicated proposals, onboarding friction, and organizational amnesia.

Looped focuses on the trust layer: identifying conflicts, surfacing current sources, showing citations, and making uncertainty explicit.

## Why Agentic AI

Determining what is current and trustworthy requires more than keyword search or static rules.

Documents may live across inconsistent versions, formats, and tools. Freshness cannot be determined by timestamp alone because a recently edited typo fix does not necessarily make a document more authoritative than an older approved architecture spec.

Looped requires multi-step reasoning across:

- retrieval,
- version analysis,
- conflict detection,
- source freshness,
- authority signals,
- synthesis,
- citation generation,
- uncertainty handling.

This makes the workflow better suited for an AI agent that can reason across unstructured inputs and orchestrate multiple steps dynamically.

## Core Workflows

### 1. Question → Trusted Answer

A user asks a natural-language question, such as:

> How does ranking in search results work on our website?

Looped generates an answer based on the current source of truth.

The answer includes:

- synthesized explanation,
- inline citations,
- source titles and metadata,
- confidence indicator,
- conflict warnings if sources disagree.

If conflicts exist, Looped explicitly surfaces both positions and explains which source it recommends using and why.

Example:

> Doc A states that algorithm X is used.  
> Doc B states that algorithm Y is used.  
> Looped recommends Doc A because it is more recent and approved, but flags the conflict for SME verification.

### 2. Follow-Up → Decision History

A user can ask follow-up questions, such as:

> Why did we switch from Y to X?

Looped retrieves relevant decision history from documents, meeting notes, Slack threads, or decision logs and explains the reasoning behind past changes.

### 3. Topic → Knowledge Brief

A user can request a broader knowledge brief, such as:

> Generate a knowledge brief on our ranking system.

Looped generates a structured document that includes:

- current state summary,
- key decisions and changes over time,
- unresolved conflicts,
- open questions,
- all cited sources,
- freshness indicators,
- generation date.

Generated documents are clearly labeled as AI-synthesized so they are not mistaken for human-authored source-of-truth documents.

### 4. User Feedback → Knowledge Improvement

Users can provide feedback when an answer is helpful, outdated, or incorrect.

SMEs can mark documents as deprecated or submit corrections. This feedback improves future retrieval, source ranking, and answer generation.

## Functional Requirements

### Trusted Answer Flow

| ID | Feature | Expected Behavior |
|---|---|---|
| P-1 | Natural-language query input | Users can ask questions in plain English. |
| P-2 | Multi-document retrieval | The system retrieves relevant documents across sources, not just the top-ranked result. |
| P-3 | Inline citations | Every key claim links back to source documents. |
| P-4 | Conflict detection | The system identifies when documents disagree and shows the conflicting positions. |
| P-5 | Confidence indicator | Each answer includes a confidence level based on source coverage, freshness, and conflicts. |
| P-6 | Follow-up conversation | Users can ask follow-up questions within the same session. |
| P-7 | Decision history surfacing | The system retrieves why decisions were made or changed over time. |
| P-8 | "I don't know" behavior | When evidence is insufficient, the system says what it could not find and suggests next steps. |

### Knowledge Brief Flow

| ID | Feature | Expected Behavior |
|---|---|---|
| S-1 | Knowledge brief generation | Users can request a structured document on a broad topic. |
| S-2 | AI-generated label | Generated documents clearly show they were created by Looped. |
| S-3 | Source freshness indicators | Each source includes freshness metadata. |
| S-4 | Conflict section | Unresolved conflicts are surfaced in a dedicated section. |
| S-5 | Change history timeline | The brief shows how the knowledge evolved over time. |

### Feedback Flow

| ID | Feature | Expected Behavior |
|---|---|---|
| F-1 | Thumbs up / down | Users can rate whether an answer was helpful. |
| F-2 | Outdated source flag | Users can flag a cited source as outdated. |
| F-3 | Correction suggestion | Users can submit corrections for SME review. |
| F-4 | Document deprecation | SMEs can mark documents as deprecated. |
| F-5 | Feedback loop visibility | The system shows how feedback improved future results. |

## Success Metrics

### North Star Metric

**Self-serve resolution rate**

The percentage of user queries resolved through Looped without requiring additional verification from an SME.

## Primary Metrics

| Metric | Definition | Target |
|---|---|---|
| Answer accuracy | Percentage of answers rated as correct or helpful | >80% |
| Citation coverage | Percentage of claims linked to source documents | >95% |
| Conflict detection recall | Percentage of actual document conflicts correctly identified | >80% |
| Freshness accuracy | Percentage of cases where the system correctly identifies the most current source | >90% |
| Hallucination rate | Percentage of unsupported claims generated by the system | <5% |

## Secondary Metrics

| Metric | What It Measures |
|---|---|
| Verification meeting reduction | Whether users ask SMEs fewer "is this still accurate?" questions |
| Repeat request reduction | Whether previously rejected ideas or feature requests are raised less often |
| Time-to-productivity for new joiners | Whether new team members ramp up faster |
| Weekly active queries | Whether users return to Looped as a recurring workflow |
| Feedback contribution rate | Whether users and SMEs actively improve the knowledge layer |

## Definition of Failure

Looped is failing if more than 50% of users still go back to an SME for verification after receiving an answer.

It is also failing if hallucination rate exceeds 5%, because unsupported claims are especially risky in a product that claims to identify the current source of truth.

## Differentiation

Looped is not a general enterprise AI assistant.

It focuses specifically on the trust layer for fragmented internal knowledge:

- detecting document conflicts,
- identifying the current source of truth,
- citing every major claim,
- surfacing uncertainty,
- preserving decision history,
- enabling SME feedback and document deprecation.

The goal is not only to find information, but to help users know whether the information can be trusted.

## Status

This repository currently documents the product concept, PRD direction, core workflows, functional requirements, and evaluation metrics for Looped.

Prototype implementation, system architecture, and roadmap may be added in future iterations.
