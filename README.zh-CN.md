# llama.cpp 模型管理器（LlamaManager）

[English](README.md) | [简体中文](README.zh-CN.md)

一个 **Windows 单文件桌面小工具**，用于管理本地 GGUF 大模型，并通过 [llama.cpp](https://github.com/ggml-org/llama.cpp) 的 `llama-server` **一键启动**，无需手敲命令行。

> 当前版本：**v1.28.0**（下载见本页右侧 **Releases**）

---

## 它能做什么

- **管理本地 GGUF 模型库**：添加 / 更换 / 复制 / 删除 / 打开文件夹；模型列表可直接拖动、按钮或右键调整顺序（自动保存）。
- **每个模型可建多套「启动方案」**：端口、上下文长度、GPU 层数、采样、推理、缓存等几十个参数任意组合，一键切换；方案名即 llama-server 别名 `-a`。
- **可视化配置，默认即官方默认**：所有参数统一下拉交互，默认值直接标注，等于默认值的不写入命令；自定义项高亮变色；参数行括号里实时显示「实际会写入命令的参数值」。
- **内置「官方参数参考」**：参数说明对照 llama.cpp 官方文档原文（中英双语界面自动切换）。
- **一键启动 + 实时日志**：启动命令逐行预览、复制；支持多模型/多方案**同时并发启动**多个服务，每个服务有独立日志面板。
- **OpenAI 兼容 API 一键可用**：复制 API 地址 / 别名 / API Key、浏览器打开接口、内置聊天测试。
- 界面浅色 / 深色双主题；**首次启动语言自动跟随系统**，可在设置里固定为简体中文或 English。

## 运行环境

- Windows 10 / 11（x64）
- 需要自行准备 **llama-server**（llama.cpp 的服务器程序，`llama-server.exe`）：
  - 官方下载：[ggml-org/llama.cpp Releases](https://github.com/ggml-org/llama.cpp/releases)，选择带 `-bin-win-` 的压缩包（N 卡用 `-cuda-`，A/I 卡用 `-vulkan-`）
  - 或在软件「设置 → 自动探测」中自动查找
- 需要本地已有 `.gguf` 格式模型文件

## 快速上手

1. 下载本页 Release 中的 `LlamaManager-1.28.0-win64.exe`（可选：用同目录 `.sha256` 文件校验完整性）。
2. 双击运行（单文件，无需安装）。
3. 首次打开会自动跟随系统语言；在「设置」里填好 `llama-server.exe` 路径。
4. 点「添加模型」选择你的 `.gguf` 文件 → 自动读取量化 / 架构 / 大小。
5. 在右侧参数页按需配置方案 → 点顶部橙色「启动」按钮 → 等状态变为「运行中」。
6. 复制 API 地址（如 `http://127.0.0.1:8080`）即可接入任何 OpenAI 兼容客户端。

## 数据保存在哪里

程序是单文件，**方案等所有配置都保存在用户数据目录**（不在 exe 目录）：

```
%APPDATA%\LlamaManager\
├─ profiles.json   模型档案 + 各方案参数（最重要的数据）
└─ settings.json   全局设置（server 路径 / 语言 / 主题…）
```

换机迁移：把整个 `%APPDATA%\LlamaManager\` 目录拷走即可；也可用界面「导入 / 导出」转移单个方案。

## 完整性校验（可选）

```powershell
# Windows PowerShell
Get-FileHash .\LlamaManager-1.28.0-win64.exe -Algorithm SHA256
# 结果应与 LlamaManager-1.28.0-win64.exe.sha256 中一致
```

## 常见问题

- **启动后立即退出 / 端口被占用**：查看服务日志；换一个空闲端口试试。
- **GPU 不工作**：请下载 CUDA / Vulkan 版 `llama-server`，并在方案的「GPU 层数」中设置大于 0。
- **杀毒软件误报**：PyInstaller 打包的单文件程序偶尔会被误报，添加信任即可。

## 关于源码

当前仅发布编译好的程序。**源码将在条件成熟后开源**（届时请留意本仓库更新）。

---

由 [llama.cpp](https://github.com/ggml-org/llama.cpp) 驱动的本地大模型管理与启动器。
