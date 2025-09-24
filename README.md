# Document-QnA-with-RAG-and-Local-LLM
# 基于RAG和本地大模型的文档问答系统

本项目实现了一个先进的检索增强生成（Retrieval-Augmented Generation, RAG）系统，能够针对用户提供的特定文档内容进行精准的问答。

一大亮点是，整个系统完全依赖于**本地运行的开源大语言模型**（通过Ollama部署的Llama 3.1），确保了数据的私密性，并且没有任何API调用成本。

---

## 📖 项目概述 (Project Overview)

RAG技术通过“开卷考试”的方式，极大地提升了大语言模型回答问题的准确性和时效性。本项目旨在搭建一个完整的RAG流程，让AI成为任何一份文档的“问答专家”。
最终成果展示：<img width="1062" height="243" alt="Image" src="https://github.com/user-attachments/assets/7099519c-60e9-49ba-bfaf-72ee8e51c6ff" />
---

## 🚀 工作流程 (Workflow)

1.  **文档加载与切分 (Load & Chunk)**:
    * 加载指定的`.txt`格式的知识库文件。
    * 将文档切分成语义相关、大小合适的文本块（Chunks）。

2.  **嵌入与存储 (Embed & Store)**:
    * 使用开源的`Sentence-Transformers`模型，将每个文本块转换成能够代表其语义的“含义向量”（Embeddings）。
    * 将这些向量存入一个高效的本地向量数据库`FAISS`中，以便快速检索。

3.  **检索与生成 (Retrieve & Generate)**:
    * 当用户提问时，系统首先将问题也转换成一个向量。
    * 在`FAISS`向量数据库中，检索与问题向量最相似的文本块。
    * 将检索到的文本块作为上下文（Context），连同原始问题，一起提交给本地运行的Llama 3大模型。
    * Llama 3根据提供的上下文，生成最终的、精准的答案。

---

## 🛠️ 如何使用 (How to Use)

1.  **克隆或下载本仓库**。
2.  **安装Ollama并下载模型**:
    * 访问 [ollama.com](https://ollama.com) 下载并安装Ollama。
    * 在命令行中运行 `ollama pull llama3.1` (或其他你选择的模型) 来下载本地大模型。
3.  **安装Python依赖库**:
    ```bash
    pip install langchain langchain-community langchain-huggingface sentence-transformers faiss-cpu jupyterlab
    ```
4.  **准备知识库**:
    * 将你自己的知识内容，粘贴到仓库中的`.txt`文件里。
5.  **运行Jupyter Notebook**:
    * 确保Ollama应用正在后台运行。
    * 启动Jupyter Notebook/Lab，并打开`.ipynb`文件，按顺序执行所有单元格。

---

## 💻 技术栈 (Tech Stack)

* **Python 3**
* **LangChain**: 用于编排和实现RAG流程。
* **Ollama**: 用于在本地运行和管理大语言模型。
* **Llama 3.1**: 作为生成答案的核心大语言模型。
* **Sentence-Transformers**: 用于生成文本嵌入向量。
* **FAISS**: 用于构建本地向量数据库。
* **Jupyter Notebook**: 用于交互式开发和展示。