# BettaFish项目软件分析树形文档

## 项目概述
BettaFish（微舆）是一个多智能体舆情分析系统，通过多个专门的AI代理协同工作，实现对社交媒体数据的深度分析和舆情报告生成。

## 项目结构树形图

```
BettaFish/
├── app.py                          # Flask主应用入口，统一管理系统各组件
├── config.py                       # 全局配置管理，使用Pydantic Settings
├── requirements.txt                # Python依赖包清单
├── docker-compose.yml             # Docker容器编排配置
├── Dockerfile                     # Docker镜像构建文件
├── .env.example                   # 环境变量配置示例文件
├── IFLOW.md                       # 项目指南文档
├── README.md                      # 项目说明文档
├── README-EN.md                   # 英文项目说明文档
├── LICENSE                        # 开源许可证
├── CODE_OF_CONDUCT.md             # 行为准则
├── CONTRIBUTING.md                # 贡献指南
├── CONTRIBUTING-EN.md             # 英文贡献指南
├── .gitignore                     # Git忽略文件配置
├── .dockerignore                  # Docker忽略文件配置
├── .github/                       # GitHub配置文件
│   └── workflows/                 # CI/CD工作流配置
│       └── docker_ci.yml          # Docker镜像构建CI流程
├── doc/                           # 项目文档目录
│   └── SOFTWARE_ANALYSIS.md       # 软件分析文档（当前文件）
├── logs/                          # 运行日志目录
├── static/                        # 静态资源文件
│   └── image/                     # 图片资源
├── templates/                     # Flask模板文件
│   └── index.html                 # 主界面模板
├── final_reports/                 # 最终生成的HTML报告文件目录
├── insight_engine_streamlit_reports/  # Insight引擎Streamlit报告目录
├── media_engine_streamlit_reports/    # Media引擎Streamlit报告目录
├── query_engine_streamlit_reports/    # Query引擎Streamlit报告目录
├── utils/                         # 通用工具函数目录
│   ├── forum_reader.py            # Agent间论坛通信工具
│   ├── retry_helper.py            # 网络请求重试机制工具
│   └── github_issues.py           # GitHub问题处理工具
├── tests/                         # 测试文件目录
│   ├── run_tests.py               # 测试运行入口
│   ├── test_monitor.py            # ForumEngine监控器测试
│   ├── forum_log_test_data.py     # 论坛日志测试数据
│   ├── __init__.py                # Python包初始化文件
│   └── README.md                  # 测试说明文档
├── ForumEngine/                   # 论坛引擎目录（Agent间协作机制）
│   ├── monitor.py                 # 日志监控和论坛管理
│   ├── llm_host.py                # 论坛主持人LLM模块
│   ├── __init__.py                # Python包初始化文件
│   └── __pycache__/               # Python缓存目录
├── InsightEngine/                 # 私有数据库挖掘Agent目录
│   ├── agent.py                   # Agent主逻辑
│   ├── __init__.py                # Python包初始化文件
│   ├── llms/                      # LLM接口封装目录
│   │   ├── base.py                # 统一的OpenAI兼容客户端
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── nodes/                     # 处理节点目录
│   │   ├── base_node.py           # 基础节点类
│   │   ├── formatting_node.py     # 报告格式化节点
│   │   ├── report_structure_node.py # 报告结构生成节点
│   │   ├── search_node.py         # 搜索节点
│   │   ├── summary_node.py        # 总结节点
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── tools/                     # 数据库查询和分析工具目录
│   │   ├── keyword_optimizer.py   # Qwen关键词优化中间件
│   │   ├── search.py              # 数据库操作工具集
│   │   ├── sentiment_analyzer.py  # 情感分析集成工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── state/                     # 状态管理目录
│   │   ├── state.py               # Agent状态定义
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── prompts/                   # 提示词模板目录
│   │   ├── prompts.py             # 各类提示词
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── utils/                     # 工具函数目录
│   │   ├── text_processing.py     # 文本处理工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   └── __pycache__/               # Python缓存目录
├── MediaEngine/                   # 多模态内容分析Agent目录
│   ├── agent.py                   # Agent主逻辑
│   ├── __init__.py                # Python包初始化文件
│   ├── llms/                      # LLM接口封装目录
│   │   ├── base.py                # 统一的OpenAI兼容客户端
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── nodes/                     # 处理节点目录
│   │   ├── base_node.py           # 基础节点类
│   │   ├── formatting_node.py     # 报告格式化节点
│   │   ├── report_structure_node.py # 报告结构生成节点
│   │   ├── search_node.py         # 搜索节点
│   │   ├── summary_node.py        # 总结节点
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── tools/                     # 搜索工具目录
│   │   ├── search.py              # Bocha多模态搜索工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── state/                     # 状态管理目录
│   │   ├── state.py               # Agent状态定义
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── prompts/                   # 提示词模板目录
│   │   ├── prompts.py             # 各类提示词
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── utils/                     # 工具函数目录
│   │   ├── text_processing.py     # 文本处理工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   └── __pycache__/               # Python缓存目录
├── QueryEngine/                   # 精准信息搜索Agent目录
│   ├── agent.py                   # Agent主逻辑
│   ├── __init__.py                # Python包初始化文件
│   ├── llms/                      # LLM接口封装目录
│   │   ├── base.py                # 统一的OpenAI兼容客户端
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── nodes/                     # 处理节点目录
│   │   ├── base_node.py           # 基础节点类
│   │   ├── formatting_node.py     # 报告格式化节点
│   │   ├── report_structure_node.py # 报告结构生成节点
│   │   ├── search_node.py         # 搜索节点
│   │   ├── summary_node.py        # 总结节点
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── tools/                     # 搜索工具目录
│   │   ├── search.py              # Tavily网络搜索工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── state/                     # 状态管理目录
│   │   ├── state.py               # Agent状态定义
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── prompts/                   # 提示词模板目录
│   │   ├── prompts.py             # 各类提示词
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── utils/                     # 工具函数目录
│   │   ├── text_processing.py     # 文本处理工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   └── __pycache__/               # Python缓存目录
├── ReportEngine/                  # 智能报告生成Agent目录
│   ├── agent.py                   # Agent主逻辑
│   ├── flask_interface.py         # Flask API接口
│   ├── __init__.py                # Python包初始化文件
│   ├── llms/                      # LLM接口封装目录
│   │   ├── base.py                # 统一的OpenAI兼容客户端
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── nodes/                     # 报告生成节点目录
│   │   ├── base_node.py           # 基础节点类
│   │   ├── template_selection_node.py # 模板选择节点
│   │   ├── html_generation_node.py # HTML生成节点
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── report_template/           # 报告模板库目录
│   │   ├── 社会公共热点事件分析.md  # 社会热点事件分析模板
│   │   ├── 商业品牌舆情监测.md      # 商业品牌舆情监测模板
│   │   └── ...                    # 其他报告模板
│   ├── state/                     # 状态管理目录
│   │   ├── state.py               # Agent状态定义
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── prompts/                   # 提示词模板目录
│   │   ├── prompts.py             # 各类提示词
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── utils/                     # 工具函数目录
│   │   ├── text_processing.py     # 文本处理工具
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   └── __pycache__/               # Python缓存目录
├── MindSpider/                    # 微博爬虫系统目录
│   ├── main.py                    # 爬虫主程序
│   ├── config.py.example          # 爬虫配置示例文件
│   ├── requirements.txt           # 爬虫依赖包清单
│   ├── README.md                  # 爬虫使用说明
│   ├── LICENSE                    # 开源许可证
│   ├── __init__.py                # Python包初始化文件
│   ├── __pycache__/               # Python缓存目录
│   ├── img/                       # 图片资源目录
│   │   └── example.png            # 示例图片
│   ├── schema/                    # 数据库结构目录
│   │   ├── db_manager.py          # 数据库管理器
│   │   ├── init_database.py       # 数据库初始化
│   │   ├── mindspider_tables.sql  # 数据库表结构定义
│   │   ├── models_sa.py           # SQLAlchemy数据模型
│   │   ├── models_bigdata.py      # 大数据处理模型
│   │   ├── __init__.py            # Python包初始化文件
│   │   └── __pycache__/           # Python缓存目录
│   ├── BroadTopicExtraction/      # 话题提取模块目录
│   │   ├── database_manager.py    # 数据库管理器
│   │   ├── get_today_news.py      # 今日新闻获取
│   │   ├── main.py                # 话题提取主程序
│   │   ├── topic_extractor.py     # 话题提取器
│   │   └── __pycache__/           # Python缓存目录
│   └── DeepSentimentCrawling/     # 深度舆情爬取目录
│       ├── keyword_manager.py     # 关键词管理器
│       ├── main.py                # 深度爬取主程序
│       ├── platform_crawler.py    # 平台爬虫管理
│       ├── __init__.py            # Python包初始化文件
│       ├── __pycache__/           # Python缓存目录
│       └── MediaCrawler/          # 媒体爬虫核心目录
├── SentimentAnalysisModel/        # 情感分析模型集合目录
│   ├── WeiboSentiment_Finetuned/  # 微调BERT/GPT-2模型
│   ├── WeiboMultilingualSentiment/# 多语言情感分析（推荐）
│   ├── WeiboSentiment_SmallQwen/  # 小参数Qwen3微调
│   └── WeiboSentiment_MachineLearning/ # 传统机器学习方法
├── SingleEngineApp/               # 单独Agent的Streamlit应用目录
│   ├── insight_engine_streamlit_app.py  # Insight引擎独立应用
│   ├── media_engine_streamlit_app.py    # Media引擎独立应用
│   └── query_engine_streamlit_app.py    # Query引擎独立应用
└── __pycache__/                   # 项目根目录Python缓存
```

## 各模块详细说明

### 1. 核心应用入口 (app.py)
- **功能**: Flask主应用，负责统一管理三个Streamlit应用，提供API接口，处理系统状态管理
- **主要职责**: 
  - 启动和监控各个Agent组件
  - 提供Web界面和API接口
  - 管理系统配置和日志
  - 协调各组件间的通信

### 2. 配置管理 (config.py)
- **功能**: 全局配置管理，使用Pydantic Settings实现配置的自动加载和验证
- **主要职责**:
  - 管理数据库连接配置
  - 管理各Agent的LLM API配置
  - 管理搜索工具API配置
  - 支持.env文件和环境变量配置

### 3. 论坛引擎 (ForumEngine/)
- **功能**: 实现Agent间的协作与交流机制
- **主要文件**:
  - `monitor.py`: 日志监控和论坛管理，监控各Agent的总结输出并组织论坛讨论
  - `llm_host.py`: 论坛主持人LLM模块，生成主持人发言引导讨论

### 4. Insight引擎 (InsightEngine/)
- **功能**: 私有数据库挖掘Agent，负责从本地数据库中挖掘舆情数据
- **主要组件**:
  - `agent.py`: Agent主逻辑，实现深度研究流程
  - `llms/`: LLM接口封装，提供统一的OpenAI兼容客户端
  - `nodes/`: 处理节点，包括报告结构生成、搜索、总结、格式化等节点
  - `tools/`: 数据库查询和分析工具，包含关键词优化和情感分析工具
  - `state/`: 状态管理，定义Agent的运行状态
  - `prompts/`: 提示词模板，提供各类LLM提示词
  - `utils/`: 工具函数，包括文本处理等

### 5. Media引擎 (MediaEngine/)
- **功能**: 多模态内容分析Agent，具备强大多模态能力
- **主要组件**:
  - `agent.py`: Agent主逻辑，实现深度研究流程
  - `llms/`: LLM接口封装
  - `nodes/`: 处理节点
  - `tools/`: 搜索工具，主要集成Bocha多模态搜索
  - `state/`: 状态管理
  - `prompts/`: 提示词模板
  - `utils/`: 工具函数

### 6. Query引擎 (QueryEngine/)
- **功能**: 精准信息搜索Agent，具备国内外网页搜索能力
- **主要组件**:
  - `agent.py`: Agent主逻辑，实现深度研究流程
  - `llms/`: LLM接口封装
  - `nodes/`: 处理节点
  - `tools/`: 搜索工具，主要集成Tavily网络搜索
  - `state/`: 状态管理
  - `prompts/`: 提示词模板
  - `utils/`: 工具函数

### 7. 报告引擎 (ReportEngine/)
- **功能**: 智能报告生成Agent，内置模板的多轮报告生成
- **主要组件**:
  - `agent.py`: Agent主逻辑
  - `flask_interface.py`: Flask API接口
  - `llms/`: LLM接口封装
  - `nodes/`: 报告生成节点，包括模板选择和HTML生成
  - `report_template/`: 报告模板库
  - `state/`: 状态管理
  - `prompts/`: 提示词模板
  - `utils/`: 工具函数

### 8. 爬虫系统 (MindSpider/)
- **功能**: 微博爬虫系统，负责从社交媒体平台抓取数据
- **主要组件**:
  - `main.py`: 爬虫主程序
  - `schema/`: 数据库结构定义和管理
  - `BroadTopicExtraction/`: 话题提取模块
  - `DeepSentimentCrawling/`: 深度舆情爬取模块
  - `MediaCrawler/`: 媒体爬虫核心

### 9. 情感分析模型 (SentimentAnalysisModel/)
- **功能**: 情感分析模型集合，提供多种情感分析方法
- **主要组件**:
  - `WeiboSentiment_Finetuned/`: 微调BERT/GPT-2模型
  - `WeiboMultilingualSentiment/`: 多语言情感分析（推荐）
  - `WeiboSentiment_SmallQwen/`: 小参数Qwen3微调
  - `WeiboSentiment_MachineLearning/`: 传统机器学习方法

### 10. 独立应用 (SingleEngineApp/)
- **功能**: 提供各Agent的独立Streamlit应用，便于单独测试和使用
- **主要文件**:
  - `insight_engine_streamlit_app.py`: Insight引擎独立应用
  - `media_engine_streamlit_app.py`: Media引擎独立应用
  - `query_engine_streamlit_app.py`: Query引擎独立应用

### 11. 工具和实用程序 (utils/)
- **功能**: 通用工具函数
- **主要文件**:
  - `forum_reader.py`: Agent间论坛通信工具
  - `retry_helper.py`: 网络请求重试机制工具
  - `github_issues.py`: GitHub问题处理工具

### 12. 测试 (tests/)
- **功能**: 项目测试文件
- **主要文件**:
  - `run_tests.py`: 测试运行入口
  - `test_monitor.py`: ForumEngine监控器测试
  - `forum_log_test_data.py`: 论坛日志测试数据

### 13. 文档和资源
- **static/**: 静态资源文件，如图片等
- **templates/**: Flask模板文件
- **final_reports/**: 最终生成的HTML报告文件
- **各引擎报告目录**: 各引擎独立运行时生成的报告
- **logs/**: 运行日志目录