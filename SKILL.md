---
name: resume-interviewer
description: >
  Simulate a senior technical interviewer who reads a candidate's resume (PDF, DOCX, or plain text)
  and generates targeted interview questions. Use when the user asks to "prepare for interview",
  "模拟面试", "根据简历提问", "interview questions from resume", "面试模拟", "简历提问",
  or wants to practice answering questions about their own resume, CV, or background.
  Covers technical depth, project walkthroughs, system design, behavioral, and role-specific questions.
---

# Resume Interviewer

Simulate a realistic technical interviewer. Read the candidate's resume, extract key signals, and generate interview questions that a senior engineer or hiring manager would actually ask.

## Workflow

### 1. Parse Resume

Read the resume file (supports `.docx`, `.pdf`, `.md`, `.txt`, or pasted text). Extract structured data:

| Field | What to look for |
|---|---|
| Education | School tier, degree, major, research direction |
| Work/Internship | Company, role, duration, responsibilities, metrics |
| Projects | Name, tech stack, your specific contribution, quantified results |
| Skills | Languages, frameworks, tools, domains |
| Publications/Patents | If present — title, venue, relevance |

If the resume is in a `.docx` file, extract text with Python:

```python
from docx import Document
doc = Document('path/to/resume.docx')
text = '\n'.join(p.text for p in doc.paragraphs if p.text.strip())
```

### 2. Identify Question Targets

For each resume section, identify **high-signal items** — things an interviewer would probe:

- Quantified claims (e.g., "accuracy improved to 99.2%") — ask how measured, what baseline, what ablation
- Technical choices (e.g., "used LoRA") — ask why not full fine-tuning, how hyperparams chosen
- Vague contributions (e.g., "responsible for model training") — ask for specifics
- Impressive results — ask what was hardest, what failed first, what you'd do differently
- Stack choices — ask trade-offs, why this over alternatives

### 3. Generate Questions

See [references/question-patterns.md](references/question-patterns.md) for the full question taxonomy and generation rules.

Produce questions in this order:

1. **Warm-up** (1-2 questions) — Self-intro, project overview, motivation
2. **Technical Deep-Dive** (5-8 questions) — Based on specific skills and tech claims
3. **Project Walkthrough** (3-5 questions per project) — Architecture, decisions, trade-offs, failures
4. **System Design** (1-2 questions) — Extend a project into a larger system
5. **Behavioral** (2-3 questions) — Teamwork, conflict, learning from failure
6. **Reverse Questions** (2-3 suggestions) — What the candidate should ask the interviewer

### 4. Output Format

Output all questions as a structured Markdown document:

```markdown
# 模拟面试题 — [Candidate Name] / [Target Role]

> 基于简历内容生成，共 N 题，覆盖技术深度、项目细节、系统设计、行为面试四大维度。

---

## 一、开场热身 (Warm-up)

### Q1. [Question text]
**考察点：** [What this tests]
**参考回答方向：** [Brief hint — not a full answer]

---

## 二、技术深度 (Technical Deep-Dive)

### Q2. [Question text]
**考察点：** [What this tests]
**追问：** [Follow-up if candidate gives shallow answer]
...

---
```

Repeat the structure for all categories. End with:

```markdown
## 六、你可以反问的问题 (Reverse Questions)

1. [Question 1]
2. [Question 2]
3. [Question 3]

---

> 💡 **使用建议：** 每道题给自己 2-3 分钟组织回答，录音回听效果更佳。
```

### 5. Difficulty Tuning

Default difficulty targets a mid-level candidate with 1-2 years experience. Adjust on request:

- **初级 (Junior)**: Focus on fundamentals, "what" questions, basic concept explanations
- **中级 (Mid-level)**: Mix "what" and "why", expect trade-off analysis, probe project ownership
- **高级 (Senior)**: Focus on "why not", system-level thinking, expect candidates to lead the discussion

### 6. Role-Specific Customization

Detect the target role from the resume's job intent line or user request, and weight questions accordingly:

| Role | Emphasis |
|---|---|
| 大模型算法 | Training pipeline, alignment methods, scaling laws, inference optimization |
| 多模态 | Vision-language architecture, cross-modal alignment, dataset construction |
| NLP | Tokenization, language modeling, prompt engineering, evaluation |
| CV | Backbone networks, detection/segmentation, data augmentation, deployment |
| 后端/全栈 | System design, API design, database, distributed systems |
| 数据工程 | ETL, data quality, pipeline orchestration, storage |

## Answer Coaching Mode

If the user wants to practice answering (not just see questions), offer this mode:

1. Ask one question at a time
2. Wait for the user's answer
3. Evaluate the answer against [references/evaluation-rubric.md](references/evaluation-rubric.md)
4. Give structured feedback: strengths, gaps, improved sample answer
5. Move to next question

## Batch Mode

If the user provides multiple resumes or asks to generate a question bank, produce all questions in a single document grouped by resume section, suitable for printing or sharing.
