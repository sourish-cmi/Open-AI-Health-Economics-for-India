# Open AI Health Economics for India

An open-source toolkit for extracting, classifying, and querying Indian public health documents using Small Language Models (SLMs) and Retrieval-Augmented Generation (RAG).

Built on [`microsoft/Phi-3.5-mini-instruct`](https://huggingface.co/microsoft/Phi-3.5-mini-instruct) (MIT License) and designed to run on Google Colab Pro with an A100 GPU.

---

## What this project does

Indian public health data, NFHS surveys, Ayushman Bharat reports, state health accounts, ICMR publications; is rich but scattered across hundreds of unstructured PDFs. 

Note that the current version is built on `NFHS-4` and `NFHS-5` data. We will keep adding other sources continuously

This toolkit provides:

- **Automated PDF ingestion** : extracts and chunks text from digital and scanned health documents
- **Thematic classification** : assigns document passages to one of 8 health economics categories using few-shot prompting (53.3% accuracy, no fine-tuning required)
- **Conversational question answering** : a RAG chatbot that retrieves relevant passages and generates grounded natural language answers to health policy questions

