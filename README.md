# SciVideoBench: Benchmarking Scientific Video Reasoning in Large Multimodal Models

[📄 Project Page](https://scivideobench.github.io/) | [📑 arXiv Paper]() | [📂 Dataset](https://huggingface.co/datasets/groundmore/scivideobench)

---

## 🔬 Overview  

Scientific experiments present unique challenges for video-language models (VLMs): precise perception of visual details, integration of multimodal signals (video, audio, transcripts), and complex reasoning across temporal scales. To address this gap, we introduce **SciVideoBench**, the first comprehensive benchmark dedicated to **scientific video reasoning**.  

SciVideoBench evaluates models across **Physics, Chemistry, Biology, and Medicine**, covering both **perceptual understanding** and **high-level reasoning** tasks. It provides a rigorous benchmark for evaluating long-form video reasoning in domains where accuracy and explainability matter most.  


<p align="center">
  <img src="figs/teaser.png" alt="SciVideoBench Overview" width="100%">
</p>

*Figure 1: The overall design of SciVideoBench, showing multi-stage data construction, annotation protocol, and evaluation pipeline.*  

---

## 🎥 Dataset Examples

<p align="center">
  <img src="figs/example.png" alt="SciVideoBench Dataset Examples" width="100%">
</p>

*Figure 2: Examples of SciVideoBench videos and their associated QA pairs across Physics, Chemistry, Biology, and Medicine.*  

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

### 1) Install (Please refer to lmms-eval)

```bash
# lmms-eval + vision extras
pip install -U lmms-eval
# or install from source (recommended)
# git clone https://github.com/EvolvingLMMs-Lab/lmms-eval.git
# pip install -e lmms-eval[all]
```

### 2) Repo Layout

After cloning **lmms-eval**, place the `scivideobench/` folder under `tasks/`:

```
lmms-eval/
  tasks/
    ├── activitynetqa/
    ├── ai2d/
    ├── aime/
    ├── air_bench/
    ├── ...
    ├── scivideobench/              # ✅ our benchmark lives here
    │   ├── scivideobench.yaml      # task definition(s) for evaluation
    │   ├── utils.py                # dataset loader, metrics, post-processing
    │   └── (optional) extra yaml   # if you split configs (chat, cot, etc.)
  ...
```

- **`scivideobench.yaml`** → Defines how `lmms-eval` loads SciVideoBench (dataset path, media fields, eval settings).  
- **`utils.py`** → Custom dataloader + evaluation metrics (accuracy, discipline/reasoning type breakdown).  
- You can create multiple YAMLs (e.g., `scivideobench_chat.yaml`, `scivideobench_cot.yaml`) if you want variants, similar to how `air_bench` has multiple YAMLs.  


### 3) Quick Start

**Local Hugging Face models (Qwen2.5-VL, InternVL-3, etc.)**  

```bash
accelerate launch --num_processes 8 --main_process_port 12380 -m lmms_eval \
    --model internvl3 \
    --config lmms-eval/lmms_eval/tasks/scivideobench/scivideobench.yaml \
    --model_args pretrained=OpenGVLab/InternVL3-2B,modality=video,num_frame=32 \
    --gen_kwargs=max_new_tokens=1024 \
    --tasks scivideobench \
    --batch_size 1 \
    --log_samples \
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
        title={SciVideoBench: Benchmarking Scientific Video Reasoning in Large Multimodal Models},
        author={Andong Deng and Taojiannan Yang and Shoubin Yu and Lincoln Spencer and Mohit Bansal and Chen Chen and Serena Yeung-Levy and Xiaohan Wang},
        journal={arXiv preprint arXiv:2501.XXXX},
        year={2025}
    }
```