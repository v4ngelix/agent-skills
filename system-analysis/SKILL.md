---
name: system-analysis
description: Turn business/functional requirements for a software or IT system into a formal System Requirements Specification (SRS) document (IEEE 830-style) plus supporting technical diagrams (data flow, entity-relationship, sequence, and system architecture/context diagrams). Use this whenever the user wants to design a new system from requirements, write up a "system spec," "requirements spec," "SRS," "technical design doc," or asks to turn a set of business requirements or a stakeholder ask into a system design — even if they don't use those exact words, e.g. "we need to design a system for X," "help me spec out this app," "turn these requirements into a design doc," or "I need diagrams and a spec for the new platform." Always use this skill for that kind of to-be system design work rather than producing an ad hoc document, since it encodes the correct SRS structure and diagram set.
---

# System Analysis & Design Specification

This skill turns a set of business/functional requirements into two things a systems analyst would actually hand off to an engineering team:

1. A formal **SRS (System Requirements Specification)** document, structured along IEEE 830 lines
2. A set of supporting **technical diagrams**: system architecture/context, data flow (DFD), entity-relationship (ER), and sequence diagrams — embedded into the document as figures

Skip use case diagrams — this skill deliberately does not produce them.

## Why this matters

A requirements list on its own tells an engineering team *what* is wanted, but not how the pieces fit together, how data moves, what the data looks like, or how components interact over time. The SRS + diagram bundle turns loose requirements into something a dev team can actually build from without having to reverse-engineer the analyst's thinking. Getting the diagrams right (not just the prose) is the whole value of doing "system analysis" as opposed to just documenting a wish list.

## Workflow

### 1. Gather what's needed

Before drafting anything, make sure you understand:
- **What the system is and who it's for** — the product/system name, its purpose, and the primary users
- **Scope** — what's in bounds vs. explicitly out of scope for this version
- **Actors and external systems** — who or what talks to this system (end users, admins, third-party APIs, other internal systems)
- **Key data entities** — the core "things" the system tracks and how they relate (this feeds the ER diagram)
- **Key workflows** — the 2-4 most important interactions or processes (these feed the DFD and sequence diagrams)
- **Constraints and non-functionals** — performance, security, compliance, platform constraints, integration requirements

If the user has already supplied a batch of requirements (a doc, an email, a list of bullet points), extract everything you can from it first, and only ask about genuine gaps — don't re-ask for things already stated. If they're missing the basics (system name, purpose, scope), ask before drafting; don't invent a fictional product to fill the gap.

### 2. Draft the SRS document

Use the structure below (adapted from IEEE 830). Fill in every section — if something genuinely doesn't apply, say so briefly rather than omitting the section silently, since a reviewer expects to see it addressed.

```
1. Introduction
   1.1 Purpose
   1.2 Scope
   1.3 Definitions, Acronyms, and Abbreviations
   1.4 References
   1.5 Overview

2. Overall Description
   2.1 Product Perspective
   2.2 Product Functions (high-level summary — details go in section 3)
   2.3 User Characteristics
   2.4 Constraints
   2.5 Assumptions and Dependencies

3. Specific Requirements
   3.1 Functional Requirements (numbered, e.g. FR-1, FR-2 — one per distinct capability)
   3.2 External Interface Requirements (user interfaces, hardware, software, communications)
   3.3 Performance Requirements
   3.4 Design Constraints
   3.5 Non-Functional Requirements (security, reliability, availability, maintainability, etc.)

4. System Design (this is where the diagrams live)
   4.1 System Architecture / Context Diagram
   4.2 Data Flow Diagram(s)
   4.3 Entity-Relationship Diagram
   4.4 Sequence Diagram(s) for key workflows

5. Appendices (glossary, open issues, revision history — as relevant)
```

Number functional requirements individually (FR-1, FR-2, ...) — this is what lets an engineering team trace requirements to design elements later, and it's a hallmark of a real SRS vs. a casual write-up.

### 3. Generate the diagrams

Use **Mermaid** syntax for all diagrams, then render each to an image and embed it into the document (see step 4). Mermaid syntax to use per diagram type:

- **System architecture / context diagram** → `flowchart` (or `graph`) showing the system as a box, with external actors/systems around it and labeled connections. Keep it high-level: this diagram answers "what does this system talk to," not internal implementation.
- **Data flow diagram (DFD)** → `flowchart`, using rounded nodes for processes, cylinder/subroutine shapes for data stores, and plain nodes for external entities. Show one DFD per major workflow if there's more than one worth separating out; don't cram every workflow into a single unreadable diagram.
- **Entity-relationship diagram** → `erDiagram`, with entities, key attributes, and relationship cardinalities (`||--o{`, etc.).
- **Sequence diagram(s)** → `sequenceDiagram`, one per key workflow identified in step 1. Show the actors/components as participants and the calls between them in order.

Render Mermaid to PNG using the `mmdc` CLI (mermaid-cli):

```bash
npm install -g @mermaid-js/mermaid-cli --silent 2>/dev/null || npm install @mermaid-js/mermaid-cli --silent
npx mmdc -i diagram.mmd -o diagram.png -b white -s 3
```

If `mmdc` isn't available or fails in the environment, fall back to hand-drawn SVG (see the Visualizer's `diagram` module) rather than skipping the diagram — the diagrams are not optional decoration, they're half the deliverable.

### 4. Assemble the final document

Read `/mnt/skills/public/docx/SKILL.md` before building the document — it covers headings, styles, and how to embed images correctly. Build one `.docx` file containing the full SRS with each diagram embedded at the point in Section 4 where it's referenced, with a figure caption (e.g., "Figure 1: System Context Diagram").

Name the output file `<SystemName>_SRS.docx`.

### 5. Deliver

Save the final `.docx` to the outputs directory and present it. Briefly summarize what's in it (section count, number of functional requirements, diagrams included) rather than repeating the document's content back in chat.

## Things to get right

- **Don't invent requirements.** If the user's input is thin in a specific area (e.g., no non-functional requirements were mentioned), note it as an open item in the document rather than fabricating specifics like made-up performance numbers.
- **Keep diagrams scoped to what was actually discussed.** A context diagram with invented third-party integrations the user never mentioned is worse than a sparse-but-accurate one.
- **Functional requirements should be atomic and testable** — "The system shall allow a user to reset their password via email" is a good FR; "the system should be user-friendly" is not, and should be pushed into a qualitative section instead.
