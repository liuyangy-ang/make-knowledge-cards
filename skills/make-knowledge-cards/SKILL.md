---
name: make-knowledge-cards
description: Turn pasted article text or local Markdown and TXT files into concise, source-grounded knowledge cards. Use when a user asks to extract, study, or review key ideas from text. Does not fetch webpages or parse PDFs.
---

# Make Knowledge Cards

Convert the user's supplied text or a local `.md`/`.txt` file into 5–8 knowledge cards when the source supports that many distinct useful ideas. Work in the source language unless the user requests another language.

## Input handling

- Accept pasted text or a local Markdown/TXT path. If both are supplied, use the user's stated preference; otherwise use the file.
- Read only local `.md` and `.txt` files. Do not fetch URLs, parse PDFs, or import Anki decks.
- If asked to process a URL or PDF, reply: “暂不支持直接处理该格式，请将文本内容复制后粘贴给我，或提供 TXT/MD 文件路径。”
- If a file is missing, unreadable, or a different format, state the problem and request supported text or a TXT/MD path.
- If the source is extremely short or contains no substantive knowledge, return exactly: “输入内容过短，无法生成知识卡片”.

## Extraction

1. Identify distinct, important claims, concepts, methods, or relationships explicitly supported by the source.
2. Merge duplicates and omit incidental details. Keep one independent point per card. Preserve important source terms and especially apt key phrases without changing their meaning.
3. Choose 5–8 cards based on information density. Fewer than five are acceptable when the source does not support five distinct, useful cards; never pad. Do not invent facts, explanations, examples, or answers. A plain-language explanation must remain entailed by the source. If the source cannot support an example, use a self-test question answerable from the source.
4. For long input, use the available context responsibly: when the full text cannot fit, divide it into coherent chunks, extract candidate points per chunk, then deduplicate and select across the source. If chunking is not feasible, process a clearly bounded beginning portion. Do not imply full coverage after truncation. Prefix the result with “因文本过长，已截取/分段处理核心内容”.

## Output format

For each card, output exactly these four fields, in this order, using Markdown. Do not add other card fields:

### [标题]
- **核心知识：** One or two sentences stating the point directly.
- **简明解释：** A plain-language explanation grounded in the source.
- **例子或自测问题：** One concrete source-supported example, or one question answerable from the source.

Separate cards with a blank line. Do not add an introduction or conclusion, except the required long-input prefix. The bracketed title is a placeholder; replace it with the actual concise title. Ensure the output's four fields are exactly title, core knowledge, simple explanation, and example or self-test.

## Example

Source excerpt: “间隔复习是在不同时间点重复学习材料。它利用遗忘随时间发生的特点，把复习安排在逐渐拉长的间隔中。”

### 间隔复习利用逐渐拉长的复习间隔
- **核心知识：** 间隔复习是在不同时间点重复学习材料，并逐渐拉长复习间隔。
- **简明解释：** 不把复习挤在同一时段，而是在之后的不同时间再回顾。
- **例子或自测问题：** 根据这段话，间隔复习的复习时间如何变化？
