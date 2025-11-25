---
layout: default
title: UBPD LLM Testimonial Classifier
description: Demo de clasificador de documentos testimoniales para la UBPD usando modelos de lenguaje grandes (LLM)
---

# Demo – UBPD LLM Testimonial Classifier / Clasificador de documentos testimoniales

[English](#english-version) · [Español](#versión-en-español)

---

## Badges

[![Status](https://img.shields.io/badge/status-demo-orange.svg)](#project-status)  
[![Language](https://img.shields.io/badge/language-Python-blue.svg)](#tech-stack)  
[![LLM](https://img.shields.io/badge/LLM-OpenAI%20GPT-lightgrey.svg)](#llm--prompt-design)  
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license)  

---

## Table of Contents

- [English Version](#english-version)
  - [Overview](#overview)
  - [Tech Stack](#tech-stack)
  - [Architecture](#architecture)
  - [Quick Start](#quick-start)
  - [LLM & Prompt Design](#llm--prompt-design)
  - [Evaluation & Next Steps](#evaluation--next-steps)
  - [Data Governance](#data-governance)
- [Versión en Español](#versión-en-español)
  - [Descripción general](#descripción-general)
  - [Tecnologías](#tecnologías)
  - [Arquitectura técnica](#arquitectura-técnica)
  - [Uso rápido](#uso-rápido)
  - [LLM y diseño de prompts](#llm-y-diseño-de-prompts)
  - [Evaluación y siguientes pasos](#evaluación-y-siguientes-pasos)
  - [Gobernanza de datos](#gobernanza-de-datos)
- [Project Status](#project-status)
- [License](#license)
- [How to Cite / Cómo citar](#how-to-cite--cómo-citar)

---

## English Version

### Overview

This project is a **prototype LLM-based classifier** for testimonial documents from the  
**Unidad de Búsqueda de Personas dadas por Desaparecidas (UBPD)** in Colombia.

The system loads a UBPD-oriented ontology defined in YAML, builds structured system/user prompts,  
and forces the model to return a controlled JSON output with:

- Document type  
- Types of events  
- Actors  
- Time period  
- Territory  
- Priority / internal routing  

The goal is to demonstrate how Large Language Models can support **early-stage analysis**  
of testimonial documents in contexts of enforced disappearance, transitional justice and humanitarian search.

---

### Tech Stack

- **Language:** Python  
- **LLM provider:** OpenAI (GPT family – configurable model)  
- **Config / ontology:** YAML  
- **Environment variables:** `.env` (with `.env.example`)  
- **Notebooks:** Jupyter / VS Code  
- **Intended use:** research & prototyping (not production)

---

### Architecture

Recommended repository structure:

```text
ubpd-llm-demo-clasificador-testimonios/
  notebooks/
    UBPD_Demo_Clasificador_Testimonios_autor.ipynb
  src/
    ubpd_classifier/
      __init__.py
      preprocessing.py
      ontology.py
      prompts.py
      classifier.py
  data/
    ontology/
      ontology_ubpd.yaml
  docs/
    arquitectura_clasificador_ubpd.md
  tests/
    test_classifier_minimo.py
  .env.example
  requirements.txt
  README.md   # (optional if using this index.md as main landing page)
```

Key components:

- `notebooks/UBPD_Demo_Clasificador_Testimonios_autor.ipynb`: interactive demo.  
- `src/ubpd_classifier/preprocessing.py`: basic text normalization.  
- `src/ubpd_classifier/ontology.py`: loads ontology from `ontology_ubpd.yaml`.  
- `src/ubpd_classifier/prompts.py`: builds system/user prompts from YAML.  
- `src/ubpd_classifier/classifier.py`: `classify_document(text)` + JSON validation.  
- `data/ontology/ontology_ubpd.yaml`: controlled vocabulary and categories.

---

### Quick Start

Install dependencies:

```bash
pip install -r requirements.txt
```

Set your environment (based on `.env.example`):

```text
OPENAI_API_KEY=your_key_here
```

Minimal usage from Python:

```python
from ubpd_classifier.classifier import classify_document

sample = """My brother disappeared in 1997 in rural Antioquia..."""
pred = classify_document(sample)
print(pred)
```

Run the notebook:

1. Start Jupyter or VS Code.  
2. Open `notebooks/UBPD_Demo_Clasificador_Testimonios_autor.ipynb`.  
3. Ensure `.env` contains your `OPENAI_API_KEY`.  
4. Execute the cells until the final example.

---

### LLM & Prompt Design

**Ontology-driven prompts**

- The UBPD ontology is defined in YAML and serialized into the system prompt.  
- The system prompt:
  - Defines a strict JSON schema.  
  - Lists allowed values for each field (document type, actors, etc.).  
  - Explains the classification criteria.  

- The user prompt:
  - Contains the raw or lightly preprocessed testimonial.  
  - Requests a JSON response following the ontology schema.

This approach aims for **structured, machine-consumable** outputs, not just free text.

---

### Evaluation & Next Steps

Planned evaluation strategy (requires annotated data):

- Precision / recall per category.  
- Confusion matrices for overlapping classes.  
- Agreement analysis between LLM and human annotators.  
- Stress tests with noisy, incomplete or ambiguous testimonies.  

Possible extensions:

- Add a small RAG pipeline for cross-document consistency checks.  
- Experiment with Spanish legal-domain embeddings.  
- Integrate with a document store or database used by UBPD or similar institutions.

---

### Data Governance

This demo uses synthetic or anonymized text.  
For real deployments in transitional justice or humanitarian settings, the system should enforce:

- Privacy and confidentiality for victims and families.  
- Data minimization (only necessary fields).  
- Secure storage and access controls.  
- Human-in-the-loop review before any operational decision.  
- Clear logging and audit trails for transparency.

These aspects are essential for **responsible AI** in sensitive contexts.

---

## Versión en Español

### Descripción general

Este proyecto es un **prototipo de clasificador basado en LLM** para documentos testimoniales  
de la **Unidad de Búsqueda de Personas dadas por Desaparecidas (UBPD)** en Colombia.

El sistema carga una ontología definida en YAML, construye prompts estructurados (system + user)  
y fuerza al modelo a devolver un JSON controlado con:

- Tipo de documento  
- Tipos de hechos  
- Actores  
- Periodo temporal  
- Territorio  
- Prioridad / ruteo interno  

El objetivo es mostrar cómo los modelos de lenguaje pueden apoyar el **análisis preliminar**  
de testimonios en contextos de desaparición forzada, justicia transicional y búsqueda humanitaria.

---

### Tecnologías

- **Lenguaje:** Python  
- **Proveedor LLM:** OpenAI (familia GPT – modelo configurable)  
- **Configuración / ontología:** YAML  
- **Variables de entorno:** `.env` (a partir de `.env.example`)  
- **Notebooks:** Jupyter / VS Code  
- **Uso previsto:** investigación y prototipado (no producción)

---

### Arquitectura técnica

Estructura sugerida de repositorio:

```text
ubpd-llm-demo-clasificador-testimonios/
  notebooks/
    UBPD_Demo_Clasificador_Testimonios_autor.ipynb
  src/
    ubpd_classifier/
      __init__.py
      preprocessing.py
      ontology.py
      prompts.py
      classifier.py
  data/
    ontology/
      ontology_ubpd.yaml
  docs/
    arquitectura_clasificador_ubpd.md
  tests/
    test_classifier_minimo.py
  .env.example
  requirements.txt
  README.md   # (opcional si este index.md es la página principal)
```

Componentes clave:

- `notebooks/UBPD_Demo_Clasificador_Testimonios_autor.ipynb`: demo interactiva.  
- `src/ubpd_classifier/preprocessing.py`: normalización básica del texto.  
- `src/ubpd_classifier/ontology.py`: carga la ontología desde `ontology_ubpd.yaml`.  
- `src/ubpd_classifier/prompts.py`: construcción de prompts system/user a partir de YAML.  
- `src/ubpd_classifier/classifier.py`: `classify_document(text)` + validación de JSON.  
- `data/ontology/ontology_ubpd.yaml`: vocabularios y categorías controladas.

---

### Uso rápido

Instalar dependencias:

```bash
pip install -r requirements.txt
```

Configurar variables de entorno (a partir de `.env.example`):

```text
OPENAI_API_KEY=tu_api_key_aqui
```

Uso mínimo en Python:

```python
from ubpd_classifier.classifier import classify_document

testimonio = """Mi hermano desapareció en 1997 en una vereda de Antioquia..."""
pred = classify_document(testimonio)
print(pred)
```

Ejecutar el notebook:

1. Iniciar Jupyter o VS Code.  
2. Abrir `notebooks/UBPD_Demo_Clasificador_Testimonios_autor.ipynb`.  
3. Configurar `.env` con tu API key.  
4. Ejecutar las celdas hasta el ejemplo final.

---

### LLM y diseño de prompts

**Prompts guiados por ontología**

- La ontología UBPD se define en YAML y se serializa en el system prompt.  
- El system prompt:
  - Define un esquema JSON estricto.  
  - Enumera los valores permitidos para cada campo.  
  - Explica criterios de clasificación.  

- El user prompt:
  - Contiene el testimonio crudo o preprocesado.  
  - Solicita un JSON conforme al esquema.

Esto busca producir salidas **estructuradas y procesables por máquina**,  
más allá de respuestas en lenguaje natural.

---

### Evaluación y siguientes pasos

Estrategia de evaluación (cuando exista un conjunto anotado):

- Precisión y recobrado por categoría.  
- Matrices de confusión en clases solapadas.  
- Análisis de concordancia entre personas anotadoras y LLM.  
- Pruebas con testimonios ruidosos, incompletos o ambiguos.  

Líneas de trabajo futuras:

- Integrar un pipeline RAG pequeño para consistencia entre testimonios.  
- Explorar embeddings legales en español.  
- Conectar con repositorios documentales o bases de datos institucionales.

---

### Gobernanza de datos

Aunque esta demo puede trabajar con texto sintético o anonimizado,  
un sistema real debe incorporar:

- Protección de datos sensibles de víctimas y familiares.  
- Minimización de datos personales.  
- Controles de acceso y cifrado donde aplique.  
- Revisión humana obligatoria antes de decisiones operativas.  
- Trazabilidad mediante logs y auditorías.

Estos elementos son indispensables para una **IA responsable**  
en contextos de justicia y derechos humanos.

---

## Project Status

This repository is a **research prototype / demo**.  
It is **not** intended as a production system.

You are welcome to:

- Fork the project.  
- Adapt the ontology to other institutions.  
- Replace the LLM provider or model.  
- Extend the evaluation toolkit.

---

## License

This project is licensed under the **MIT License**.

A typical `LICENSE` file would include:

```text
MIT License

Copyright (c) 2025  <Your Name>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
...
```

Replace `<Your Name>` with your actual name (e.g., **Manuel Daza Ramírez**)  
and place the full text in a top-level `LICENSE` file in your repository.

---

## How to Cite / Cómo citar

If you reference this demo in academic, technical, or policy work, you can cite it as:

> Daza Ramírez, M. (2025). *Demo – UBPD LLM Testimonial Classifier*.  
> Prototype repository exploring LLM-based classification of testimonial documents  
> for the Unidad de Búsqueda de Personas dadas por Desaparecidas (UBPD), Colombia.  
> Available at: GitHub (public repository).

Si lo citas en español:

> Daza Ramírez, M. (2025). *Demo – Clasificador de documentos testimoniales UBPD con LLM*.  
> Repositorio prototipo que explora la clasificación de testimonios mediante modelos de lenguaje  
> para la Unidad de Búsqueda de Personas dadas por Desaparecidas (UBPD), Colombia.  
> Disponible en: GitHub (repositorio público).

---
