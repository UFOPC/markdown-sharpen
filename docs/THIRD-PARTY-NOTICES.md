# 第三方许可清单 · THIRD-PARTY-NOTICES

生成日期 2026-10-17。本文件是**清单与口径**，不是许可文本的替代品：每个组件的许可以原项目原文为准。

## 0. 我们自己的授权口径（先把能证的和不能说分的清）

| 事实 | 口径 |
| --- | --- |
| `LICENSE`（仓库根，202 行） | Apache License 2.0 标准文本，附录占位行仍是模板的 `Copyright [yyyy] [name of copyright owner]`（Apache 官方样例就这样，不是漏改） |
| 分发形态 | **只发成品（两支 exe），当前不公开源码**（2026-10-17 用户裁决） |
| 于是能说什么 | 「成品按 Apache-2.0 条款授权」——这是我们能兑现的那一半 |
| 于是不能说什么 | 「开源」「源码可用」「自由再分发源码」——许可里关于源码形式的权利在你拿到源码之前无从行使 |

**为什么 `package.json` / `src-tauri/Cargo.toml` 里不加 `license` 字段**（刻意不做）：许可口径现在只写在 `LICENSE` + `README.md` §License + 本文件三处。往构建元数据里再塞一个字符串就是第四本账——它不进成品、没人读、漂了没人红。`package.json` 同样没有 `author` 字段（版权人名号未定，见 §6），**不编一个填进去**。

## 1. JS 依赖 · 运行期（打进 dist，随成品分发）

来源：`package.json` 的 31 条 `dependencies`，逐一读 `node_modules/<pkg>/LICENSE*` 与 `package.json:license`。

| 包 | 许可 | | 包 | 许可 |
| --- | --- | --- | --- | --- |
| `@codemirror/autocomplete` | MIT | | `katex` | MIT（代码；字体见 §4） |
| `@codemirror/commands` | MIT | | `markdown-it` | MIT |
| `@codemirror/lang-css` | MIT | | `markdown-it-container` | MIT |
| `@codemirror/lang-html` | MIT | | `markdown-it-footnote` | MIT |
| `@codemirror/lang-javascript` | MIT | | `markmap-lib` | MIT |
| `@codemirror/lang-json` | MIT | | `markmap-view` | MIT |
| `@codemirror/lang-markdown` | MIT | | `pele` | MIT（Obsidian 出品；随仓库 `vendor/pele-1.10.0.tgz` 静态引入，无运行时依赖） |
| `@codemirror/lang-python` | MIT | | `prismjs` | MIT |
| `@codemirror/lang-rust` | MIT | | `react` | MIT |
| `@codemirror/lang-sql` | MIT | | `react-dom` | MIT |
| `@codemirror/language` | MIT | | `reveal.js` | MIT |
| `@codemirror/search` | MIT | | `turndown` | MIT |
| `@codemirror/state` | MIT | | `zustand` | MIT |
| `@codemirror/view` | MIT | | `chart.js` | MIT |
| `@tauri-apps/api` | Apache-2.0 OR MIT | | `@tauri-apps/plugin-dialog` | MIT OR Apache-2.0 |
| `@tauri-apps/plugin-opener` | MIT OR Apache-2.0 | | | |

一条都没命中 copyleft。下钻一层（各包的直接依赖）扫过一遍，无 GPL / AGPL / SSPL / CC-BY-NC。⚠ 这条结论的范围是**直接依赖 + 一层**，不是全依赖图。

## 2. JS 依赖 · 构建期（不进成品）

`@tauri-apps/cli` Apache-2.0 OR MIT · `typescript` Apache-2.0 · `vite` MIT · `esbuild` MIT · `@vitejs/plugin-react` MIT · `@types/{node,react,react-dom,prismjs,turndown,markdown-it,markdown-it-container,markdown-it-footnote}` MIT。
构建工具不随成品分发，义务面与成品无关；列在这里是为了「装了些什么能在本机跑起来这条构建链」可对账。

## 3. Rust crate（静态链接进两支 exe）

**方法**（可复跑）：解析 `src-tauri/Cargo.lock` 的全部 `[[package]]` 行 → 按 `<name>-<version>` 在本机两个 registry 源缓存目录（`index.crates.io-…` 与 `rsproxy.cn-…`，本机镜像配置导致两源混用）里取 `Cargo.toml` 的 `license =` 字段；再用 `src-tauri/target/release/deps/*.rlib`（去名去哈希）交叉出**实际参与链接**的集合。

| 量 | 实测 |
| --- | --- |
| `Cargo.lock` 里的 crate 条目 | **569** |
| 参与 release 链接的（rlib） | **299** |
| 许可字段已读到 | **455 / 569** |
| 未读到 | 114 —— 逐条核对后：它们全是**同名多版本**里的另一版（如 `base64 0.21.7` 未读到而 `0.22.1` 读到）或本机未缓存的交叉平台/构建期条目；**没有任何一个是「某个参与链接的 crate 的唯一版本记录」**。所以参与链接的 crate 至少都有一条许可记录。 |

分布（前几名，完整表见生成时的原始输出）：`MIT OR Apache-2.0` 218 · `MIT` 88 · `Apache-2.0 OR MIT` 47 · `MIT/Apache-2.0` 21 · `Unicode-3.0` 18 · `Unlicense OR MIT` 9 · `Zlib OR Apache-2.0 OR MIT` 7 · `MPL-2.0` 5，余下各 1–4。

### copyleft 命中（7 条，这是本文件真正需要处理的部分）

| crate | 许可 | 我们的处置 |
| --- | --- | --- |
| `cssparser 0.36.0` | MPL-2.0 | **未修改**，原样静态链接 |
| `cssparser-macros 0.6.1` | MPL-2.0 | 同上 |
| `dtoa-short 0.3.5` | MPL-2.0 | 同上 |
| `option-ext 0.2.0` | MPL-2.0 | 同上 |
| `selectors 0.36.1` | MPL-2.0 | 同上 |
| `r-efi 5.3.0` / `6.0.0` | MIT OR Apache-2.0 **OR** LGPL-2.1-or-later | 三许可可选 ⇒ 按 **MIT** 取用，LGPL 义务不触发 |

MPL-2.0 是**文件级** copyleft：不要求我们开源自己的代码，但它 §3 要求分发可执行文件时**附上该许可文本**，并给出「被覆盖文件的源码从哪、怎么拿」的显式说明。我们的处置 = 本文件点名这些 crate + 原项目发布位（`crates.io/crates/<name>`，该页给出仓库与源码下载），源码即原项目未修改版本。⚠ 这一步以前**没做**（仓库里既无 NOTICE 也无本文件），是本文件补上的。

## 4. 字体（OFL —— 这一节是本次新查出来的，之前无人记账）

成品里确实带着两类字体二进制，两条都是**实测**：

1. **KaTeX 数学字体 20 族**（`node_modules/katex/dist/fonts/`，TTF/WOFF/WOFF2）。
   KaTeX 的 npm 包只带一份 MIT `LICENSE`（那是**代码**的许可），**没带字体许可文本**；字体自己的许可写在字体文件里——用 fontTools 读 `name` 表，20 个 TTF **全部**给出 `nameID 14 = http://scripts.sil.org/OFL`，`nameID 13 = Copyright (c) 2009-2010, Design Science, Inc.` 与 `Copyright (c) 2014-2018 Khan Academy` ⇒ **SIL Open Font License 1.1**。`KaTeX_Main-Regular.woff2` 单独复核，同样带这两条记录（woff2 容器保留了 name 表）。
2. **Source Sans Pro 4 字重**（`node_modules/reveal.js/dist/theme/fonts/source-sans-pro/`）。
   入口是 `SlidesStage.tsx:192` 之后 `import("reveal.js/dist/theme/white.css")`，而该文件 `:6` 有一行 `@import url(./fonts/source-sans-pro/source-sans-pro.css)` ⇒ Vite 把字体切成资产、Tauri 再嵌进 exe。实测产物目录里 4 个 `.woff` 的字节数正好是原项目四文件各自 **+5**（codegen 的包装偏移），一一对上：98,556 / 114,324 / 115,648 / 98,816 B。许可文本原项目**带着**：`…/source-sans-pro/LICENSE`（44 行，OFL，`Copyright 2010, 2012 Adobe Systems Incorporated, with Reserved Font Name 'Source'`）。`league-gothic` 未被引用，没进包。

OFL 1.1 允许把字体嵌入并再分发程序，条件是分发时**同时给出许可文本与版权声明**，且不得单卖字体、派生版不得用保留字体名。我们**没有改动任何字体**，且字体自带的 name 记录会随二进制一起走——但那只对能读字体元数据的解码器可见，对用户不可见。

⇒ **待办（见 §6）**：OFL 全文要作为文本随成品走一遍，不能只靠字体自己的 name 表。

另外两条澄清，免得被误记成第三方字体：`src/styles/global.css:8` 的 `@font-face "CJK2x"` **只写 `local()`**（引用本机已装字体，不下载不分发）；界面图标不是字体图标，是我方从 `MD.svg` 生成的位图/`ico`（`scripts/gen-icon-set.mjs`）。

## 5. 不在清单里的东西（也说明一下）

`public/html-sharpen/html-sharpen.html` 与 `themes/*.css` 全是本仓自研；`src-tauri/icons/` 自研；`.mds/` 是运行时数据目录，不含第三方代码。AI 侧**不内置任何服务商**，运行时由用户自填接口，因此不产生第三方 SDK 依赖。

## 6. 缺口（明写，不含糊过去）

| # | 缺口 | 处置 |
| --- | --- | --- |
| 1 | OFL 全文未随成品分发（§4） | 需要一条能落地的路径：在 使用说明/帮助 里加「第三方许可」一页，或把文本随包发布。⚠ 前者要动 `uiCopy` + `HelpDialog` 的键数与「6 个选项」那类硬编码计数，**不在 v0.2.8 本批**，排到下一批单独定 |
| 2 | 版权人名号未定 | `LICENSE` 的 (c) 行与 `package.json:author` 都缺一个名号；**不代填**，等用户给 |
| 3 | 「Apache-2.0」在仓库里此前只有一句话（`README.md:141`），无 NOTICE、无本文件 | 本文件即补齐动作；口径改写成 §0 那两句能证的 |

## 7. 复跑本清单

```bash
node C:/tmp/lic.mjs src-tauri/Cargo.lock          # Rust crate 许可分布 + copyleft 命中 + 未取到清单
stat -c '%s' src-tauri/target/release/build/*/out/tauri-codegen-assets/*.woff*   # 字体资产
uv run --with fonttools --with brotli python -c "…name 表…"                        # 字体许可记录
```
