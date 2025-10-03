# Research-Design-Plan Prompting Methodology

## Overview

This repository curates three prompt templates designed to drive a vertical-slice product workflow with ChatGPT and Copilot, progressing from discovery research to solution design and finally to slice-by-slice implementation planning.

## Step 1 — Research Prompt

The Step 1 template casts ChatGPT as a product research analyst, taking structured project inputs and generating an evidence-backed Product Requirements Document (PRD). It instructs the assistant to gather citations, surface assumptions and open questions, outline candidate vertical slices, sketch a data model, recommend stacks, and define risks, acceptance criteria, and out-of-scope items.

## Step 2 — Design Prompt

The Step 2 template positions ChatGPT as a solution architect who converts the Step 1 PRD into a Copilot-ready Technical Design Document (TDD). It calls for selecting a pragmatic stack, detailing the architecture, interfaces, domain model, data flow, tooling, and risks for the first vertical slice, while documenting assumptions, open questions, and an iteration plan consistent with the prior research.

## Step 3 — Planning Prompt

The Step 3 template treats ChatGPT as a senior developer crafting a build plan that translates the PRD and TDD into an executable, tests-first slice roadmap. It captures required inputs, emphasizes the “one failing test → cohesive surface → make it pass” loop, and specifies the structure of the slice plan (plan overview, global guardrails, quality and security expectations) even though the first enumerated instruction under “What to do” is truncated in the source file.

## Suggested Workflow

1. Fill in the Step 1 prompt with project context and run it (with browsing) to produce the research brief (step-1-research-output.md).
2. Feed the Step 1 output into the Step 2 prompt to generate a concise TDD aligned with the chosen slice strategy.
3. Combine the Step 1 and Step 2 artifacts in the Step 3 prompt to produce the detailed slice execution plan for implementation.