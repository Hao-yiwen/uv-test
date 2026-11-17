# uv-test

[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![uv](https://img.shields.io/badge/uv-lockfile-DE5FE9)](https://docs.astral.sh/uv/)
[![version](https://img.shields.io/badge/version-0.1.0-555555)](pyproject.toml)

用 [uv](https://docs.astral.sh/uv/) 管理的最小 Python 示例。运行入口后，标准输出打印一行：

```text
Hello from uv-test!
```

仓库用来确认「Python 3.12 + uv 锁定依赖」这条链路可以装起来、跑起来。当前没有业务功能、测试、命令行入口或界面。`pyproject.toml` 里的 `description` 仍是脚手架占位文案 `Add your description here`。

## 仓库里有什么

| 内容 | 现状 |
| --- | --- |
| 入口脚本 | `main.py` 定义 `main()`，打印 `Hello from uv-test!`；以脚本方式执行时调用它 |
| 直接依赖 | `requests>=2.32.5`，`uv.lock` 锁定为 **2.32.5** |
| 入口对依赖的使用 | 入口脚本只打印问候，没有导入或调用 `requests` |
| 测试、许可证、截图 | 仓库中没有 |

锁定后随 `requests` 一起安装的传递依赖：

| 包 | 锁定版本 |
| --- | --- |
| certifi | 2025.8.3 |
| charset-normalizer | 3.4.3 |
| idna | 3.10 |
| urllib3 | 2.5.0 |

## 技术栈

- **语言：** Python `>=3.12`（`.python-version` 指定 `3.12`）
- **项目元数据：** `pyproject.toml`，包名 `uv-test`，版本 `0.1.0`
- **依赖管理：** [uv](https://docs.astral.sh/uv/)，锁文件 `uv.lock`（uv lock 格式 version 1，revision 3）
- **构建后端：** 未配置。仓库没有 `[build-system]`，也没有 `[project.scripts]`，因此没有可安装的控制台命令

## 目录结构

```text
.
├── main.py           # 入口：打印一行问候
├── pyproject.toml    # 项目名、Python 版本要求、依赖声明
├── uv.lock           # 已解析并锁定的依赖
├── .python-version   # 3.12
├── .gitignore        # 忽略 __pycache__、构建产物和 .venv
└── README.md
```

`uv sync` 会在本地创建 `.venv`（已被 `.gitignore` 忽略）。

## 环境要求

- Python 3.12 或更高版本
- [uv](https://docs.astral.sh/uv/getting-started/installation/)（按锁定文件安装依赖时需要）

本仓库在以下环境验证过安装与运行：Python **3.12.3**、uv **0.13.8**（Linux x86_64）。

## 安装与运行

在仓库根目录执行：

```bash
uv sync
uv run python main.py
```

`uv sync` 按 `uv.lock` 创建虚拟环境并安装依赖。上述环境中安装结果为：

```text
certifi==2025.8.3
charset-normalizer==3.4.3
idna==3.10
requests==2.32.5
urllib3==2.5.0
```

`uv run python main.py` 的输出：

```text
Hello from uv-test!
```

查看锁定后的依赖树：

```bash
uv tree
```

系统已有 Python 3.12+ 时，也可以直接运行入口（已在 Python 3.12.3 上验证，输出同上）：

```bash
python3 main.py
```

这条路径使用当前解释器，不会读取 `uv.lock`，也不会安装 `requests`。需要锁定依赖时使用上面的 `uv sync`。

## 备注

- 依赖来自 PyPI（`https://pypi.org/simple`），版本以 `uv.lock` 为准。
- 更新依赖时在本机执行 `uv lock` / `uv sync`，并提交更新后的 `uv.lock`。
- 仓库没有截图、文档站或额外示例。
