# End-to-end handwritten text recognition for early modern Spanish documents with LLM or Vision-Language Model pipeline creation

**GSoC 2026 Final Submission**

[![Live Demo](https://img.shields.io/badge/🤗%20Live%20Demo-Hugging%20Face%20Spaces-blue)](https://huggingface.co/spaces/aniket-junghare/spanish-handwriting-ocr)
[![LoRA Adapter](https://img.shields.io/badge/🤗%20Model-LoRA%20Adapter-yellow)](https://huggingface.co/aniket-junghare/qwen2.5-vl-spanish-ocr-lora)
[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](LICENSE)

📄 **Blog posts:** [Midterm Update](https://medium.com/@aniketjunghare999/building-an-end-to-end-vlm-driven-pipeline-for-reading-early-modern-spanish-handwriting-gsoc-2026-b307b89f5c92) · [Final Update](#) *(link once published)*

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
