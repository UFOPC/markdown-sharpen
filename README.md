# Markdown-Sharpen

[English](./README.en.md) · **中文**

**MDS-Lite（莫得闲）**：Windows 上的只读 Markdown 阅读器，单文件、免安装、不联网。

它主要为这个场景做的：用[小红虾](https://github.com/UFOPC/red-clipper-sharpen)把资料剪藏成 Markdown 之后，在本地舒服地读完——多标签对照、搜索、高亮、图表、公式、朗读，打开就能用，不给剪藏库添任何多余文件。

Markdown-Sharpen 家族：**Lite（本仓库，阅读器）先行**；三款编辑器的功能分工见「版本路线」。

## 下载

当前版本 **MDS-Lite 0.1.6**，[全部历史版本](https://github.com/UFOPC/markdown-sharpen/releases)。

| 文件 | 说明 |
| --- | --- |
| [MDS-Lite.7z](https://github.com/UFOPC/markdown-sharpen/releases/download/reader-v0.1.6/MDS-Lite.7z) | 主程序压缩包，2.2 MB，解压后双击 `MDS-Lite.exe` 即用 |
| [FONT-LICENSES.txt](https://github.com/UFOPC/markdown-sharpen/releases/download/reader-v0.1.6/FONT-LICENSES.txt) | 内嵌字体的许可全文（OFL 要求随包给出） |

系统要求：Windows 10 / 11（64 位）。唯一外部依赖是 WebView2 运行时，Windows 11 已预装；老系统若缺，按首次启动的提示装一次即可。

首次运行可能遇到 SmartScreen「未知发布者」提示：exe 没有代码签名，属预期，点「仍要运行」。

下载后可核对 SHA256：

```
MDS-Lite.7z   540ad1d426ad97852a7d57a2e476247cb49e0f6cb66b4c64f47c809f3707e8c1
```

## 读剪藏，它能帮上什么

- **打开就能读**：支持 `.md` / `.markdown` / `.mdown` / `.mkd` / `.txt`，拖进窗口或 `Ctrl+O` 都行；也可以把它注册成 `.md` 的候选打开方式，之后双击剪藏文件直接进阅读器。
- **资料多了也不乱**：多标签、单双栏对照（左右或上下），重启后恢复上次的标签和每篇读到的位置。
- **找得快**：大纲跳转、文内搜索、跨标签全文搜索，支持整词与大小写。
- **重点留得住**：三色高亮标记，跟着文档走，下次打开还在。
- **剪藏里的技术内容照常呈现**：KaTeX 公式、Mermaid 图表、Chart.js 数据图、Markmap 思维导图，另有整篇文档的导图视图。
- **不想看可以听**：系统语音朗读，从滚动位置或点选的段落起念，语速音色可调。
- 五套主题、字号行距缩放；文件被别的编辑器改过，回到窗口自动重读。

## 它刻意不做什么

- **不改你的剪藏**。没有注册任何写命令，Markdown 原文一个字节都不会动。
- **不在剪藏目录建东西**。不会在资料旁边生成 `.mds`、`assets` 之类的目录，剪藏库保持原样。
- **不联网**。没有更新检查、没有遥测、没有账号。正文里的外链点击只用系统浏览器打开，阅读器自己不出网。
- **不做格式转换**。没有集成 pandoc 之类的转换器——如果将来做，会放在单独的 Plus 变体里，不占用 Lite 的体积。

## 数据放在哪

阅读进度、最近打开、高亮和界面配置都存放在：

```
%APPDATA%\com.mdsharpen.reader\state.json
```

删除这个文件等于重置。它与其他版本的配置目录是物理隔离的，互不影响。

## 常用操作

| 操作 | 效果 |
| --- | --- |
| `Ctrl+O` | 打开文件（也可把文件拖进窗口） |
| `Ctrl+F` / `Ctrl+Shift+F` | 文内搜索 / 跨标签搜索 |
| `Ctrl+W` / `Ctrl+Tab` | 关闭标签 / 切换标签 |
| 顶栏「分栏」图标 | 单栏 ↔ 双栏（同一篇也能左右对照） |
| 顶栏「链条」图标 | 注册 / 取消文件关联（只登记为候选，不抢默认程序） |
| 点一下正文段落 | 设为朗读起点 |
| `F1` | 用法速查 |

## 版本路线

- **Lite（阅读器）**：当前发布线，配合小红虾剪藏阅读持续完善。
- **标准版 / Pro / Plus（三款编辑器，功能规划）**：有需求就随时发布，功能分工如下。
  - **标准版（写作）**：保真编辑器、双链知识库、表格、HTML 阅读、AI 助手（自填 OpenAI 兼容凭据）。
  - **Pro（技术创作与转换）**：在标准版之上，加公式与图表、docx 导出、HTML 可视化编辑、演示模式，并含部分 pandoc 转换能力。
  - **Plus（完整格式转换，规划）**：pandoc 类全格式转换。

## License

本作品按 [Apache-2.0](LICENSE) 条款授权。本公开仓库当前只放发布门面与成品。视需求公开源码。

第三方组件与原项目参照的许可逐项列在 [docs/THIRD-PARTY-NOTICES.md](docs/THIRD-PARTY-NOTICES.md)；随包内嵌的 KaTeX 字体为 SIL OFL 1.1，全文随每个 Release 以 `FONT-LICENSES.txt` 给出。

发现问题请到 [Issues](https://github.com/UFOPC/markdown-sharpen/issues) 反馈。
