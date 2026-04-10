# OpenClaw-Gene-Pool 🦞

这是一个开源的 **OpenClaw 基因库**，提供业界著名的“龙虾”核心基因文件。

# OpenClaw-Gene-Pool 仓库介绍
OpenClaw-Gene-Pool 是一个开源的 AI 智能体OpenClaw的“基因文件”集合仓库，以“龙虾（OpenClaw）”为生态标识，核心是通过标准化的 markdown 配置文件「标准化基因文件」，为 AI 智能体注入标准化的人格设定、能力体系与交互逻辑，是面向 AI 智能体工程化落地的配置文件库。

## 📄 核心内容
仓库按不同智能体场景划分了多个子目录（如 feishu-openclaw、stepclaw、AutoClaw 等），每个子目录下均包含一套完整的“基因文件”体系，覆盖 AI 智能体的核心维度：
- **SOUL.md**：定义 AI 智能体的核心逻辑基座与道德准则，是智能体的“灵魂”核心；
- **AGENTS.md**：规范智能体的任务分发规则、多智能体协作逻辑等核心运行机制；
- **TOOLS.md**：配置智能体可调用的外部工具与能力扩展，是智能体的“技能库”；
- **IDENTITY.md**：塑造智能体独特的语言风格、背景设定等身份特征；
- **USER.md**：记录用户偏好维度，支撑智能体实现个性化交互与记忆共鸣。



## 🧬 基因库 名单

> 💡 每个文件后括号内为 Git blob SHA（前7位），**相同 SHA = 完全相同的内容**，方便快速识别重复基因。

| OpenClaw 名字 | 文件地址 | 差异度 | 1. `SOUL.md` (灵魂核心) | 2. `AGENTS.md` (智能体设定) | 3. `TOOLS.md` (工具技能) | 4. `IDENTITY.md` (身份定义) | 5. `USER.md` (用户画像) |
| :--- | :--- | :---: | :--- | :--- | :--- | :--- | :--- |
| **feishu-openclaw** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/feishu-openclaw) | ⭐⭐⭐⭐⭐ | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/feishu-openclaw/SOUL.md) `73e1588` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/feishu-openclaw/AGENTS.md) `10c6365` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/feishu-openclaw/TOOLS.md) `319bb13` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/feishu-openclaw/IDENTITY.md) `0a80d28` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/feishu-openclaw/USER.md) `b62e151` |
| **kimiclaw** | [link](https://github.com/ericlinwang/openclaw-gene-pool/tree/main/kimiclaw) | ⭐⭐⭐ | [SOUL.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/kimiclaw/SOUL.md) `267d043` | [AGENTS.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/kimiclaw/AGENTS.md) `6e0f303` | [TOOLS.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/kimiclaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/kimiclaw/IDENTITY.md) `7a50791` | [USER.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/kimiclaw/USER.md) `5bb7a0f` |
| **Autoclaw** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/AutoClaw) | ⭐ | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/AutoClaw/SOUL.md) `792306a` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/AutoClaw/AGENTS.md) `25ee219` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/AutoClaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/AutoClaw/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/AutoClaw/USER.md) `5bb7a0f` |
| **Maxclaw** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/maxclaw) | ⭐ | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/maxclaw/SOUL.md) `792306a` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/maxclaw/AGENTS.md) `0b850df` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/maxclaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/maxclaw/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/maxclaw/USER.md) `5bb7a0f` |
| **stepclaw** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/stepclaw) | — | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/stepclaw/SOUL.md) `792306a` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/stepclaw/AGENTS.md) `887a5a8` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/stepclaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/stepclaw/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/stepclaw/USER.md) `5bb7a0f` |
| **Qclaw** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/QClaw) | — | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/QClaw/SOUL.md) `792306a` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/QClaw/AGENTS.md) `887a5a8` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/QClaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/QClaw/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/QClaw/USER.md) `5bb7a0f` |
| **WorkBuddy** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/WorkBuddy) | — | [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/WorkBuddy/SOUL.md) `792306a` | [AGENTS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/WorkBuddy/AGENTS.md) `887a5a8` | [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/WorkBuddy/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/WorkBuddy/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/WorkBuddy/USER.md) `5bb7a0f` |
| **easyclaw** | [link](https://github.com/ericlinwang/openclaw-gene-pool/tree/main/easyclaw) | — | [SOUL.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/easyclaw/SOUL.md) `792306a` | [AGENTS.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/easyclaw/AGENTS.md) `887a5a8` | [TOOLS.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/easyclaw/TOOLS.md) `917e2fa` | [IDENTITY.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/easyclaw/IDENTITY.md) `eb8d42c` | [USER.md](https://github.com/ericlinwang/openclaw-gene-pool/blob/main/easyclaw/USER.md) `5bb7a0f` |
---

## 全网爆火的 SKii 库 名单
| 序号| 类型 |skill名字| 链接 | 说明 | 
| :---| :---| :---  | :--- |:--- |
| 1| 职场、自媒体|女娲.skill| [link](https://github.com/alchaincyf/nuwa-skill) |自动蒸馏任何人的终极工具 | 
| 2| 职场、自媒体|同事.skill| [link](https://github.com/titanwings/colleague-skill) |把真实同事蒸馏成 AI（SKILL 流起点） | 




## 🦞社区有意思的龙虾（仅供学习参考）
![A股卡片](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/kapian.png)

| 🦐 OpenClaw 名字| 文件地址 | 1. `SOUL.md` (灵魂核心) | 2. `AGENTS.md` (智能体设定) | 3. `TOOLS.md` (工具技能) | 4. `IDENTITY.md` (身份定义) | 5. `USER.md` (用户画像) |
| :---| :---  | :--- | :--- | :--- | :--- | :--- |
| **A股利好监控的小龙虾** | [link](https://github.com/WangLin-Eric/openclaw-gene-pool/tree/main/A%E8%82%A1%E7%9B%91%E6%8E%A7)| [SOUL.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/SOUL.md) | [Agents.md ](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/AGENTS.md)| [TOOLS.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/TOOLS.md)| [IDENTITY.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/IDENTITY.md)| [USER.md](https://github.com/WangLin-Eric/openclaw-gene-pool/blob/main/A%E8%82%A1%E7%9B%91%E6%8E%A7/USER.md)|
---

## 仓库结构
仓库根目录下按不同智能体场景拆分出独立子目录（feishu-openclaw/stepclaw/AutoClaw/maxclaw/QClaw/WorkBuddy 等），每个子目录均配套上述全套“基因文件”；根目录 README.md 则通过表格清晰汇总了各子目录的文件地址与核心配置文件链接，便于快速查阅和使用。


## 🚀 快速开始

1. **下载**: 获取项目中的 `OpenClaw_Genes.zip`。
2. **集成**: 将 `.md` 文件内容注入到你的大模型 Prompt 框架或 Agent 系统中。
3. **自定义**: 根据场景需求微调 `IDENTITY.md` 以获得不同的人格表现。

   
## 🤝 贡献
欢迎通过 Issue 或 Pull Request 提交新的基因片段，共同完善龙虾 🦞 生态。
## 生态协作
仓库支持开发者通过 Issue 反馈需求、提交 Pull Request 贡献新的配置片段，共同完善基于“OpenClaw”体系的 AI 智能体配置生态。

---
