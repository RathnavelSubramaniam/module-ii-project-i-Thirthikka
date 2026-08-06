[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/CtKjnZeu)


## Problem Statement
Healthcare professionals face information overload when trying to find accurate,
timely answers from large medical references. This project builds an AI-based
Q&A system to streamline access to trusted medical knowledge and support faster,
evidence-based clinical decisions.

## Objective
Develop and evaluate a Retrieval-Augmented Generation (RAG) solution over the
Merck Manuals to reduce hallucination and improve the reliability of AI-generated
medical answers compared to a standalone LLM.

## Data
- **Source:** Merck Manuals (PDF, 4,000+ pages, 23 sections)
- Covers disorders, diagnoses, tests, and drug information

## Approach
1. **Baseline (Prompt Engineering):** Query LLaMA-2 13B Chat (GGUF, via
   llama-cpp-python) directly using its pre-trained knowledge — no external data.
2. **RAG Pipeline:**
   - Chunk and embed the Merck Manuals using HuggingFace sentence-transformers
   - Store embeddings in a Chroma vector store
   - Retrieve relevant chunks per query and generate grounded answers with the
     same local LLaMA-2 model
3. **Evaluation:** LLM-as-a-Judge scoring for **relevance** and **groundedness**
   (1–5 scale), comparing baseline vs. RAG outputs across four test questions:
   - Sepsis management protocol (critical care)
   - Appendicitis symptoms and treatment (general surgery)
   - Patchy hair loss causes and treatment (dermatology)
   - Traumatic brain injury treatment (neurology)

## Key Findings
- Baseline LLM: high relevance (4–5/5) and surprisingly high groundedness
  (4–5/5) from parametric knowledge alone, but with no source citations.
- RAG: matched/improved groundedness by anchoring answers directly in Merck
  Manual excerpts, eliminating hallucination risk and enabling verifiable,
  source-backed responses.

## Recommendations
- Add hybrid retrieval (BM25 + vector similarity) for better handling of
  technical terms, dosages, and abbreviations.
- Build automated evaluation pipelines to continuously monitor groundedness/
  relevance before production deployment.

## Stack
`llama-cpp-python` · `LLaMA-2-13B-Chat (GGUF)` · `LangChain` · `Chroma` ·
`HuggingFace sentence-transformers`
