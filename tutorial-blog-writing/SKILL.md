---
name: tutorial-blog-writing
description: Use when the user says "博客" (blog) or "教程" (tutorial)
---

# Tutorial/Blog Writing Convention

## Overview

This skill guides the AI in writing Chinese technical tutorials. There is only one core goal: **a complete beginner with zero background should be able to become an expert in the topic after reading the article**.

This means:
- Every concept must be explained from scratch, assuming the reader knows nothing
- Every term must be explained to the point that a layperson can understand it
- Every step must come with code examples and run results so the reader can follow along
- Progress step by step, starting from the simplest and gradually going deeper
- The end goal is that the reader can work independently and solve real problems after reading

At the same time, the article must read like notes handwritten by a real person, not an AI-generated textbook.

## When to Use

**Applicable scenarios:**
- Writing Chinese technical tutorials aimed at zero-background readers
- Removing traces of AI generation, aiming for a handwritten-notes style
- Long-form technical content such as blog posts and teaching documents
- Hands-on tutorials where readers are expected to follow the code step by step

**Not applicable:**
- English technical articles (language habits and writing conventions are completely different)
- Pure API reference documentation (no need for tutorial-style explanations and code examples)
- Non-technical writing such as fiction, prose, or essays
- Casual chat or short social media content
- Academic papers or formal technical reports (different format requirements)

## Core Patterns

Below are the most essential writing patterns of this skill; each one is key to distinguishing an AI article from a handwritten one. Detailed rules are in the later sections.

| Pattern | Core rule | Detailed section |
|------|---------|---------|
| Alternate code and text | Every knowledge point is immediately followed by code + run results; long stretches of pure text are forbidden | [Code-to-Text Ratio](#code-to-text-ratio) |
| Explain terms on first use | When a term first appears, use the format "中文全称（英文，缩写）：plain-language explanation" | [Explaining Technical Terms](#explaining-technical-terms) |
| Tables first | Anything listable—APIs, parameters, function lists—must use tables | [Using Tables](#using-tables) |
| No summaries | End right after the last knowledge point; no summary/next steps/pleasantries | [Article Structure](#article-structure) |
| Natural comments | Inline comment format: `code # comment`, no alignment | [Code Comment Format](#code-comment-format) |
| Real run results | Code run results must be copied from actual execution, never fabricated | [Verifying Code Runnability](#verifying-code-runnability) |
| Verifiable installation | Every installation step comes with a verification command, split by OS | [Writing Installation Steps](#writing-installation-steps) |
| Anticipate errors | Error-prone code is immediately followed by common errors and solutions | [Error Handling and Troubleshooting Guide](#error-handling-and-troubleshooting-guide) |
| Progressive code | The same concept grows in complexity across the article; don't overwhelm the reader | [Progressive Code Complexity](#progressive-code-complexity) |
| Multi-platform support | Commands, paths, and package managers explicitly labeled with the OS | [Multi-Platform Notes](#multi-platform-notes) |

## Tone and Address

- **Assume the reader has zero background.** Before writing each sentence, ask yourself: would a beginner understand this? If a term isn't explained or a step is skipped, the beginner falls behind. Better to over-explain than to assume the reader "should know".
- Tone: **like taking notes or writing a reference manual**, not like lecturing. Remove teaching-style phrases like「首先让我们来了解一下...」「接下来我们将学习...」("First let's take a look at...", "Next we will learn...").
- **It's OK to honestly state the limits of the content.** For example, "该教程并不适合完全零基础的读者" ("this tutorial isn't suitable for complete beginners")—this kind of honesty is characteristic of handwritten articles.
- Keep sentences short. Prefer short sentences over long ones; prefer separate lines over piling everything into one paragraph.

## Forbidden Items (AI-Flavor Removal Checklist)

The following behaviors are **strictly forbidden**:

1. No openings like「在当今这个 xxx 的时代」("In today's era of xxx").
2. No boilerplate phrases like「总而言之」「综上所述」「值得注意的是」「需要强调的是」("in conclusion", "to sum up", "it's worth noting", "it must be emphasized").
3. No polite closing lines like「希望这篇文章对你有所帮助」("hope this article helps you"); no ending sections like「总结」「小结」("Summary")—finish the last knowledge point and stop, no gilding the lily.
4. No long stretches of pure text—tutorials must alternate between code and text. More than 3 consecutive paragraphs of pure text (no code, no lists, no tables) is not allowed.
5. No empty made-up filler—if you don't know a detail, write less rather than inventing it.
6. No long-winded, rambling, or lyrical openings—tutorials focus on substance; open with 1-3 sentences of overview and get straight to the point.
7. No `---` horizontal rules to separate sections—one blank line between sections is a natural enough transition.

## Emoji Usage

**Use in moderation; natural is best.**

- Quantity: keep it to **2-5** emojis per article—not too many, not zero.
- Placement: at the end of a sentence or paragraph, as a touch of tone; never in headings.
- Suitable: tips (💡), warnings (⚠️), emphasis (🔥), a dash of mood (🤔).
- Forbidden: adding emojis to several consecutive paragraphs, or using emojis as list bullets.

## Metaphors and Analogies

**Use in moderation, only when they genuinely aid understanding.**

- Quantity: keep it to **1-2** metaphors per article.
- Use them only when an abstract concept needs to be made concrete; use once and move on—no piling up.
- Forbidden: flowery literary metaphors ("巨轮航行在代码海洋" — "a great ship sailing the ocean of code"), or long fable-style metaphors.
- The mark of a good metaphor: precise, short, like something a real person would say in casual conversation.

## Article Structure

### Opening

**The article body does not start with an `# Title`.** The title lives in the file name; the body starts directly with the overview. No `---` rules between sections—one blank line is a natural transition.

```markdown
简短概述 → 官方链接/参考链接（如有）→ 直接进入正题
```

```markdown
xxx 是一个 xxx。它的主要特点是 xxx。

相关网址:

- 官方文档：https://xxx.com
- 教程：https://xxx.com

```

### Heading Levels

**No H1 as the article's main title inside the body.** The body starts directly with the overview paragraph; the first section heading uses `#` (level 1), subsections use `##` (level 2), and so on.

```markdown
# 章节标题

## 小节标题

### 小小节标题
```

### Ending

Stop right after the last knowledge point. **No** summary paragraph, **no** "what to learn next", **no** pleasantries.

## Writing Installation Steps

Installation is where beginners get stuck most easily; it must be written with zero ambiguity and be verifiable. Iron rules for installation steps:

- **Split by OS**: if the tool installs differently on Windows/Mac/Linux, list each separately—never write just one
- **Every step gets a verification command**: right after installing something, tell the reader how to confirm it worked, e.g., after installing Python immediately follow with a `python --version` check
- **Package managers first**: if `pip install`, `npm install`, or `brew install` can do the job, prefer the package manager command over sending readers to download installers from official sites
- **Plan for network issues**: readers in mainland China may hit slow or failing pip/npm downloads; provide mirror options (e.g., `pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple`)
- **What success looks like**: use text or screenshots to show what the terminal should output after a successful install, so readers can compare
- **Pitfalls like environment variables**: for PATH and environment variables, spell out where to set them and how to verify the setting took effect

Installation step example template:

```markdown
## 安装

### Windows

下载安装包：https://xxx.com/download

安装时勾选「Add to PATH」——这一步很重要，不勾的话后面命令会报错。

装完后打开终端（PowerShell 或 CMD），输入：

```shell
python --version
```

看到类似 `Python 3.8.10` 的输出就说明装好了。

### Mac

```shell
brew install python@3.8
```

验证：

```shell
python3 --version
# 输出：Python 3.8.10
```

### 国内网络问题

如果下载很慢，先换国内镜像源：

```shell
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
```

## Pacing Control

A tutorial is not a running log. Different content needs different pacing:

| Content type | Pace | Approach |
|---------|------|------|
| Core concepts (e.g., closures, prototype chains) | **Slow** | First explain in plain language why it's needed, then give the simplest code example; let the reader digest |
| Basic syntax (e.g., variable assignment, loops) | **Fast** | Code + comments is enough; no lengthy explanations—zero-background readers can understand code plus comments |
| Installation/environment setup | **Detailed** | Every step gets a screenshot or command output; no skipping steps |
| Hands-on projects | **Slow then fast** | Break the first feature down in detail; later features get code + key comments only |
| Advanced tips | **Fast** | Code + a one-line note; readers who want depth can dig in themselves |

Concrete pacing rules:

- After each important concept, add one transition sentence before the next concept—readers must never feel the topic jumped
- Five or more consecutive simple points can be merged into one quick section, so the article doesn't become an API list
- No more than 3 "hard parts" (concepts the reader must stop and think about) per article; if there are more, split into multiple articles

## Multi-Platform Notes

Whenever the tutorial involves commands, paths, or package managers, platform differences must be handled explicitly:

- **Command differences**: Windows uses backslashes `\`, Mac/Linux use forward slashes `/`; Windows terminal commands differ (`dir` vs `ls`) and must be given separately
- **Path styles**: mixing `F:/environment/...` and `/usr/local/...` in examples is a normal trait of handwritten articles and doesn't need unifying—but clearly label which OS each path belongs to
- **Shortcut differences**: `Ctrl+C` vs `Cmd+C`; on first appearance note「Mac 用 Cmd 替换 Ctrl」("on Mac, replace Ctrl with Cmd")
- **If only one platform is covered**: declare at the start of the article「本文以 Windows/Mac/Linux 为例」("this article uses Windows/Mac/Linux as the example") so readers on other platforms aren't blindsided

Example:

```shell
# Windows (PowerShell)
python hello.py

# Mac / Linux
python3 hello.py
```

## Title Naming Convention

The article's title (i.e., the file name) directly affects how well it spreads. Follow these rules:

- Title length: **10-30 Chinese characters**; too long dilutes information density, too short is unclear
- Title format: `技术主题：一句话描述` (topic: one-sentence description), e.g., `Python 装饰器：从闭包到实战`
- **No** clickbait (「全网最全」「一篇文章搞懂所有 xxx」— "the most complete on the whole internet", "understand all of xxx in one article"), but do convey the article's value accurately
- **No** piling version numbers into the title; version info goes in the environment note at the start of the article
- The file name is the article title; don't repeat it as an H1 in the body

## Images and Screenshots

Images in a technical tutorial should serve the content, not decorate it:

- **Screenshots must be annotated**: mark key areas with arrows, boxes, or numbers—never drop in a bare screenshot and make readers hunt
- Resize the window before capturing; capture only the relevant area, not the full screen
- Choose **either** a screenshot **or** text output for code results—prefer copyable text output (so readers can copy and verify); use screenshots only for GUI content
- Image naming: lowercase English + hyphens, e.g., `pip-install-success.png`
- **Alt text is mandatory**: `![pip 安装成功界面](pip-install-success.png)`—never leave alt empty

## Code-to-Text Ratio

- **Every concept/knowledge point must be immediately followed by a code example.** The reader should see how it's used in code right after reading the concept.
- The number of code blocks should equal or exceed the number of body paragraphs.
- **Run results must be shown.** Readers need to know what the code looks like when it runs, so they can verify their own attempt. A tutorial without run results might as well not exist.
- Use the compact bullet + code block pattern:

```markdown
- 返回列表的长度

`len(number)`

- 循环打印列表元素

`for i in number:
    print(i)`
```

- Code run results must be displayed:

```markdown
运行结果

`a =  [1, 2, 3, 4, ['a', 'b'], 5]
b =  [1, 2, 3, 4, ['a', 'b'], 5]`
```

## Progressive Code Complexity

Don't present the final version of the code right away. Readers need to see the code "grow" from simple to complex:

- **The first time a concept appears**, give the simplest example—one variable, one function call, no full program structure needed
- **The second time**, add one dimension on top—e.g., add a loop or wrap it in a function
- **The last time**, give the complete code with error handling and edge cases

Example (reading a file in Python):

First appearance (simplest):
```python
with open("data.txt") as f:
    print(f.read())
```

Second appearance (add a loop):
```python
with open("data.txt") as f:
    for line in f:
        print(line.strip())  # strip() 去掉每行末尾的换行符
```

Last appearance (complete):
```python
try:
    with open("data.txt", encoding="utf-8") as f:
        for i, line in enumerate(f, 1):
            print(f"第{i}行: {line.strip()}")
except FileNotFoundError:
    print("文件不存在，请检查路径")
```

Bridge each version with text, e.g.:「上面的写法能跑，但一行一行读更省内存。改一下——」("The version above works, but reading line by line saves memory. Let's tweak it—")

## Inline Code vs Code Blocks

An easily overlooked detail that heavily affects reading experience:

| Scenario | Use | Example |
|------|------|------|
| File names, module names, function names, variable names mentioned in prose | Inline code | the `main()` function in `app.py` |
| Terminal commands embedded in prose | Inline code | run `pip install requests` in the terminal |
| Values of configuration options | Inline code | change `timeout` to `30` |
| Complete code statements (even a single line) | Code block | see below |
| Shell commands and their output | Code block | see below |
| Configuration file content (JSON/YAML, etc.) | Code block | see below |

One-sentence test: **things the reader needs to copy-paste go in code blocks; things the reader only needs to know the name of go in inline code.**

## Code Comment Format

### Core Rule

The inline comment format must be: **code + one space + comment symbol + one space + comment text**. No alignment, no tidy columns.

Correct format (natural):

```python
from wayw import app as app_module  # noqa: F821
app_module.config._settings_cache = None  # type: ignore
```

```python
number.pop(1) # 删除第一个元素
number.remove(3) # 删除数组中元素为3的元素
```

```python
self.adb = ADB(self.serialno,adb_path="F:/environment/Android_SDK/platform-tools/adb.exe")
self.adb.wait_for_device()
```

```go
var name string = "张三"  // 显式声明
score := 95               // 短声明
```

```shell
ls -la                     # 详细列表含隐藏文件
cd ~                       # 回主目录
```

### Forbidden Aligned Comments

The following format is a telltale AI trait and is **strictly forbidden**:

```python
# ❌ 禁止：工整对齐的注释
name          = "张三"     # 用户姓名
age           = 25          # 用户年龄
email         = "z@x.com"   # 用户邮箱
```

```python
# ❌ 禁止：注释符号前没有空格
x = 5# 定义变量
```

```python
# ❌ 禁止：注释符号后没有空格
x = 5  #定义变量
```

### Comment Content Requirements

- Comments only explain **key logic**, not "what this is" basic syntax.
- Comment style can be casual—exclamation marks, colloquial phrasing, abbreviations are fine; don't write them like API docs.

```python
# ✅ 好注释：解释为什么
number = 5.454245435
round(number,3) # 保留3位小数

# ❌ 坏注释：描述代码本身
# 定义一个名为 x 的变量并赋值为 5
x = 5
```

### Cross-Language Rules

| Language | Comment format (correct) |
|------|-----------------|
| Python | `code # comment` |
| JavaScript/Go/Rust/C | `code // comment` |
| SQL | `code -- comment` |
| Shell | `code # comment` |

Uniform across all languages: **space + comment symbol + space**.

## Using Tables

API lists, parameter descriptions, function lists, type mappings—**anything that can be laid out as a table must use a table**.

```markdown
| 函数 | 作用 |
|------|------|
| len(list) | 返回列表元素个数 |
| max(list) | 返回列表元素最大值 |
```

## Citations and Attribution

Whenever external material is referenced, it must be attributed:

- `引用：[链接]` — content partially borrowed but rewritten
- `参考：[链接]` — ideas borrowed from the content
- `转载：[链接]` — original material quoted directly
- `源自：[链接]` — this part is mainly sourced from there

```markdown
> 引用：https://www.runoob.com/python3/python3-tutorial.html
```

## Code Repository Links

If the article has a companion source code repository:

- Put the repo link after the opening overview paragraph, before the first section
- Link format: `GitHub 仓库：https://github.com/xxx/xxx`, placed inside a quote block
- The README must at least include: project intro, environment requirements, installation steps, how to run
- The code in the repo must be **exactly identical to the code in the article**, including comments and variable names
- Organize the code into per-chapter folders (`ch01-basics/`, `ch02-advanced/`) so readers can browse along with their progress

## Code Blocks Must Declare a Language

**Every code block must have a language identifier right after the opening triple backticks.** Bare triple backticks (code blocks without a language tag) are forbidden.

Correct:

```python
# ✅ ```python
import os
print(os.getcwd())
```

```shell
# ✅ ```shell
ls -la
```

```sql
# ✅ ```sql
SELECT * FROM users;
```

Incorrect:

```
# ❌ 裸 ```  —— 不允许！(bare ``` — not allowed!)
ls -la
```

Common language identifiers: `python`, `javascript`, `typescript`, `go`, `rust`, `java`, `shell`, `bash`, `sql`, `html`, `css`, `json`, `yaml`, `markdown`, `plaintext`.

Use `shell` or `plaintext` for run results. Sample output (Linux as the example):

```shell
# 运行结果：
linux:~# Hello, World!
```

## Explaining Technical Terms

**Every technical term must be explained clearly the first time it appears.** Assume the reader has zero background—any unexplained abbreviation or term might as well not be written.

### Explanation Format

Standard format: **中文全称（英文原名，缩写）+ colon + one plain-language explanation** (Chinese full name, original English name, abbreviation).

```markdown
RPC（Remote Procedure Call，远程过程调用）：一种技术，让你调用远程计算机上的函数
就像调用本地函数一样，不用关心网络传输的细节。
```

### Explain in Plain Language

Don't explain terms with more terms; use metaphors or plain phrasing a beginner understands:

```markdown
# ✅ 好的解释
API（Application Programming Interface，应用程序接口）：程序之间沟通的"约定"。
比如你去餐厅，菜单就是 API——你按菜单点菜，厨房按菜单做菜，你不需要知道厨房怎么运作。

# ❌ 差的解释
API（Application Programming Interface）：一组预定义的函数和协议，
用于构建软件应用程序的接口。
```

### What Must Be Explained

| Category | Examples |
|------|------|
| Technical abbreviations | API, SDK, ORM, JWT, CSRF, ACID |
| Technical nouns | container, closure, coroutine, serialization, deadlock |
| Protocol names | HTTP, TCP, WebSocket, gRPC |
| Math concepts | matrix, vector, eigenvalue, singular value |
| Tool/framework names on first appearance | Docker, Kubernetes, Nginx, Redis |

### When Not to Explain

- Basic nouns appearing in the first section heading (`#`)—the article is about them, and the whole article explains them
- Terms already explained earlier (no need to re-explain the second time)
- Extremely common words (like "file", "folder", "code", "function")

### Where to Explain

Right after the sentence where the term **first appears**, introduced with parentheses or a dash:

```markdown
Docker 用容器（Container）来运行应用——容器就是一个轻量级的隔离环境，
里面包含了应用所需的全部东西。

Kubernetes（简称 K8s）是一个容器编排平台。
```

## Adapting to Different Article Types

All types follow the same core principle: **start from a first step a beginner can understand, and end with the reader able to independently solve real problems**.

| Type | Zero-to-expert route |
|------|-----------------|
| Programming language | Install → first program → basic syntax (variables/types/control flow) → core features → hands-on project |
| Third-party library | What problem the library solves → install → core API table → code for each API → complete example |
| Database | What a database is → install → CRUD demonstrated one by one → advanced queries → connect from a programming language |
| Command-line | What the tool is → install/enter → common command table → examples grouped by scenario |
| Tooling | What pain point the tool solves → install → core concepts → common operations demonstrated one by one |
| Theory/math | Concepts in plain language → break down the formulas → verify with code → real application scenarios |
| Life/soft skills | What the problem is → why it matters → concrete methods → practical advice → common pitfalls |

## Version Annotation

When the tutorial involves software versions, follow these rules so readers don't get stuck on version mismatches:

- State the author's environment at the top of the article, e.g.:「笔者环境：Python 3.8.10 / Windows 10 / VS Code 1.85」
- Version numbers precise to the **minor version** (e.g., 3.8, not 3.8.10), leaving readers some flexibility
- If a feature requires a specific version, note it:「（需要 Python 3.8+）」
- Mark the **writing date** when publishing, so readers can judge freshness:「本文撰写于 2024 年 1 月」
- If the content is outdated, flag it prominently at the top:「⚠️ 本文内容适用于 xxx 版本，最新版本 API 已变更，仅供参考」

## Verifying Code Runnability

A tutorial's core value is that readers can **follow along and get it running**. If the article's code itself has bugs, readers get stuck and give up. After finishing the article, every code segment must be verified to run.

### Verification Principles

- **Actually run every executable code segment.** Never assume "this segment should be fine".
- Run results shown in the article must be **copy-pasted from an actual run**, never fabricated.
- If the code depends on an environment (specific Python version, installed libraries, OS differences), state it clearly in the article.

### What Must Be Verified

| Code type | Handling |
|---------|---------|
| Complete executable snippets | **Must actually run**; passes only if the result matches the article |
| Shell commands | **Must actually execute**; confirm the output matches the article |
| SQL statements | **Must run against the corresponding database**; confirm the result is correct |
| Config files (JSON/YAML/TOML, etc.) | Check syntax validity and presence of key fields |
| Pseudocode or incomplete sketch code | Label as「示例代码，不可直接运行」("sample code, not directly runnable") |
| Code depending on external services (API calls, etc.) | At least verify the syntax; set up an environment to verify when possible |

### Verification Process

1. Prepare the environment described in the article (versions and dependencies matching what the article declares)
2. Copy and run each code segment in the order it appears in the article
3. Compare actual output with the run results in the article
4. Where they differ, fix the code or fix the article's results until they match
5. For verified segments, display the **actual run output** as the run results in the article

### Handling Common Issues

- **Run errors**: check for missing imports, variable definitions, or prerequisite steps. Tutorial code must be complete and **executable top to bottom in order**.
- **Mismatched results**: output can vary slightly across versions and OSes. Note the range of variation in parentheses after the run result, or pin the exact version used.
- **Cannot run locally**: if the code needs special hardware (GPU) or paid services, at least validate it with a syntax checker for that language.

## Error Handling and Troubleshooting Guide

One dividing line between good and bad tutorials: whether they anticipate the errors readers will hit. A tutorial that only shows the "correct code" loses readers the moment something fails.

### Error Types to Anticipate

| Error type | Trigger scenario | What the tutorial should do |
|---------|---------|--------------|
| Environment errors | Missing dependency, wrong version, PATH not configured | Provide verification commands and match against error messages |
| Syntax errors | Bad indentation, unmatched brackets, typos | Provide the common error message text + fixes |
| Path errors | File missing, wrong path | Teach readers to confirm location with `pwd` / `ls` |
| Permission errors | No read/write permission, port occupied | Note admin mode on Windows, `sudo` on Mac/Linux |
| Network errors | Download timeouts, API unavailable | Provide mirrors, offline options, or how to skip the step |

### How to Write Troubleshooting Content

Format: **if error xxx appears → what the cause is → how to fix it**

```markdown
如果运行时出现：

```shell
ModuleNotFoundError: No module named 'requests'
```

说明 requests 库还没安装。执行：

```shell
pip install requests
```

如果 pip 下载很慢或报 timeout，换清华镜像源：

```shell
pip install requests -i https://pypi.tuna.tsinghua.edu.cn/simple
```
```

### Where to Place Troubleshooting Content

- **Immediately after the code block**: the 1-2 most common errors for that code, right after its run results
- **Not after every code block**: only add troubleshooting for error-prone steps (installation, network requests, file operations, database connections)
- **A consolidated "FAQ" section at the end is allowed**: collect general cross-section issues there

## Common Mistakes

The most frequent mistakes when writing technical tutorials, and their fixes:

| Mistake | Problem | Correct approach |
|------|------|---------|
| Aligned comments | `name = "张三"     # 姓名` | `name = "张三" # 姓名` |
| Bare code blocks | ` ``` ` without a language tag | ` ```python ` |
| Code without results | Readers don't know what running it looks like | Follow every code segment with the actual output |
| Unexplained terms | Assuming readers know API, SDK | Expand the full name + plain explanation on first appearance |
| Ending with a summary | 「综上所述」「希望有帮助」 | End when done; no gilding the lily |
| Long pure-text stretches | More than 3 consecutive paragraphs without code/tables | Break up text with code blocks or tables |
| H1 as the article title | Body starting with `# Title` | The title is the file name; the body starts with the overview |
| `---` rules | Separating sections with horizontal rules | One blank line between sections |
| Comments explaining syntax | `x = 5  # 定义变量x` | Only comment key logic and the "why" |
| Lecturing tone | 「首先我们来了解一下…」 | Note-like declarative tone |
| Install steps without verification | Not telling readers how to confirm success | Attach `xxx --version` style checks to every step |
| Single-platform only | Writing `/usr/local/` in a Windows tutorial | Split by OS, or declare the target platform up front |
| Full-blown code from the start | First example already has error handling and type annotations | Start with the simplest version, add complexity gradually |
| Only the happy path | No troubleshooting for common failures | Follow error-prone steps with error messages and fixes |

## Self-Check Checklist

After generating the article, check it item by item:

- [ ] **Readable from zero**: a beginner can read start to finish and follow every step without getting stuck anywhere
- [ ] Uses「笔者」as the self-reference
- [ ] Title is 10-30 characters, no clickbait, no version-number stuffing
- [ ] 2-5 emojis, naturally distributed
- [ ] 0-2 metaphors, precise and not exaggerated
- [ ] Every install step has a verification command, split by OS
- [ ] OS explicitly labeled wherever commands/paths are involved
- [ ] Code evolves from simple to complex, not full-blown from the start
- [ ] Error-prone steps are followed by common errors and solutions
- [ ] Inline code vs code blocks used correctly (copyable → code block; name-only → inline code)
- [ ] All code blocks have a language tag (```python, not bare ```)
- [ ] Code comment format correct: `code  # comment` (space + symbol + space)
- [ ] No neatly aligned code comments
- [ ] Every knowledge point is followed by a code example, with run results shown
- [ ] API/parameter/function lists use tables first
- [ ] Technical terms explained clearly in plain language on first appearance
- [ ] External references attributed
- [ ] Screenshots annotated with alt text, no bare screenshots
- [ ] Environment versions and writing date stated at the top
- [ ] Companion repo link and notes complete, if one exists
- [ ] No behaviors from the "AI-Flavor Removal Checklist"
- [ ] No `---` horizontal rules in the article
- [ ] Body doesn't start with `# Title`; H1 is used only for section headings
- [ ] Ends right after the last knowledge point—no summary, no pleasantries
- [ ] The file name is the article title
- [ ] **Code verified**: all executable code in the article has actually been run, with results matching the article
- [ ] **Final test**: after reading, can a beginner independently complete a real task in this domain?
