# Resume Interviewer

A Codex skill that simulates a senior technical interviewer — reads a candidate's resume and generates targeted, realistic interview questions.

## What It Does

Feed it a resume (PDF, DOCX, or plain text), and it produces a structured set of interview questions that a real interviewer would ask, covering:

- **Warm-up** — Self-intro, project overview
- **Technical Deep-Dive** — Probes real understanding of listed skills
- **Project Walkthrough** — Maps every resume bullet to a question
- **System Design** — Extends projects into larger-scale challenges
- **Behavioral** — Soft skills, teamwork, learning ability
- **Reverse Questions** — Thoughtful questions to ask back

## Features

- **Resume-aware**: Questions are derived from actual resume content, not generic
- **Follow-up chains**: Each question includes 1-2 levels of follow-up probes
- **Difficulty tuning**: Junior / Mid / Senior levels adjust question depth and phrasing
- **Role-specific**: Auto-detects target role (LLM, CV, NLP, Backend, etc.) and weights questions
- **Answer coaching mode**: Practice answering one question at a time with structured feedback
- **Bilingual**: Works with both Chinese and English resumes

## Installation

```bash
codex skill install resume-interviewer
```

Or manually clone into your skills directory:

```bash
git clone https://github.com/YOUR_USERNAME/resume-interviewer.git ~/.codex/skills/resume-interviewer
```

## Usage

### Basic: Generate Questions from Resume

```
帮我根据简历生成面试题
```

```
Prepare interview questions based on my resume at /path/to/resume.pdf
```

### Specify Difficulty

```
帮我生成高级难度的面试题
```

```
Generate junior-level interview questions from my resume
```

### Answer Coaching Mode

```
我想练习面试，一次问一道题，我回答后你给我反馈
```

```
Let's do a mock interview, ask me one question at a time and evaluate my answer
```

### Specify Target Role

```
我投的是大模型算法岗，帮我生成针对性的面试题
```

```
I'm applying for a CV engineer role, tailor the questions accordingly
```

## Output Example

```markdown
# 模拟面试题 — 潘瑞 / 大模型算法工程师

> 基于简历内容生成，共 18 题，覆盖技术深度、项目细节、系统设计、行为面试四大维度。

---

## 一、开场热身 (Warm-up)

### Q1. 请做一个简短的自我介绍，并用 2-3 分钟介绍你最有代表性的项目。
**考察点：** 表达能力、项目优先级判断、自我认知
**参考回答方向：** 选择与目标岗位最相关的项目，突出个人贡献和量化结果

---

## 二、技术深度 (Technical Deep-Dive)

### Q2. 你在项目中使用了 LoRA 对 Qwen2-VL-7B 进行微调。LoRA 的核心原理是什么？为什么选择 LoRA 而不是全量微调？
**考察点：** 对参数高效微调的理解深度
**追问：** LoRA 的秩 r 是怎么选的？不同 r 值对效果有什么影响？

### Q3. DPO 和 RLHF 都是偏好对齐方法，它们的核心区别是什么？你在什么场景下选择了 DPO？
**考察点：** 对齐方法的工程选型能力
**追问：** DPO 的 loss function 是怎样的？它有什么已知的局限性？
...
```

## How It Works

```
Resume (PDF/DOCX/Text)
    │
    ▼
┌─────────────┐
│  Parse       │  Extract: education, experience, projects, skills
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Signal      │  Identify: quantified claims, tech choices, vague areas
│  Extraction  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Question    │  Apply: pattern templates, difficulty scaling, role weighting
│  Generation  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Structure   │  Output: categorized Markdown with follow-ups and hints
│  & Format    │
└─────────────┘
```

## Project Structure

```
resume-interviewer/
├── SKILL.md                          # Core skill instructions
├── README.md                         # This file
├── references/
│   ├── question-patterns.md          # Question taxonomy & generation rules
│   └── evaluation-rubric.md          # Answer scoring criteria
└── examples/
    └── sample-output.md              # Example generated questions
```

## Requirements

- Codex CLI or Codex Desktop
- Python 3.8+ (for `.docx` resume parsing)
- `python-docx` package (only if parsing `.docx` files)

```bash
pip install python-docx
```

## Contributing

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/new-pattern`)
3. Add question patterns to `references/question-patterns.md`
4. Test with real resumes
5. Submit a pull request

### Adding New Question Patterns

To add patterns for a new role or domain, edit `references/question-patterns.md` and add a new section following the existing format. Include:
- Question template with `{placeholder}` syntax
- 2-3 concrete examples
- Generation rules (how many to produce, what to prioritize)

## License

MIT License. See [LICENSE](LICENSE) for details.

## Acknowledgments

Built as a [Codex Skill](https://github.com/openai/codex) — designed to make interview preparation accessible and personalized.
