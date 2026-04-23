# 中文

[English](README_EN.md) | [中文](README_ZH.md) | [한국어](README.md)

一款功能强大的 GUI 应用程序，用于翻译 Paradox (P社) 游戏模组。它使用 OpenAI 兼容 API 高效地翻译 YAML 本地化文件。

![UI 设置](asset/image%201%20-%20ui%20setting.png)

## 主要功能

### 🌍 多语言支持
- 实时 UI 语言切换
- 自动检测系统语言
- 支持韩语、英语、中文

### 🔧 高级翻译功能
- **OpenAI 兼容 API 集成**：高质量的 AI 翻译
- **批量处理**：将大文件分割成块进行处理
- **恢复系统**：基于检查点的中断翻译恢复
- **质量保证**：YAML 语法检查和翻译质量验证

### 🎮 游戏专属优化
- 针对每款 Paradox 游戏的特定翻译提示
- 支持游戏专属术语表
- 支持《欧陆风云IV》、《十字军之王III》、《钢铁雄心IV》等

### 📊 分析与监控
- **实时预览**：实时查看翻译进度
- **统计仪表板**：翻译分析和进度跟踪
- **一致性检查器**：验证翻译术语的一致性

## 屏幕截图

### API 设置
![API 设置](asset/image%202%20-%20API%20setting.png)

- 目前可以选择 5 种 API
- 2.5 Flash：默认
- 2.0 Flash：用于避免审查的选择
- 1.5 系列：当成本较高时
- 2.5 Pro：当您想要高质量时（非常昂贵且限制严格！！）

### 文件夹选择
![文件夹选择](asset/image%203%20-%20Floder%20Selection.png)

### 语言设置
![语言设置](asset/image%204%20-%20Language%20Setting.png)

- 目前支持英语、韩语、中文（简体）、法语、德语、西班牙语、葡萄牙语、日语、俄语、土耳其语

### 翻译设置
![翻译设置](asset/image%205%20-%20Translation%20Setting.png)

- **Batch Size (批处理大小)**: 一次翻译多少行（line）。
- **Concurrent Files (并发文件数)**: 一次同时翻译多少个文件。
- **Max Output Tokens (最大输出令牌数)**: 控制最大令牌数（2.5 设置为 65536，其余设置为 8192）。
- **Delay Between Batches (批次间延迟)**: 设置 API 响应之间的时间延迟。
- **File Split Threshold (文件分割阈值)**: 将长文件分割翻译的功能（例如，一个 30000 行的文件设置为 1000，将被分成 30 个部分进行翻译）。
- **Temperature (温度)**: 您希望回答有多大的创造性（越接近 0 越确定，越接近 2.0 越富有想象力）。
- **Max Retries (最大重试次数)**: 翻译过程中批处理出错时，将重试多少次。

- **Keep Original l_english identifier (保留原始 l_english 标识符)**: 如果您的语言不被游戏支持，请勾选此项。
- **Prioritize UI setting... (优先使用UI设置...)**: 如果您要翻译的文件的源语言也不被游戏支持，请勾选此项。（例如：在欧陆风云中翻译中文 -> 韩文）。
- **Skip Already Translated Lines (跳过已翻译行)**: 在翻译部分已翻译的模组时使用。

### 提示编辑
![提示编辑](asset/image%206%20-%20Edit%20Prompt.png)

### 术语表管理
![术语表管理](asset/image%207%20-%20glossary%20management.png)

### 控制面板
![开始/停止按钮](asset/image%208%20-%20start%20and%20stop%20button.png)

### 日志面板
![日志面板](asset/image%209%20-%20File%20Comparison%20Review%20Tool.png)

### 实时预览面板
![实时预览面板](asset/image%2010%20-%20File%20Comparison%20Review%20Tool%20Window.png)

## 安装与运行

### 系统要求
```bash
pip install customtkinter requests
```

### 运行方法
```bash
python "pdx translation tool/run_translator.py"
```

-或者，从 Release 部分下载并运行 .EXE 文件。

## 使用方法

### 1. API 设置
- 输入 Base URL（例如 `https://api.openai.com/v1`）。
- 输入 API 密钥。
- 输入要使用的模型名称（自由输入）。

### 2. 文件夹设置
- **输入文件夹**：选择包含待翻译 YAML 文件的文件夹。
- **输出文件夹**：选择用于保存翻译后文件的文件夹。

### 3. 语言设置
- **源语言**：原始文件的语言。
- **目标语言**：要翻译成的语言。

### 4. 高级设置
- **批处理大小**：一次处理的文本量。
- **并发工作线程数**：并行处理的线程数。
- **重试次数**：API 出错时的重试次数。

### 5. 开始翻译
- 点击“开始翻译”按钮。
- 实时监控进度。
- 完成后检查结果。

## 软件架构

### 核心组件

#### TranslatorEngine (`translator_app/core/translator_engine.py`)
- 负责 API 调用和文件处理。
- 实现批量翻译和恢复机制。

#### TranslationGUI (`translator_app/gui/main_window.py`)
- 主应用程序窗口。
- 协调所有 UI 面板并管理应用程序状态。

#### SettingsManager (`translator_app/core/settings_manager.py`)
- 处理设置的持久化和加载。

### GUI 面板结构

#### 设置面板 (`translator_app/gui/panels/`)
- `api_model_panel.py`: Base URL、API 密钥和模型输入。
- `folder_panel.py`: 输入/输出文件夹选择。
- `translation_lang_panel.py`: 源/目标语言设置。
- `detailed_settings_panel.py`: 高级翻译参数。
- `prompt_glossary_panel.py`: 自定义提示和术语表管理。
- `control_panel.py`: 开始/停止翻译控制。
- `log_panel.py`: 记录翻译进度。
- `live_preview_panel.py`: 实时翻译预览。

#### 工具窗口 (`translator_app/gui/windows/`)
- `translation_dashboard.py`: 翻译统计与分析。
- `term_consistency_checker.py`: 翻译一致性验证。

## 翻译工作流程

1.  **文件发现**：在输入文件夹中扫描 YAML 文件（.yml/.yaml）。
2.  **批量处理**：根据可配置的阈值分割大文件。
3.  **API 翻译**：使用支持 `/v1/chat/completions` 的 OpenAI 兼容 API，并结合自定义提示词和术语表。
4.  **恢复系统**：基于检查点的中断翻译恢复。
5.  **质量保证**：内置 YAML 语法验证和翻译质量检查。

## 主要特点

### 🔄 多线程处理
- 通过可配置的工作线程限制并发处理文件。

### 🎯 游戏专属提示
- 为各种 Paradox 游戏优化的提示。

### 📚 术语表支持
- 使用外部术语表文件以确保术语一致。

### 👀 实时预览
- 在处理过程中实时预览翻译。

### 📈 统计仪表板
- 全面的翻译分析。

### 💾 备份系统
- 翻译前可选择性地备份文件。

## 配置文件

- **主设置**: `translation_gui_config.json`
- **检查点目录**: `checkpoints/` (用于恢复)
- 应用程序退出时自动保存设置。

## 开发信息

### 技术栈
- **GUI**: CustomTkinter (用于现代 UI 风格)
- **API**: OpenAI 兼容 Chat Completions API
- **语言**: Python 3.7+
- **编码**: UTF-8-BOM (为确保兼容性)

### 语言文件
- 位置: `translator_app/utils/localization.py`
- 支持自动系统语言检测。

### 贡献
1.  Fork 此仓库。
2.  创建您的功能分支 (`git checkout -b feature/AmazingFeature`)。
3.  提交您的更改 (`git commit -m 'Add some AmazingFeature'`)。
4.  推送到分支 (`git push origin feature/AmazingFeature`)。
5.  打开一个 Pull Request。

## 许可证

该项目根据 MIT 许可证分发。有关更多信息，请参阅 `LICENSE` 文件。

## 支持

如果您遇到任何问题或有功能请求，请通过 GitHub Issues 告诉我们。

---

**祝您翻译愉快！🎮🌍**
