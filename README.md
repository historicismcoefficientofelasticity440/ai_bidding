# 🚀 AI-Bidding (AI智能招投标文档生成系统-一个简易的demo系统)

基于大语言模型 (LLM) 与检索增强生成 (RAG) 技术的智能辅助编写系统。本项目旨在解决传统招投标文件编写耗时长、历史资料利用率低等痛点，通过结合本地知识库高精度检索与大模型文本生成能力，实现招投标模块的自动化撰写、排版与导出。

> 目前本项目 **仅完成了核心后端业务逻辑与 AI 链路的开发，前端部分（UI/UX）完全处于待开发状态！**

---

## ✨ 核心功能 (Features)

* **🧠 RAG 知识库引擎 (`file_to_chroma.py`)**
    * 支持解析历史标书、规范文件等非结构化文档。
    * 自动进行文本切分与向量化提取，并持久化存储至本地 Chroma 向量数据库 (`chroma_db/`)。
    * 实现基于语义的高精度、毫秒级上下文召回。
* **🤖 智能标书撰写 (`qwen_client.py`)**
    * 深度对接阿里云通义千问 (Qwen) API。
    * 针对招投标垂直场景内置专业 Prompt 模板，将 Chroma 检索到的合规段落作为上下文注入，大幅降低大模型“幻觉”，确保内容专业合规。
* **📄 一键文档导出 (`md_to_word.py`)**
    * 定制化格式转换引擎，支持将大模型生成的 Markdown 文本流自动解析。
    * 支持复杂语法（表格、多级标题、列表等）到标准 Word (`.docx`) 格式的无损排版与导出，打通业务交付闭环。
* **🔐 用户与权限管理 (`users.py` & `bidding.db`)**
    * 基于 SQLite 的轻量级关系型数据存储。
    * 提供基础的用户认证、权限拦截与历史任务管理功能。

## 🛠️ 技术栈 (Tech Stack)

* **核心语言:** Python 3.9+
* **Web 框架:** 详见 `main.py` 与 `routes.py` (核心路由设计)
* **大语言模型:** 通义千问 (Qwen)
* **向量数据库:** ChromaDB (本地化运行)
* **关系型数据库:** SQLite (`bidding.db`)
* **文档处理:** `python-docx` / Markdown 解析库

## 📁 核心目录结构

```text
ai_bidding/
├── main.py                # 后端服务入口文件
├── routes.py              # 核心业务路由及 API 接口定义
├── users.py               # 用户认证与权限管理模块
├── qwen_client.py         # 大模型 API 封装与调用链路
├── file_to_chroma.py      # 知识库文档解析与 Chroma 向量化持久化
├── md_to_word.py          # Markdown 转 Word (.docx) 排版导出引擎
├── chroma_db/             # ChromaDB 向量数据库本地存储目录
├── bidding.db             # SQLite 关系型数据库文件
└── .env                   # 环境变量与敏感配置 (API Keys 等)
