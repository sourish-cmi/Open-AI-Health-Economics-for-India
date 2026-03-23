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

---

## Notebooks

| Notebook | Description | Open in Colab |
|---|---|---|
| `Notebook_1_Data_Pipeline.ipynb` | PDF extraction, chunking, and annotation pipeline | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kVjTi_nWaYiM2MNJ-G9f_960xgJluBMN?usp=sharing) |
| `Notebook_2_SLM_Finetuning.ipynb` | LoRA fine-tuning experiment on Phi-3.5-mini-instruct | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1wvqSLuUZUMkVBA0Oxz3rbuM0MuFuEp25?usp=sharing) |
| `Notebook_3_SLM_Few_Shot_Learning.ipynb` | 8-shot document classifier with evaluation and error analysis | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1isWE8w3r8RthQl7CJv-sHTT2RLJap6Qq?usp=sharing) |
| `Notebook_4_Chatbot_Demo_for_Document_Classifier.ipynb` | Gradio demo of the document classifier | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://drive.google.com/file/d/1NpCHi9bE1MApeQJTbo2RZdhKdE0p6Az0/view?usp=sharing) |
| `Notebook_5_Conversational_Chatbot.ipynb` | Conversational RAG chatbot over the document corpus | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://drive.google.com/file/d/18mKPaMZrxpiz__6xmzCEgUx-kWHKU357/view?usp=sharing) |

---

## Document categories

The classifier assigns health document passages to one of 8 thematic categories:

1. Child Health and Nutrition
2. Maternal Health
3. Nutrition and Biomarkers
4. Survey Methodology and Metadata
5. HIV/AIDS and Sexual Health
6. Sociodemographic and Household
7. Family Planning and Fertility
8. Women's Empowerment and Gender

---

## Technology stack

| Component | Library | Version | Licence |
|---|---|---|---|
| Language model | `transformers` | 4.44.0 | Apache 2.0 |
| SLM | Phi-3.5-mini-instruct | 3.8B params | MIT |
| LoRA fine-tuning | `peft` | latest | Apache 2.0 |
| Sentence embeddings | `sentence-transformers` | latest | Apache 2.0 |
| Embedding model | all-MiniLM-L6-v2 | 22M params | Apache 2.0 |
| Vector search | `faiss-cpu` | latest | MIT |
| Demo interface | `gradio` | latest | Apache 2.0 |
| PDF extraction | `pdfplumber` | latest | MIT |
| OCR fallback | `pytesseract` | latest | Apache 2.0 |

---
