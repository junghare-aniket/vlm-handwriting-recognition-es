# End-to-end handwritten text recognition for early modern Spanish documents with Vision-Language Model pipeline creation

**GSoC 2026 Final Submission**

[![Live Demo](https://img.shields.io/badge/🤗%20Live%20Demo-Hugging%20Face%20Spaces-blue)](https://huggingface.co/spaces/aniket-junghare/spanish-handwriting-ocr)
[![LoRA Adapter](https://img.shields.io/badge/🤗%20Model-LoRA%20Adapter-yellow)](https://huggingface.co/aniket-junghare/qwen2.5-vl-spanish-ocr-lora)
[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](LICENSE)

📄 **Blog posts:** [Midterm Update](https://medium.com/@aniketjunghare999/building-an-end-to-end-vlm-driven-pipeline-for-reading-early-modern-spanish-handwriting-gsoc-2026-b307b89f5c92) · [Final Update](https://medium.com/@aniketjunghare999/end-to-end-handwritten-text-recognition-for-early-modern-spanish-documents-with-vision-language-6d455fe35d92)

---

## **Abstract**

This project focuses on building an ***end-to-end Handwritten Text Recognition (HTR) pipeline*** for ***early modern Spanish manuscripts*** by placing a ***Vision-Language Model (VLM)*** at the center of every processing stage, rather than using it as a late-stage corrector. The system leverages ***Qwen2.5-VL-7B-Instruct*** with ***LoRA-based fine-tuning*** across a ***multi-task training strategy***, teaching the model both to ***faithfully read handwriting*** and to ***produce clean, corrected transcriptions***. A ***fine-tuned MIM-TrOCR model***, developed during ***GSoC 2025***, provides ***supplementary line-level evidence*** via ***OpenCV-based line segmentation***. The pipeline operates through ***four distinct stages***: ***document analysis***, ***line-level OCR***, ***literal reading***, and ***reconciliation/correction***, enabling robust transcription of ***degraded historical manuscripts***. Evaluated on the ***Rodrigo***, ***Orinoco***, and ***Tridis*** datasets, the system achieves competitive results. In the final phase of the project, the pipeline was also packaged into a ***publicly hosted, open-source web application***, deployed on ***Hugging Face Spaces***, making the tool usable directly from a browser with no local setup, contributing to the development of ***VLM-driven pipelines*** for ***historical document analysis*** and the ***digital preservation*** of ***Renaissance textual heritage***.

---
## **Try It Now**

A live, interactive version of the pipeline is hosted on **Hugging Face Spaces**:

**🔗 [huggingface.co/spaces/aniket-junghare/spanish-handwriting-ocr](https://huggingface.co/spaces/aniket-junghare/spanish-handwriting-ocr)**

Upload a scanned manuscript image and get a full transcription, with intermediate pipeline stages (document analysis, preliminary readings) viewable alongside the final result. No installation required, runs on Hugging Face's free ZeroGPU tier.

> **Note:** the deployed web app runs the leaner ***3-stage VLM-only pipeline*** by default (document analysis → literal reading → correction) to keep GPU usage within the free tier's quota. The optional ***4-stage pipeline with TrOCR*** (described below) is available when running the code locally with a TrOCR model configured, and is what's used for the full local `inference.py` / `evaluate.py` scripts and the benchmark results below.

---

##  **Repository Structure**

```
GSoC26/
├── README.md                                        # Project overview, approach, results, and usage guide
├── environment.yml                                 # Python dependencies
│
├── finetune.py                                      # Fine-tuning: LoRA training of Qwen2.5-VL-7B-Instruct
├── inference.py                                     # Inference: 4-stage VLM+TrOCR pipeline + visual output
│
├── scripts/
│   ├── run_finetune.sh                              # SLURM script for fine-tuning
│   ├── run_inference.sh                             # SLURM script for inference
│
├── models/                                          # Model weights (download separately)
│   ├── Qwen2.5-VL-7B-Instruct/                      # Base VLM model
│   ├── qwen2.5-vl-ocr-lora-handwritten              # LoRA adapter weights (output of finetune.py)
│
├── data/                                            # Datasets (download separately)
│   ├── Handwriting-scans/                           # Training images (used by finetune.py)
│   ├── Handwriting-transcriptions/                  # Training ground truth (used by finetune.py)
│   ├── test_images_handwritten/                     # Test images (used by inference.py)
|
└── results/                                         # Pipeline outputs
    ├── Visual_Results/                              # Side-by-side original vs transcription comparisons
```

---
