# 妙笔生花 · Novel Agent

本地运行的 **长篇小说创作助手**：管理作品与章节、维护世界观与人物，集成 **DeepSeek** 等大模型辅助写作，并通过 **知识库（RAG）** 在写作时检索设定与资料。数据默认保存在本机，适合希望「打开即用、稿子在自己电脑上」的作者与爱好者。

> **分发形态**  
> 已支持 **Windows 压缩包**：解压后双击 **`MiaoBiShengHua.exe`** 启动内置 Web 服务，在浏览器访问 **`http://127.0.0.1:5000`** 即可使用，无需单独安装 Python。  
> 更详细的桌面端说明见 **`使用说明.txt`**（含管理员与普通用户区别、RAG 使用建议等）。

---

## 功能概览

| 模块 | 说明 |
|------|------|
| **作品与章节** | 多本小说、分章管理；维护世界观、人物、伏笔等创作素材 |
| **AI 辅助写作** | 基于兼容 OpenAI API 的服务（默认 DeepSeek）生成、续写与调整正文 |
| **知识库 RAG** | 上传 `.txt` 资料，写作时按相似度检索片段写入提示，减少设定冲突 |
| **账号体系** | 登录注册；新用户默认待 **管理员审核**；管理员可管理用户与部分知识库操作 |
| **产品介绍页** | 内置 `/about`，便于了解产品与设计理念 |

调用云端 API **需用户自备 API Key**（在「账号设置」中配置）。

**关于向量与 RAG）**

- **从源码运行（源码优化后上传Git）**：默认使用 **sentence-transformers**（如 BAAI/bge-small-zh-v1.5）+ **ChromaDB** 持久化；首次用嵌入时可能从 HuggingFace 拉取模型，请保持网络畅通（国内可配镜像）。
- **Windows 打包版（exe）**：默认使用 **本地哈希向量 + SQLite**（`data/rag_vectors.sqlite3`）做检索，**不依赖** Chroma 的 HNSW，也**不要求**为知识库去下 BGE；可选环境变量 `MIAOBI_TRY_ONNX=1` 尝试 ONNX MiniLM（需本机 ONNX 正常，且与哈希非同一向量空间，切换后需重建知识库）。详见 `使用说明.txt`。

---

## 下载安装 · Windows exe

1. 在 **[Releases](https://github.com/zhaimaoNB/novel-agent-pro/releases)** 下载最新 Windows 压缩包（请将链接改成你实际上传的仓库 Releases）。
2. 解压到任意目录（路径尽量不含特殊字符）。
3. 进入解压后的 **`MiaoBiShengHua`** 文件夹，双击 **`MiaoBiShengHua.exe`**。
4. 若防火墙提示，按需允许 **专用网络** 访问。
5. 浏览器打开 **`http://127.0.0.1:5000`**。

**数据存放**：作品、SQLite（`novels.db`）、上传文件、向量数据等默认在 **`exe 同目录下的 data\`**；卸载或换机前请自行备份整个 `data` 文件夹。

---

## 从源码运行 （待优化后上传）

1. Python **3.11+**，建议新建虚拟环境。
2. 安装依赖（以你项目内 `requirements.txt` 或实际冻结列表为准，例如）  
   `pip install -r requirements.txt`
3. 配置环境变量（可选）：首次无用户时可用 `ADMIN_USERNAME`、`ADMIN_PASSWORD` 创建管理员（见 `config.py`）。
4. 启动：  
   `python app.py`  
   默认监听 **`http://127.0.0.1:5000`**（`app.py` 中可为 `0.0.0.0`）。

---

## 首次使用提示

- 使用**管理员账号**登录；开放注册时，新用户需 **管理员审核通过** 后才能正常使用写作与知识库等页面。
- 在「**账号设置**」中填写 DeepSeek（或兼容接口）的 **API Key** 后再使用 AI 生成相关功能。
- **知识库不是「资料越多越好」**：精炼、与当前作品强相关的设定稿，通常比整本塞入更有效；详见 **`使用说明.txt`** 第四节。

---

## 技术栈（简要）

Python · Flask · SQLite · 兼容 OpenAI API 的聊天接口  

知识库实现：**开发环境** ChromaDB + sentence-transformers；**打包版** NumPy + SQLite 向量表（可选 ONNX 嵌入）。

---



## 联系与支持

- **作者**：宅子里的猫  
- **微信**：fengyu3061（技术交流或商务合作）

---

## 妙笔生花文创智能体交流群
### 扫码加入交流群
<img width="798" height="864" alt="image" src="https://github.com/user-attachments/assets/c302dacb-d152-4940-81a4-7d4860d056b7" />






## 致谢

感谢所有试用与反馈的朋友。
