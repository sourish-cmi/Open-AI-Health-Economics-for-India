# Open AI Health Economics for India

An open-source AI toolkit for extracting, classifying, and querying *Indian public health documents* using **Small Language Models (SLMs) and Retrieval-Augmented Generation (RAG)**.

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
## Demo on YouTube

[![Watch Video](https://img.youtube.com/vi/dQw4w9WgXcQ/0.jpg)](https://youtu.be/e7eBdEUfBHY)

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

## Getting started

### Requirements

- Google Colab Pro with A100 GPU (40 GB VRAM)
- Google Drive with at least 10 GB free
- NFHS or other Indian health PDF documents to index

### Running order

Run the notebooks in sequence:

```
Notebook 1  →  Notebook 3  →  Notebook 4   (document classifier demo)
                          ↘
                           Notebook 5       (RAG chatbot)
```

Notebook 2 is standalone and documents the fine-tuning experiment. Currently, we do not have enough data and computing power to make the fine-tuning efficient. So we are relying on Few-Shot Learning  from Notebook 3. Once we able to fine tune the SLM and accuracy becomes better than that of Few-Shot learning, we will replace Notebook 3 by Notebook 2.

### Quick start : RAG chatbot only

If you already have a `extracted_chunks.csv` from Notebook 1, you can run Notebook 5 directly:

1. Upload `extracted_chunks.csv` to `MyDrive/.../data/`
2. Open `Notebook_5_RAG_Chatbot.ipynb` in Colab
3. Set runtime to A100 GPU
4. Run all cells — a public Gradio link appears at the end

---
## Results

| Approach | Task | Accuracy | Training required |
|---|---|---|---|
| Zero-shot prompting | 8-class classification | 43.3% | None |
| 8-shot few-shot prompting | 8-class classification | 53.3% | None |
| LoRA fine-tuning (200 samples) | 8-class classification | 26.7% | ~10 min |
| RAG generation | Question answering | Qualitative | None |

The fine-tuning result (26.7%) demonstrates that a minimum labelled corpus of ~1,000 samples per class is required for effective SLM adaptation — a finding that motivates the data collection work in this project.

---
## Data sources

This toolkit is designed to work with publicly available Indian health datasets:

- [NFHS-5 (2019–21)](http://rchiips.org/nfhs/nfhs5.shtml) — National Family Health Survey
- [NFHS-4 (2015–16)](http://rchiips.org/nfhs/nfhs4.shtml) — National Family Health Survey
- [Ayushman Bharat PM-JAY](https://pmjay.gov.in) — Health insurance scheme reports
- [National Health Accounts](https://mohfw.gov.in) — Ministry of Health and Family Welfare

> **Note on data:** NFHS microdata requires registration at [DHS Program](https://dhsprogram.com). The PDF reports are publicly available without registration.
> **Current version is developed on NFHS-4 and NFH-5 dataset.**
---
## Project structure

```
├── Notebook_1_Data_Pipeline.ipynb                              # PDF ingestion and chunking
├── Notebook_2_SLM_Finetuning.ipynb                             # LoRA fine-tuning experiment
├── Notebook_3_SLM_Few_Shot_Learning.ipynb                      # Few-shot evaluation
├── Notebook_4_Chatbot_Demo_for_Document_Classifier.ipynb       # Document classifier demo
├── Notebook_5_Conversational_Chatbot.ipynb                     # Conversational RAG chatbot
└── README.md
```
Data and model files are stored in Google Drive and are not committed to this repository.

---

## Known issues and limitations

- **Accuracy ceiling:** 53.3% few-shot accuracy reflects the difficulty of fine-grained thematic classification on domain-specific text without a large labelled corpus. A labelled dataset of 5,000+ examples is expected to push accuracy above 80%.
- **Scanned PDFs:** OCR quality varies. Tesseract performs well on clean scans but degrades on low-resolution or multi-column layouts.
- **Context window:** The RAG prompt is capped at 3,072 tokens. Very long questions with extensive chat history may truncate retrieved passages.
- **Colab session limits:** Colab Pro sessions disconnect after 12–24 hours. The FAISS index is saved to Drive and reloads instantly on reconnect.

---

## Contributing

Contributions are welcome. Priority areas:

- Additional Indian health document sources (ICMR, State Health Accounts, NSSO)
- Improved OCR pipeline for regional language documents
- Hindi and other Indic language support
- Evaluation on larger held-out test sets

Please open an issue before submitting a pull request.

---

## Current Team

1. Amiya R. Bhoumik, Institute of Chemical Technology, Mumbai
2. Anirban Chakraborti, JNU, New Delhi
3. Sourish Das, Chennai Mathematical Institute
4. Sukanya Das, TERI School of Advanced Studies, New Delhi
5. Pranabendu Misra, Chennai Mathematical Institute
6. Madhavan Mukund, Chennai Mathematical Institute
7. Areejit Samal, IMSc, Chennai
8. Ramaseshan Ramachandran, Chennai Mathematical Institute
9. Suchitra Karunkaran, AlgoLabs, Chennai
---

## Licence

This code is released under the **MIT Licence**. See [LICENSE](LICENSE) for details.

The base model (`microsoft/Phi-3.5-mini-instruct`) is also MIT licensed.
Sentence embedding model (`all-MiniLM-L6-v2`) is Apache 2.0.
FAISS is MIT licensed.

---

## Citation

If you use this toolkit in your research, please cite:

```bibtex
@misc{india-health-ai-2026,
   title  = {Open Health Economics Infrastructure for India: FAIR Datasets and Domain-Specific Small Language Models},
  author = {Bhoumik, Amiya R.; and Chakraborti, Anirban; and Das, Sourish; and Das, Sukanya; and Misra, Pranabendu; and Mukund, Madhavan; and Samal, Areejit},
  year   = {2026},
  note   = {AI for Science},
  url     = {https://github.com/sourish-cmi/Open-AI-Health-Economics-for-India},
  licence = {MIT}
}
```

---

## Acknowledgements

- [Microsoft Research](https://huggingface.co/microsoft) for Phi-3.5-mini-instruct
- [HuggingFace](https://huggingface.co) for the Transformers and PEFT libraries
- [Meta AI](https://github.com/facebookresearch/faiss) for FAISS
- [International Institute for Population Sciences](http://rchiips.org) for NFHS data
