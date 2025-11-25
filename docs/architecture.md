---
layout: default
title: Architecture – UBPD LLM Classifier
---

# Architecture

This page describes the high-level architecture of the UBPD LLM testimonial classifier.

## Pipeline

1. Input testimonial text.
2. Preprocessing and normalization.
3. Ontology loading (YAML).
4. Prompt construction (system + user).
5. Call to the LLM provider (OpenAI).
6. JSON parsing and validation.
7. Optional post-processing and routing.

You can expand this page with diagrams (Mermaid, images) and further details.
