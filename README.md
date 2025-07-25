# AttackJudgmentTool - EVM 攻击交易判断工具

[![Python Version](https://img.shields.io/badge/python-3.13%2B-blue)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

一个专业的 EVM 攻击交易智能判断工具，基于 AI 驱动的分析引擎自动识别区块链攻击交易。通过 Cursor 集成 Workflow5 工作流程，实现交易追踪、合约分析、攻击检测的全自动化流程，为 DeFi 安全分析提供专业支持。


## 🛠️ 安装

### 环境要求
- Python 3.13+
- pip 包管理器

### 快速安装

```bash
# 克隆项目
git clone https://github.com/ACaiSec/EVMReadableTrace.git
cd EVMReadableTrace

# 安装依赖
pip install -r requirements.txt

# 配置环境变量
cp env.example .env
# 编辑 .env 文件，填入你的 Etherscan API 密钥
```


## 📚 使用方法

### 基本使用
运行程序只需要在 cursor 窗口引用 Workflow5.md 文件，并输入链和交易哈希
```bash
@Workflow5.md
BSC 0x362fa1ce7e3f4bdbf2b2ce2569c06082b386223bfd05dec456635cdc5c696832 
```

## ⚙️ 配置

### 环境变量配置

创建 `.env` 文件来配置 API 密钥和其他设置：

```bash
# 复制示例配置文件
# 编辑 .env 文件，填入你的配置
cp env.example .env
```

### .env 文件配置项

```bash
# API 配置
ETHERSCAN_API_KEY=your_etherscan_api_key_here

# RPC 端点配置
RPC_ETH=https://...
RPC_BSC=https://...
RPC_POLYGON=https://...
```


## 📁 项目结构

```
AttackJudgmentTool/
├── main.py                    # 主程序入口
├── requirements/              # 工作流程和规则定义
│   ├── Workflow5.md          # AI分析工作流程
│   └── judgeRules.md         # 攻击判断规则引擎
├── trace/                     # 交易分析结果目录
│   └── <txHash>/             # 按交易哈希组织
│       ├── trace.json        # 原始RPC trace数据
│       ├── readableTrace.txt # 人类可读trace解析
│       └── analysisResult.txt # AI攻击判断结果
├── source_code/              # 智能合约源码分析
│   └── <txHash>/             # 按交易哈希组织
│       ├── TokenA.txt        # 相关合约源代码
│       ├── TokenB.txt        # 自动获取并缓存
│       └── ...
├── .env                      # 环境配置文件
├── env.example              # 配置模板
├── pyproject.toml           # 项目依赖配置
└── README.md               # 项目文档
```

## 📝 分析输出说明

### 自动生成的分析文件

每次分析会在 `./trace/<txHash>/` 目录下生成：

1. **trace.json** - 原始 RPC trace 数据 (30KB)
   - 包含完整的EVM执行追踪信息
   - JSON格式的原始调用数据

2. **readableTrace.txt** - 人类可读的trace解析 (3-4KB)  
   - 按层级展示的函数调用关系
   - 智能解码的参数和返回值
   - 清晰的合约交互流程

3. **analysisResult.txt** - AI攻击判断结果 (1-2KB)
   - 基于Workflow5的智能分析结论
   - 结构化的攻击/非攻击判定报告
   - 详细的技术分析和风险评估

### 自动获取的合约源码

每次分析会在 `./source_code/<txHash>/` 目录下缓存：

- **合约源代码文件** (10-40KB each)
  - 如：`MIL.txt`、`WETH9.txt`、`UniswapV2Pair.txt`
  - 自动从Etherscan获取并验证
  - 支持ABI解析和函数签名识别
  - 用于深度合约逻辑分析




## 🐛 常见问题

### Q: 如何获取 Etherscan API 密钥？
A: 访问 [Etherscan.io](https://etherscan.io/apis) 注册账户并创建 API 密钥。

### Q: 支持哪些区块链网络？
A: 目前支持 Ethereum、BSC、Polygon，可以通过修改 RPC 配置添加更多网络。

### Q: 如何自定义配置？
A: 复制 `env.example` 为 `.env` 文件，然后修改其中的配置项。所有配置都有合理的默认值，只需要设置 `ETHERSCAN_API_KEY` 即可开始使用。

## 📄 许可证

本项目基于 MIT 许可证开源。详情请参阅 [LICENSE](LICENSE) 文件。



