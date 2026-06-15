---
layout: post
title: "Drug Insights Platform: Architecture and Project Structure"
date: 2026-06-15
categories: [python, ai, streamlit, data-engineering]
tags: [drug-insights, vector-database, streamlit, ingestion, analytics]
permalink: /portfolio/druginsights-RAG/
author: "Oyetolu Zeenat"

---
[Back to Portfolio Website](https://oyetoluzeenat.github.io/)
[**View the Full Codebase on GitHub**](https://github.com/Oyetoluzeenat/druginsights)
---

# Drug Insights Platform: Architecture and Project Structure

## Overview

The Drug Insights Platform is a Python-based data intelligence application designed to extract, process, index, and analyze pharmaceutical and drug-related information. The project combines data ingestion pipelines, document extraction capabilities, vector database integration, agent-driven workflows, and a Streamlit user interface to provide actionable insights from structured and unstructured data sources.

The repository follows a modular architecture that separates user interfaces, ingestion workflows, core business logic, vector storage integrations, testing, and configuration management.

---

## Repository Structure

![drug_insights](/images/drug_insight_repository_structure.png)


## Development Environment

### `.devcontainer/`

The development container configuration enables consistent development environments across machines.

#### `devcontainer.json`

Defines:

- Container image configuration
- Development dependencies
- VS Code extensions
- Environment initialization settings
- Container startup behavior

This allows developers to quickly launch a fully configured workspace using Visual Studio Code Dev Containers or GitHub Codespaces.

---

## Streamlit Configuration

### `streamlit/`

Contains configuration files specific to the Streamlit application.

#### `secrets.toml`

Stores:

- API keys
- Database credentials
- Vector database access tokens
- External service configuration

Sensitive information should never be committed to source control.

---

## Data Processing Components

### `data/`

Contains document-processing utilities.

#### `pdf2.py`

Responsible for PDF extraction and preprocessing workflows.

Potential responsibilities include:

- Text extraction
- Metadata collection
- Document cleaning
- Section identification

#### `pdf3.py`

Provides additional PDF-processing capabilities such as:

- Advanced parsing
- OCR support
- Data normalization
- Structured content extraction

---

## Research and Experimentation

### `notebooks/`

Contains exploratory development assets.

#### `pinecone_integration_notes.ipynb`

Documents experimentation related to:

- Pinecone vector database integration
- Embedding generation
- Similarity search workflows
- Retrieval optimization strategies

This notebook serves as a knowledge base for future vector search enhancements.

---

## Data Ingestion Pipeline

### `scripts/`

Contains operational scripts and runtime configurations.

#### `config.json`

General application configuration including:

- Environment settings
- Processing parameters
- Integration options

#### `ingest_config.json`

Defines ingestion-specific behavior such as:

- Source locations
- Batch sizes
- Chunking strategies
- Embedding settings

#### `ingest_data.py`

Main ingestion entry point responsible for:

1. Loading source documents
2. Extracting content
3. Transforming data
4. Generating embeddings
5. Storing vectors
6. Updating search indexes

---

## Core Application Logic

### `src/`

Contains the primary source code for the platform.

### `agent/`

Implements intelligent agent functionality responsible for:

- Query orchestration
- Workflow coordination
- Context management
- Insight generation

### `drug_insight/`

Core business domain package containing:

- Domain models
- Processing services
- Insight-generation logic
- Application workflows

### `Druginsights.egg-info/`

Packaging metadata generated during installation and build processes.

### `extractors/`

Responsible for extracting information from source documents.

Typical functionality includes:

- PDF extraction
- Structured data parsing
- Metadata extraction
- Content normalization

### `loaders/`

Provides data-loading mechanisms for:

- Filesystems
- External APIs
- Cloud storage providers
- Local repositories

### `vector_db/`

Abstraction layer for vector database operations.

Responsibilities may include:

- Embedding storage
- Similarity search
- Index management
- Retrieval optimization

### `version.py`

Centralized version management for the application.

---

## Testing

### `test/`

Contains automated test suites.

#### `test_example_feature.py`

Demonstrates:

- Unit testing patterns
- Feature validation
- Regression testing practices

Automated tests help maintain reliability as the platform evolves.

---

## Root-Level Configuration Files

### `.env`

Stores environment variables such as:

- API keys
- Service endpoints
- Runtime configuration

### `.gitignore`

Defines files and directories excluded from version control.

### `LICENSE`

Specifies the project's legal usage terms.

### `pyproject.toml`

Modern Python packaging configuration that defines:

- Build system
- Dependencies
- Project metadata
- Tool configurations

### `requirements.txt`

Lists Python package dependencies required for execution.

### `setup.cfg`

Contains configuration for:

- Packaging
- Testing tools
- Linting
- Formatting

### `README.md`

Primary project documentation including:

- Installation instructions
- Usage examples
- Architecture overview
- Contribution guidelines

### `ui.py`

Application entry point for the user interface.

Likely responsibilities include:

- Streamlit application initialization
- User interaction workflows
- Visualization rendering
- Insight presentation

---

## High-Level Architecture

The platform follows a layered architecture:

1. **Data Sources** – PDF documents and external repositories.
2. **Loaders and Extractors** – Convert raw documents into structured content.
3. **Ingestion Pipeline** – Processes and prepares data for indexing.
4. **Vector Database Layer** – Stores embeddings and supports semantic retrieval.
5. **Agent Layer** – Coordinates retrieval and insight generation.
6. **User Interface** – Presents results through Streamlit.

This separation of concerns improves maintainability, scalability, and extensibility.

---

## Conclusion

The Drug Insights Platform demonstrates a well-structured architecture that combines document processing, vector search, intelligent agents, and an interactive web interface. Its modular organization enables independent development of ingestion workflows, retrieval systems, analytical components, and user-facing features while supporting future expansion into more advanced pharmaceutical intelligence and knowledge discovery capabilities.

[**View the Full Codebase on GitHub**](https://github.com/Oyetoluzeenat/druginsights)