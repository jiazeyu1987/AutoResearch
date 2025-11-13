# 微舆 (BettaFish) 项目指南

## 项目概述

"微舆"（BettaFish）是一个从零实现的创新型多智能体舆情分析系统，旨在帮助用户破除信息茧房，还原舆情原貌，预测未来走向，辅助决策。用户只需像聊天一样提出分析需求，智能体就会全自动分析国内外30+主流社媒与数百万条大众评论。

项目具备六大核心优势：
1. **AI驱动的全域监控**：AI爬虫集群7x24小时不间断作业，全面覆盖微博、小红书、抖音、快手等10+国内外关键社媒
2. **超越LLM的复合分析引擎**：融合5类专业Agent、微调模型、统计模型等中间件
3. **强大的多模态能力**：深度解析短视频内容，精准提取结构化多模态信息
4. **Agent"论坛"协作机制**：通过"论坛"机制进行链式思维碰撞与辩论
5. **公私域数据无缝融合**：支持内部业务数据库与舆情数据无缝集成
6. **轻量化与高扩展性框架**：基于纯Python模块化设计，实现轻量化、一键式部署

## 系统架构

### 整体架构
- **Insight Agent**：私有数据库挖掘 - 私有学术数据库深度分析AI代理
- **Media Agent**：多模态内容分析 - 具备强大多模态能力的AI代理
- **Query Agent**：精准信息搜索 - 具备国内外网页搜索能力的AI代理
- **Report Agent**：智能报告生成 - 内置模板的多轮报告生成AI代理
- **Forum Engine**：论坛引擎 - 实现Agent间的协作与交流

### 分析流程
1. 用户提问：Flask主应用接收查询
2. 并行启动：三个Agent同时开始工作
3. 初步分析：各Agent使用专属工具进行概览搜索
4. 策略制定：基于初步结果制定分块研究策略
5. 循环阶段：论坛协作 + 深度研究（多轮循环）
   - 深度研究：各Agent基于论坛主持人引导进行专项搜索
   - 论坛协作：ForumEngine监控Agent发言并生成主持人总结
   - 交流融合：各Agent根据讨论调整研究方向
6. 结果整合：Report Agent收集所有分析结果和论坛内容
7. 报告生成：动态选择模板和样式，多轮生成最终报告

## 项目结构

```
BettaFish/
├── QueryEngine/                   # 国内外新闻广度搜索Agent
│   ├── agent.py                   # Agent主逻辑
│   ├── llms/                      # LLM接口封装
│   ├── nodes/                     # 处理节点
│   ├── tools/                     # 搜索工具
│   ├── utils/                     # 工具函数
│   └── ...                        # 其他模块
├── MediaEngine/                   # 强大的多模态理解Agent
│   ├── agent.py                   # Agent主逻辑
│   ├── nodes/                     # 处理节点
│   ├── llms/                      # LLM接口
│   ├── tools/                     # 搜索工具
│   ├── utils/                     # 工具函数
│   └── ...                        # 其他模块
├── InsightEngine/                 # 私有数据库挖掘Agent
│   ├── agent.py                   # Agent主逻辑
│   ├── llms/                      # LLM接口封装
│   │   └── base.py                # 统一的 OpenAI 兼容客户端
│   ├── nodes/                     # 处理节点
│   │   ├── base_node.py           # 基础节点类
│   │   ├── formatting_node.py     # 格式化节点
│   │   ├── report_structure_node.py # 报告结构节点
│   │   ├── search_node.py         # 搜索节点
│   │   └── summary_node.py        # 总结节点
│   ├── tools/                     # 数据库查询和分析工具
│   │   ├── keyword_optimizer.py   # Qwen关键词优化中间件
│   │   ├── search.py              # 数据库操作工具集
│   │   └── sentiment_analyzer.py  # 情感分析集成工具
│   ├── state/                     # 状态管理
│   │   ├── __init__.py
│   │   └── state.py               # Agent状态定义
│   ├── prompts/                   # 提示词模板
│   │   ├── __init__.py
│   │   └── prompts.py             # 各类提示词
│   └── utils/                     # 工具函数
│       ├── __init__.py
│       ├── config.py              # 配置管理
│       └── text_processing.py     # 文本处理工具
├── ReportEngine/                  # 多轮报告生成Agent
│   ├── agent.py                   # Agent主逻辑
│   ├── llms/                      # LLM接口
│   ├── nodes/                     # 报告生成节点
│   │   ├── template_selection.py  # 模板选择节点
│   │   └── html_generation.py     # HTML生成节点
│   ├── report_template/           # 报告模板库
│   │   ├── 社会公共热点事件分析.md
│   │   ├── 商业品牌舆情监测.md
│   │   └── ...                    # 更多模板
│   └── flask_interface.py         # Flask API接口
├── ForumEngine/                   # 论坛引擎简易实现
│   ├── monitor.py                 # 日志监控和论坛管理
│   └── llm_host.py                # 论坛主持人LLM模块
├── MindSpider/                    # 微博爬虫系统
│   ├── main.py                    # 爬虫主程序
│   ├── config.py                  # 爬虫配置文件
│   ├── BroadTopicExtraction/      # 话题提取模块
│   │   ├── database_manager.py    # 数据库管理器
│   │   ├── get_today_news.py      # 今日新闻获取
│   │   ├── main.py                # 话题提取主程序
│   │   └── topic_extractor.py     # 话题提取器
│   ├── DeepSentimentCrawling/     # 深度舆情爬取
│   │   ├── keyword_manager.py     # 关键词管理器
│   │   ├── main.py                # 深度爬取主程序
│   │   ├── MediaCrawler/          # 媒体爬虫核心
│   │   └── platform_crawler.py    # 平台爬虫管理
│   └── schema/                    # 数据库结构
│       ├── db_manager.py          # 数据库管理器
│       ├── init_database.py       # 数据库初始化
│       └── mindspider_tables.sql  # 数据库表结构
├── SentimentAnalysisModel/        # 情感分析模型集合
│   ├── WeiboSentiment_Finetuned/  # 微调BERT/GPT-2模型
│   ├── WeiboMultilingualSentiment/# 多语言情感分析（推荐）
│   ├── WeiboSentiment_SmallQwen/  # 小参数Qwen3微调
│   └── WeiboSentiment_MachineLearning/ # 传统机器学习方法
├── SingleEngineApp/               # 单独Agent的Streamlit应用
│   ├── query_engine_streamlit_app.py
│   ├── media_engine_streamlit_app.py
│   └── insight_engine_streamlit_app.py
├── templates/                     # Flask模板
│   └── index.html                 # 主界面前端
├── static/                        # 静态资源
├── logs/                          # 运行日志目录
├── final_reports/                 # 最终生成的HTML报告文件
├── insight_engine_streamlit_reports/    # Insight引擎Streamlit报告目录
├── media_engine_streamlit_reports/      # Media引擎Streamlit报告目录
├── query_engine_streamlit_reports/      # Query引擎Streamlit报告目录
├── utils/                         # 通用工具函数
│   ├── forum_reader.py            # Agent间论坛通信
│   └── retry_helper.py            # 网络请求重试机制工具
├── app.py                         # Flask主应用入口
├── config.py                      # 全局配置文件
├── .env.example                   # 环境变量配置示例
├── docker-compose.yml             # Docker Compose配置文件
├── Dockerfile                     # Docker镜像构建文件
└── requirements.txt               # Python依赖包清单
```

## 环境配置

### 依赖安装
```bash
# 创建conda环境
conda create -n bettafish python=3.11
conda activate bettafish

# 安装基础依赖
pip install -r requirements.txt

# 或使用uv（更快）
uv pip install -r requirements.txt

# 安装Playwright浏览器驱动（用于爬虫功能）
playwright install chromium
```

### 配置说明
1. 复制`.env.example`文件并重命名为`.env`
2. 在`.env`中填入API密钥和数据库配置信息

关键配置项：
- Flask服务器配置（HOST、PORT）
- 数据库配置（PostgreSQL或MySQL）
- LLM API配置（支持任意兼容OpenAI格式的提供商）
- 搜索API配置（Tavily、Bocha等）

## 启动方式

### Docker启动（推荐）
```bash
# 后台启动所有服务
docker compose up -d
```

### 源码启动
```bash
# 启动完整系统
python app.py

# 单独启动某个Agent
streamlit run SingleEngineApp/query_engine_streamlit_app.py --server.port 8503
streamlit run SingleEngineApp/media_engine_streamlit_app.py --server.port 8502
streamlit run SingleEngineApp/insight_engine_streamlit_app.py --server.port 8501
```

### 爬虫系统
```bash
# 进入爬虫目录
cd MindSpider

# 项目初始化
python main.py --setup

# 运行话题提取（获取热点新闻和关键词）
python main.py --broad-topic

# 运行完整爬虫流程
python main.py --complete --date 2024-01-20
```

## Docker部署

### Docker Compose配置
项目提供docker-compose.yml文件，包含两个服务：
- **bettafish**: 主应用服务，暴露端口5000、8501、8502、8503
- **db**: PostgreSQL数据库服务，暴露端口5444（默认）

### 构建和运行
```bash
# 构建并启动服务
docker compose up -d --build

# 查看服务状态
docker compose ps

# 查看日志
docker compose logs -f

# 停止服务
docker compose down
```

### Dockerfile说明
- 基于python:3.11-slim镜像
- 安装了科学计算和爬虫所需的系统依赖
- 使用uv包管理器加速依赖安装
- 预安装chromium浏览器用于Playwright
- 暴露端口5000（Flask）、8501-8503（Streamlit应用）

## 开发约定

### 代码结构
- 所有引擎（QueryEngine、MediaEngine、InsightEngine）遵循相同的结构模式
- 每个引擎包含：agent.py（主逻辑）、llms/（LLM接口）、nodes（处理节点）、tools（工具集）、state（状态管理）、utils（工具函数）
- 使用Pydantic进行配置管理
- 使用loguru进行日志记录

### Agent运行模式
- 每个Agent都包含研究流程：生成报告结构 → 处理段落 → 初始搜索和总结 → 反思循环 → 生成最终报告
- 支持最大反思次数配置
- 每个Agent都有独立的工具集和配置参数

## 扩展开发

### 自定义报告模板
在`ReportEngine/report_template/`目录下创建新的模板文件，Agent会自行选用最合适的模板。

### 接入自定义业务数据库
1. 修改数据库连接配置
2. 创建自定义数据访问工具
3. 集成到InsightEngine中

### 接入不同LLM模型
支持任意兼容OpenAI调用格式的LLM提供商，只需在config.py或.env文件中填写对应的KEY、BASE_URL、MODEL_NAME即可。

## 项目特点

### 实时监控与日志管理
- 通过ForumEngine实现多Agent间的实时监控
- 详细的日志记录和状态跟踪
- 支持Socket.IO实时通信

### 配置管理
- 使用Pydantic Settings进行配置管理
- 支持.env文件和环境变量双重配置
- 运行时动态重载配置

## 免责声明

本项目仅供学习、学术研究和教育目的使用。严禁将本项目用于任何商业用途或盈利性活动。使用爬虫功能时必须遵守目标网站的robots.txt协议和相关法律法规。