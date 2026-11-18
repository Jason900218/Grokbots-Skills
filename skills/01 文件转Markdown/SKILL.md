---
name: 文件转Markdown
description: >-
  当需要阅读较大的 Word、PPT、PDF 或图片，或为节省 token 先把这类文件转成 Markdown 再读时使用。以后遇到类似情况都要优先转成
  md。
---
# 文件转 Markdown

阅读较大的 Word、PowerPoint、PDF、图片时，先转成 Markdown，再读 md，不要直接把原始二进制文件整份塞进上下文。原件只作对照和排版依据，不要覆盖。

## 1. 把文件放到共享电脑

文件若在用户电脑上，先用 `ListMachines` 确认机器在线，再用 `CopyToBox` 逐份拷贝到盒子（单文件不超过 100 MiB）。大文件一次一个，等当次拷贝完成再拷下一个。已在盒子上的文件直接使用。

## 2. 转换

输出与源文件同名的 `.md`，放在专门目录（如 `/workspace/.../md/`），不要写回用户原目录覆盖原件。

优先用盒子上已安装的 `markitdown`：

```bash
markitdown "input.docx" -o "output.md"
```

支持常见的 `.docx` `.pptx` `.pdf` `.xlsx` `.html` 及常见图片。读标准输入时可加 `-x` 或 `--mime-type` 提示格式。

若 `markitdown` 失败或结果明显缺失，按类型降级：

- PDF：`pdftotext -layout`；扫描件或图文混排时再辅助 OCR或描述页面截图
- Word：用 Python 读 `word/document.xml` 或 `python-docx` 抽段落与表格；有 `pandoc` 时也可用
- PPT：先 `markitdown`；仍不清楚时再按页提取文字，必要时渲染页面集中描述版式与图
- 图片：先把图放到盒子，用 Read 看图；有大段印刷体文字时再 OCR，把识别结果写进 md
- Excel：先 `markitdown` 或导成 CSV 后再读；注明工作表名与范围

## 3. 怎么读

转完只读 Markdown。先看目录与文件大小，再按需分段读，不要一次把不相干的长文全部塞进上下文。

转换不会完全保留排版、页眉页脚、文字框位置、批注和复杂图表。md 用于掌握事实与结构；写份或对版式时，再打开原件核对字体、页边距、表格和页数。

数字、名称、条款只以源文件为准。转换丢失、乱码或看不清的地方标为「待核对」，不要猜写。

## 4. 交付

在工作记录里写清：源文件路径、md 路径、用了哪种转换方法、哪些内容可能丢失。只把任务需要的摘要交给上级，不要把全部 md 贴回聊天。
