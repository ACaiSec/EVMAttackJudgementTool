# ReadableTrace - EVM Trace 解析器

[![Python Version](https://img.shields.io/badge/python-3.13%2B-blue)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

一个高性能的 EVM 区块链交易追踪解析器，能够将复杂的 EVM trace 数据转换为人类可读的格式。支持从 RPC 接口获取交易数据，智能解析合约 ABI，并提供清晰的函数调用层级展示。


## 🛠️ 安装

### 环境要求
- Python 3.13+
- pip 包管理器

### 快速安装

```bash
# 克隆项目
git clone https://github.com/ACaiSec/EVMReadableTrace.git
cd ReadableTrace

# 安装依赖
pip install -r requirements.txt

# 配置环境变量
cp env.example .env
# 编辑 .env 文件，填入你的 Etherscan API 密钥

# 运行程序
python3 main.py --help
```


## 📚 使用方法

### 基本使用

```bash
# 指定链和交易哈希，目前支持 ETH，BSC，POLYGON
python3 main.py -c BSC -t 0x2d9c1a00cf3d2fda268d0d11794ad2956774b156355e16441d6edb9a448e5a99 -s
```

### 命令行参数

| 参数 | 简写 | 描述 | 默认值 |
|------|------|------|--------|
| `--static-call` | `-s` | 包含 STATICCALL 信息 | `false` |
| `--chain` | `-c` | 指定区块链网络 | `BSC` |
| `--tx` | `-t` | 交易哈希值 | 使用本地文件 |


## ⚙️ 配置

### 环境变量配置

创建 `.env` 文件来配置 API 密钥和其他设置：

```bash
# 复制示例配置文件
cp env.example .env

# 编辑 .env 文件，填入你的配置
nano .env
```

### .env 文件配置项

```bash
# API 配置
ETHERSCAN_API_KEY=your_etherscan_api_key_here

# RPC 端点配置
RPC_ETH=https://...
RPC_BSC=https://...
RPC_POLYGON=https://...

# 网络请求配置
REQUEST_DELAY=0.2
MAX_RETRIES=3
REQUEST_TIMEOUT=30

# 缓存配置
ENABLE_CACHE=true
CACHE_DIR=source_code

# 输出配置
OUTPUT_DIR=docs
```

### 必需的配置

- **ETHERSCAN_API_KEY**: 从 [Etherscan.io](https://etherscan.io/apis) 获取的 API 密钥

### 可选配置

所有其他配置项都有默认值，可以根据需要调整：

- **RPC_***: 各链的 RPC 端点地址
- **REQUEST_***: 网络请求相关配置
- **ENABLE_CACHE**: 是否启用源代码缓存
- **CACHE_DIR**: 缓存文件存放目录
- **OUTPUT_DIR**: 输出文件存放目录

## 📊 输出格式

### 标准格式

```
<Level> [<CallType>] [<Value>] <Contract>.<Function>(<ArgType>=<ArgValue>, ...) => (<OutputType>=<OutputValue>, ...)
```

### 输出示例

```
[Sender] 0xad2cb8f48e74065a0b884af9c5a4ecbba101be23
0 [CREATE] 0x1e2d48e640243b04a9fa76eb49080e9ab110b4ac.<empty>() => ()
  1 [CALL] PancakeV3Pool.flash(recipient=0xFd9267eE6594bD8E82e8030c353870fA1773F7f8, amount0=0, amount1=2,813,769,505,544,453,342,436) => ()
    2 [CALL] WBNB.transfer(dst=0xFd9267eE6594bD8E82e8030c353870fA1773F7f8, wad=2,813,769,505,544,453,342,436) => (output0=true)
      3 [STATICCALL] RANTToken.balanceOf(account=PancakePair) => (output0=107,339,710,714,035,019,906,756,623)
```


## 📁 项目结构

```
ReadableTrace/
├── main.py                    # 主程序文件
├── docs/                      # 文档和数据目录
│   ├── trace.json            # 原始 trace 数据
│   └── readableTrace*.txt    # 解析结果文件
├── source_code/              # 合约源代码缓存
│   └── ...
├── pyproject.toml           # 项目配置
└── README.md               # 项目说明文档
```

## 📝 输出文件说明

### 生成的文件

1. **trace.json**: 原始的 RPC trace 数据
2. **readableTrace{timestamp}.txt**: 人类可读的解析结果
3. **source_code/*.txt**: 合约源代码文件




## 🐛 常见问题

### Q: 如何获取 Etherscan API 密钥？
A: 访问 [Etherscan.io](https://etherscan.io/apis) 注册账户并创建 API 密钥。

### Q: 支持哪些区块链网络？
A: 目前支持 Ethereum、BSC、Polygon，可以通过修改 RPC 配置添加更多网络。

### Q: 如何自定义配置？
A: 复制 `env.example` 为 `.env` 文件，然后修改其中的配置项。所有配置都有合理的默认值，只需要设置 `ETHERSCAN_API_KEY` 即可开始使用。

## 📄 许可证

本项目基于 MIT 许可证开源。详情请参阅 [LICENSE](LICENSE) 文件。



