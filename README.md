# Mathematical RAG: Searching My Maths Notes

A Python-based semantic retrieval prototype for finding relevant passages in mathematics PDFs and tracing them back to their source pages.

## Overview

Mathematical notes can be difficult to search using exact keywords, especially when a question is phrased differently from the original text. This project explores semantic search as a way to retrieve potentially relevant passages from mathematics documents.

Given a question, the system ranks text chunks by semantic similarity and displays the retrieved passages with their source filenames and page numbers.

**Scope:** This is a retrieval-focused prototype. It does not generate answers using a large language model or verify mathematical reasoning.

## How It Works

1. **PDF text extraction:** Uses `pypdf` to extract text page by page and retain source metadata.
2. **Text chunking:** Splits extracted text into chunks of 600 characters with 100 characters of overlap. Chunks remain associated with their source pages.
3. **Embedding generation:** Uses the `sentence-transformers/all-MiniLM-L6-v2` model to represent each chunk as a 384-dimensional vector.
4. **Similarity search:** Uses normalized embeddings and NumPy dot products to rank chunks by cosine similarity.
5. **Source-aware results:** Returns the top three passages with similarity scores, filenames, and page numbers.
6. **Interactive queries:** Allows multiple questions to be entered in a single session.

## Technologies

- Python
- Google Colab
- pypdf
- Sentence Transformers
- NumPy

## Testing and Experiments

The notebook includes synthetic tests for PDF text extraction, chunking, embedding generation, retrieval, and source attribution. The reported 22/22 checks passed for these built-in tests.

The retrieval pipeline was also explored using `ArtinAlgebra.pdf`, a real mathematics PDF. The document yielded 552 pages of extracted text and 3,237 chunks, represented by an embedding matrix of shape `(3237, 384)`.

Tested queries included questions about row reduction, equivalence relations, equivalence classes, and partitions. The retrieved passages included relevant material and source-page information for these examples.

These results describe the tested cases only. They are not a general retrieval-accuracy benchmark.

## Limitations

- Retrieval quality has not been evaluated on a large, labeled question set.
- The similarity threshold is a rough, uncalibrated setting, not a guarantee that a result is relevant.
- Scanned PDFs require OCR, which is not implemented in this notebook.
- Mathematical notation, tables, and symbols may not be extracted accurately from every PDF.
- The system retrieves passages; it does not generate answers or validate mathematical correctness.

## Running the Notebook

1. Open the notebook in Google Colab.
2. Run the setup and installation cells.
3. Upload a text-based mathematics PDF when prompted.
4. Wait for text extraction, chunking, and embedding generation to finish.
5. Enter a question and inspect the retrieved passages and their source pages.
6. Compare the retrieved text with the original PDF before relying on it.

If no PDF is uploaded, the notebook can use a small synthetic example for testing.

## What I Learned

Through this project, I explored how to build a semantic retrieval pipeline from individual components: extracting document text, chunking it while preserving metadata, representing text as vectors, and ranking passages using cosine similarity. I also learned the importance of testing components separately and checking retrieved results against their original sources.

## Future Improvements

- Evaluate retrieval using a labeled set of questions and relevant source passages.
- Compare chunk sizes, overlap settings, and embedding models.
- Improve the handling of mathematical notation and scanned documents.
- Calibrate the similarity threshold using evaluation data.

## Project Structure

This project is currently implemented as a Google Colab notebook.
