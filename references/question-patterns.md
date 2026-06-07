# Question Patterns Reference

Taxonomy of interview question types and generation rules for each category.

---

## 1. Warm-up Questions

Purpose: Break the ice, let the candidate settle in.

Patterns:
- "请做一个简短的自我介绍。"
- "能用 2-3 分钟介绍一下你简历上最有代表性的项目吗？"
- "为什么对这个岗位感兴趣？"
- "你最近在关注什么技术方向？"

Rules:
- Generate 1-2 warm-up questions
- Never start with a hard technical question
- One question should invite the candidate to pick their strongest project

---

## 2. Technical Deep-Dive

Purpose: Verify that listed skills reflect real understanding, not just keyword stuffing.

### Pattern A: Concept Verification
For each major skill listed, ask the candidate to explain it:

Template: "{Skill} 在你的简历中被提到，能解释一下它的核心原理吗？"
Examples:
- "LoRA 和全量微调的本质区别是什么？为什么你选择了 LoRA？"
- "Transformer 中 self-attention 的计算复杂度是多少？有什么优化方法？"
- "DPO 和 RLHF 的区别是什么？为什么你在这个项目中选择了 DPO？"

### Pattern B: Trade-off Analysis
Template: "在 {scenario} 中，你会选择 {option A} 还是 {option B}？为什么？"
Examples:
- "QLoRA 的 4-bit 量化会带来什么精度损失？你是怎么评估的？"
- "知识图谱 RAG 和纯向量检索 RAG 各有什么优劣？"
- "vLLM 和 TGI 在推理加速上有什么区别？"

### Pattern C: Depth Probe (Follow-up Chain)
When an answer is shallow, follow up:
1. "能再具体说说吗？"
2. "这个过程中遇到了什么问题？"
3. "如果参数调到 X 会怎样？"
4. "有没有做过消融实验验证这个选择？"

### Generation Rules:
- Generate 5-8 technical questions per resume
- Each listed framework/tool should have at least one question
- At least 2 questions should require explaining a concept from first principles
- At least 1 question should be a "why not X" trade-off question
- Mark each question with its follow-up chain (1-2 levels deep)

---

## 3. Project Walkthrough

Purpose: Understand the candidate's actual contribution depth, not just project description.

### Standard Project Question Set (pick 3-5 per project):

**Architecture & Design**
- "这个系统的整体架构是怎样的？能画一下数据流吗？"
- "为什么选择这个技术方案？考虑过哪些替代方案？"

**Your Contribution**
- "这个项目中你具体负责哪部分？哪些是你独立完成的？"
- "团队是如何分工的？你和其他成员如何协作？"

**Challenges & Problem-Solving**
- "项目中遇到的最大技术挑战是什么？你是怎么解决的？"
- "有没有做过不起作用的尝试？后来怎么调整的？"

**Results & Reflection**
- "你提到的 {metric} 是怎么衡量的？评估指标是什么？"
- "如果给你更多时间，你会怎么改进这个项目？"
- "从这个项目中你学到了什么？"

### Generation Rules:
- Map each bullet point on the resume to at least 1 question
- Quantified claims (numbers, percentages) must be questioned for methodology
- If a project mentions multiple technologies, ask about the integration challenges
- At least 1 "what would you do differently" question per major project

---

## 4. System Design

Purpose: Test ability to think at scale, beyond the specific project scope.

### Pattern: Extend a Resume Project
Take the candidate's most relevant project and extend it:

Examples:
- "如果这个系统要服务日均 100 万次请求，你会怎么设计？"
- "如果需要支持多语言，架构上需要做哪些改动？"
- "如何把这个离线评测系统改造成在线 A/B 测试框架？"
- "如果模型需要每周更新，如何设计持续训练和部署流水线？"

### Pattern: Classic System Design (role-relevant)
For ML roles:
- "设计一个大规模推荐系统的召回和排序模块"
- "设计一个多模态搜索系统"
- "设计一个模型的在线推理服务平台"

### Generation Rules:
- Generate 1-2 system design questions
- At least 1 should be an extension of an actual resume project
- Include expected discussion points (data layer, serving layer, monitoring)

---

## 5. Behavioral Questions

Purpose: Assess soft skills, teamwork, learning ability, and cultural fit.

Patterns:
- "描述一次你在团队中遇到分歧的经历，你是怎么处理的？"
- "你有没有一次尝试了很长时间但最终失败的经历？你从中学到了什么？"
- "你是怎么学习一个新的技术领域的？能举一个具体的例子吗？"
- "如果 deadline 很紧但技术方案还不成熟，你会怎么做？"
- "你认为自己最大的技术短板是什么？你打算怎么弥补？"

### Generation Rules:
- Generate 2-3 behavioral questions
- At least 1 should relate to the candidate's actual experience (from resume)
- At least 1 should be a general "how do you work" question

---

## 6. Reverse Questions

Purpose: Suggest thoughtful questions the candidate can ask the interviewer.

Good patterns:
- "这个岗位日常工作中最大的技术挑战是什么？"
- "团队目前的技术栈和基础设施是怎样的？"
- "新人入职后的第一个月通常会做什么？"
- "团队在 AI 方向上未来半年的规划是什么？"

### Generation Rules:
- Generate 2-3 reverse questions tailored to the target company/role
- Questions should show strategic thinking, not just curiosity
- Avoid questions easily answered by the job posting

---

## Difficulty Scaling

| Level | Technical % | "What" vs "Why" | Expected Depth |
|---|---|---|---|
| Junior | 60% what, 40% why | Know concepts, explain basics | Can describe what they did |
| Mid | 40% what, 60% why | Explain trade-offs, own decisions | Can explain why and alternatives |
| Senior | 20% what, 80% why | System thinking, challenge assumptions | Can propose better approaches |

Adjust question phrasing:
- Junior: "什么是 LoRA？"
- Mid: "LoRA 的秩 r 是怎么选的？不同 r 对效果有什么影响？"
- Senior: "LoRA 在大规模多任务场景下有什么局限性？你会怎么设计更好的 PEFT 方法？"
