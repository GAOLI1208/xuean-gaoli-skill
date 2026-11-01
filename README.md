# xuean-gaoli 完整技能包

这是初高中物理教学学案技能 `xuean-gaoli` 的完整发布包，用于把真实题目整理成可追溯的 A4 学案：按条件找候选、从 HTML/PDF/扫描页提取、逐空映射来源答案、审核后生成题目版或来源答案版 PDF。

## 下载与解压

仓库根目录的完整包是：

```text
xuean-gaoli-skill.zip
```

在 GitHub 页面下载该 zip 后解压：

```sh
mkdir -p xuean-gaoli
unzip xuean-gaoli-skill.zip -d xuean-gaoli
cd xuean-gaoli
```

zip 共 **44 个文件**（另有目录项，含 `LICENSE`），保留包内相对目录；`install.sh`、`uninstall.sh`、`bin/xuean` 在 zip 中带可执行位。若下载/解压工具丢失权限，先恢复：

```sh
chmod +x install.sh uninstall.sh bin/xuean
```

## 安装

### 安装到项目（推荐，不做用户级安装）

```sh
cd xuean-gaoli
chmod +x install.sh uninstall.sh bin/xuean
./install.sh /path/to/your-project
```

安装后技能位于：

```text
/path/to/your-project/.dsh/skills/xuean-gaoli/
```

首次安装需要 PyPI 访问，会在该目录创建隔离 `.venv` 并安装 `requirements.lock.txt` 的锁定依赖。

### 只在本包目录运行

```sh
cd xuean-gaoli
chmod +x install.sh uninstall.sh bin/xuean
PYTHON=/path/to/python3.12 ./install.sh ./
./bin/xuean doctor
```

也可以不依赖可执行位，直接：

```sh
sh install.sh /path/to/your-project
```

### 卸载

```sh
cd xuean-gaoli
chmod +x uninstall.sh
./uninstall.sh /path/to/your-project
```

只删除带 `.xuean-installed` 标记的项目技能目录，不删除用户级目录或源码。

## DSH 集成

安装后从项目**工作区根**启动 DSH，新会话检查：

```text
.dsh/skills/xuean-gaoli/SKILL.md
```

DSH 只负责技能发现与调用说明；搜索工具由 DSH 环境提供，PDF/Typst 由本包隔离 `.venv` 提供。不要用用户级安装绕过发现路径。

## 现有验证

本包随附的 `VALIDATION.md` 记录了实际执行结果：

- 隔离临时项目安装：`exit 0`，15 个锁定依赖安装成功；技能路径与 `SKILL.md` 存在。
- `bin/xuean --help`：`exit 0`。
- `bin/xuean doctor`：在可用 Python 3.12 下 `exit 0`，Typst 样页、Songti 字体、依赖检查通过。
- 自造最小示例：`validate` 初始按预期阻断；完成 source/text 审核后 `promote`、`validate`、`build`、`audit`、`visual`、`deliver` 均 `exit 0`；1 页，正文 11.5pt，字体嵌入。
- 项目内和本包目录模式的安装/卸载均验证过。

**版本范围**：安装器门槛为 Python `>=3.10, <3.14`，但当前**仅实际验证 Python 3.12**。3.10/3.11/3.13 是预期兼容范围，未逐版验证；不声称“支持 3.10–3.13”。

## 依赖与平台

- Python 3.10–3.13 为版本门槛/预期范围；只有 3.12 实测。安装器不打包解释器或第三方二进制，用系统/官方 Python 建隔离 `.venv`。
- 依赖见 `requirements.lock.txt`：BeautifulSoup、pdfplumber/pdfminer、pypdf、pypdfium2、Pillow、Typst Python 包、SymPy 等。
- 中文字体：macOS 已用系统 `Songti SC` 验证；字体不随包，其它系统需自行提供兼容字体，当前未验证。
- 扫描 OCR：macOS `xcrun`/Swift + Xcode Command Line Tools；Linux/Windows 未验证。
- 安装脚本是 POSIX shell；Windows 需 WSL/Git Bash，当前未验证。

## 真实局限

- 这是**实验候选**，主要验证初高中物理；不是任意网站、任意版式的全自动系统。
- 提取、OCR、图文关系、来源核验可能需要模型辅助；人工审核和逐页目视仍必需。
- 搜索预算流程可能被直接工具调用绕过；CLI 只约束走 CLI 的调用。年度/地区/材料性质必须回源核实。
- 不承诺成功率或“全自动正确”；机器 audit 通过不等于内容/排版合格。
- 本包不包含真实试卷、个人数据、账号配置、`runs/`、缓存或第三方运行时；`examples/minimal/` 为手写自造示例，不是真实题。
- 本仓库和 zip 内的代码、文档、自造示例采用 **MIT License**，版权为 **Copyright (c) 2026 GAOLI1208**；完整文本见根目录 `LICENSE`（zip 内也有同名文件）。
- 第三方依赖、字体、Typst 和真实材料各自遵循上游/来源权利与许可；详见包内 `NOTICE.md`。MIT 许可不改变这些第三方权利。

## 包内文件

- `SKILL.md`：DSH 技能说明与流程
- `README.md`（包内）：较完整的技能说明
- `VALIDATION.md`：验证命令、结果、未验证项
- `references/`：搜索、提取、答案映射、交付、限制
- `xuean.py`、`xueanlib/`：CLI 与核心代码
- `LICENSE`：MIT License（Copyright 2026 GAOLI1208）
- `templates/`：问题 schema 与 Typst 版式
- `scripts/vision_ocr.swift`：macOS OCR 源文件
- `examples/minimal/`：自造 smoke test
- `install.sh`、`uninstall.sh`、`bin/xuean`：安装/运行入口

本 README 是仓库根说明，zip 内另有技能包 README。
