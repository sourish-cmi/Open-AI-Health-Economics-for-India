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

