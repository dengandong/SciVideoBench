# SciVideoBench: A Scientific Video Reasoning Benchmark for Multimodal LLMs  

**The First-Ever Benchmark for Scientific Video Reasoning and Understanding**  

[📄 Project Page](https://scivideobench.github.io/) | [📑 arXiv Paper]() | [📂 Dataset](https://huggingface.co/datasets/groundmore/scivideobench)

---

## 🔬 Overview  

Scientific experiments present unique challenges for video-language models (VLMs): precise perception of visual details, integration of multimodal signals (video, audio, transcripts), and complex reasoning across temporal scales. To address this gap, we introduce **SciVideoBench**, the first comprehensive benchmark dedicated to **scientific video reasoning**.  

SciVideoBench evaluates models across **Physics, Chemistry, Biology, and Medicine**, covering both **perceptual understanding** and **high-level reasoning** tasks. It provides a rigorous benchmark for evaluating long-form video reasoning in domains where accuracy and explainability matter most.  

---

## 📌 Key Features  

- **Domain Coverage**: 4 scientific disciplines (Physics, Chemistry, Biology, Medicine) with diverse experimental settings.  
- **Scale**: 1,000 high-quality, human-verified multiple-choice questions.  
- **Reasoning Dimensions**:  
  - *Conceptual Reasoning* – understanding principles and experimental setups.  
  - *Quantitative Reasoning* – extracting and reasoning with measurements, numbers, and calculations.  
  - *Hypothetical Reasoning* – counterfactual and “what-if” scientific scenarios.  
- **Rich Metadata**: Each QA pair is annotated with discipline, subject, timestamp breakdowns, and rationale.  
- **Evaluation Protocols**: Compatible with `lmms-eval` for standardized model comparison.  

---

## 📰 News  

- **2025.10** 🎉 SciVideoBench introduced as the **first benchmark for scientific video reasoning**.  

---

## 📂 Dataset  

- **Total Videos**: 240+ scientific experiments  
- **Disciplines**: Physics, Chemistry, Biology, Medicine  
- **QA Pairs**: 1,000 carefully curated multiple-choice questions  
- **Formats**: JSON/JSONL with video-level metadata and QA annotations  
- **Annotations**: Timestamp breakdowns, rationales, difficulty levels  

Example QA format:  

```json
{
  "video_id": "58827",
  "question_id": "1",
  "question": "What is the purpose of transferring the sample between chambers as shown between 02:22 and 02:33?",
  "options": {
    "A": "Align the sample with the deposition target",
    "B": "Cool the sample before deposition",
    "C": "Measure sample thickness prior to coating",
    "D": "Preserve main chamber vacuum integrity"
  },
  "answer": "D",
  "question_type": "Conceptual Reasoning",
  "discipline": "Chemistry",
  "subject": "Nanomaterials",
  "timestamp_breakdown": [...]
}
```

---

## 🧪 Evaluation (via lmms-eval)

SciVideoBench integrates directly with **[lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval)** using our task YAML and utils.py.

### 1) Install

```bash
# lmms-eval + vision extras
pip install -U lmms-eval
# or install from source (recommended)
# git clone https://github.com/EvolvingLMMs-Lab/lmms-eval.git
# pip install -e lmms-eval[all]
```

### 2) Repo Layout

```
scivideobench/
  configs/
    scivideobench.yaml        # ✅ task definition
  scivideobench/
    utils.py                  # ✅ dataloader, metrics, post-processing
  data/
    scivideobench.jsonl       # QA annotations
```

### 3) Quick Start

**API models (OpenAI, Azure, Gemini)**  

```bash
export OPENAI_API_KEY=...
export GEMINI_API_KEY=...

lmms-eval \
  --model openai/gpt-4o \
  --tasks scivideobench \
  --config configs/scivideobench.yaml \
  --output_dir results/gpt4o
```

**Local Hugging Face models (Qwen2.5-VL, InternVL-3)**  

```bash
lmms-eval \
  --model hf/Qwen/Qwen2.5-VL-7B-Instruct \
  --tasks scivideobench \
  --config configs/scivideobench.yaml \
  --output_dir results/qwen25vl_7b \
  --device cuda \
  --max_samples -1
```
---


## 📂 Dataset  

**License:**  

> SciVideoBench is only used for **academic research**. Commercial use in any form is **strictly prohibited**.  
> The copyright of all videos belongs to the **original video owners** and [JoVE](https://app.jove.com/).  
> If there is any infringement in SciVideoBench, please email us and we will promptly remove the content.  
> Without prior approval, you cannot distribute, publish, copy, disseminate, or modify SciVideoBench.  
> You must strictly comply with the above restrictions.  

Please send an email to **andong.deng@ucf.edu** for inquiries. ✨


## ✨ Citation  

If you use SciVideoBench, please cite our paper:  

```bibtex
@article{deng2025scivideobench,
  title={SciVideoBench: A Scientific Video Reasoning Benchmark for Multimodal LLMs},
  author={Deng, Andong and et al.},
  journal={arXiv preprint arXiv:2504.xxxxx},
  year={2025}
}
```