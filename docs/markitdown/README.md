# 📄 MarkItDown

> *Most reasoning starts with text — but the information you need often arrives locked inside a PDF, a deck, or a spreadsheet. This is the bridge.*

---

## What this category is

MarkItDown wraps [Microsoft MarkItDown](https://github.com/microsoft/markitdown), a lightweight utility that converts documents and files into clean, LLM-ready Markdown. Unlike the thinking skills in this toolkit, it is a *tool-use* skill: its job is to faithfully extract content — preserving headings, lists, tables, and links — from formats a language model can't read directly, then hand off to whatever analysis the content calls for.

It supports PDFs, Office documents (Word, PowerPoint, Excel), images (EXIF + OCR), audio (transcription), HTML, YouTube URLs, CSV/JSON/XML, ZIP archives, and EPubs. Optional Azure Document Intelligence support handles complex or scanned layouts, and the Python API can generate LLM descriptions of images.

---

## When to reach for it

- You have a PDF, Word doc, slide deck, or spreadsheet whose content you need as text
- You want to summarize, search, or reason over a document and need clean input first
- You need to extract text from an image (OCR) or transcribe audio
- You want to convert an HTML page, YouTube URL, CSV/JSON/XML, ZIP, or EPub into Markdown
- You want document *structure* preserved — tables as tables, headings as headings

---

## When *not* to reach for it

**Don't use it on content that's already text.** If you have clean Markdown, plain text, or a source/config file you can simply open, read it directly — round-tripping it through a converter adds nothing and risks degrading it.

**Don't expect a visual reproduction.** MarkItDown optimizes for token-efficient *semantic* content for LLMs, not for pixel-perfect layout, fonts, or page geometry. When you need a faithful visual rendering, use a PDF renderer or the original application instead.

The nearest neighbor: [Sensory](../sensory/) — which helps you *observe* what's actually present in material you already have. MarkItDown gets the raw content out of a file; sensory skills help you find the signal once it's in front of you.

---

## Skills in this category

| Skill | What it does | Trigger when... |
|---|---|---|
| [`/markitdown`](README.md) | Converts documents, media, web pages, and data files into clean Markdown using Microsoft MarkItDown | You have a PDF, Office file, image, audio, HTML page, URL, or data file you need as Markdown |

---

## Example

**Input:**
> Convert this quarterly board deck (`Q2-board-deck.pptx`) to markdown so I can summarize it.

**Output:**

---

**Converted:** `Q2-board-deck.pptx` → `Q2-board-deck.md`
**Format:** PowerPoint (.pptx)
**Options used:** None (digital slides, no OCR needed)

**Markdown output:**

```markdown
# Q2 Board Deck

## Agenda
- Revenue review
- Pipeline health
- Hiring plan

## Revenue Review

| Metric | Q1 | Q2 | QoQ |
|--------|-----|-----|------|
| ARR | $4.2M | $5.1M | +21% |
| Net retention | 108% | 112% | +4pts |
| Gross margin | 71% | 73% | +2pts |

## Pipeline Health
- Coverage ratio: 3.4x (target 3.0x)
- Two enterprise deals slipped from Q2 to Q3
...
```

**Fidelity notes:**
- The revenue table converted cleanly. One slide was a screenshot of a chart — its numeric values were *not* extracted (image-only content); the takeaway text beneath it was preserved. Spot-check the chart slide against the original before quoting figures from it.

---

## Related categories

- [Sensory](../sensory/) — for finding the signal in content once it's extracted
- [Investigation](../investigation/) — for auditing the evidence and claims inside the converted document
- [Writing](../writing/) — for turning the extracted material into prose or argument
