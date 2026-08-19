
##  **Repository Structure**

```
GSoC26/
├── README.md                                        # Project overview, approach, results, and usage guide
├── requirements.txt                                 # Python dependencies
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
    ├── Visual_Results/                              # Generated visual transcription images
    ├── Comparison/                                  # Side-by-side original vs transcription comparisons
    |── Rodrigo_evaluation_results.csv               # Evaluation CSV with per-image metrics 
    |── Orinoco_evaluation_results.csv               # Evaluation CSV with per-image metrics
    └── Tridis_evaluation_results.csv                # Evaluation CSV with per-image metrics
```

---
