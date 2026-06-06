---
name: markitdown
description: "Convert documents and files into clean, LLM-ready Markdown using Microsoft MarkItDown. Use when you say 'convert this to markdown', 'markitdown', 'turn this PDF/Word/Excel/PowerPoint into text', 'extract text from this document', 'read this file as markdown', or when you have a PDF, Office document, image, audio file, HTML page, CSV/JSON/XML, ZIP, EPub, or YouTube URL whose content you need as Markdown for reading, summarizing, or further reasoning."
---

# MarkItDown

Most reasoning starts with text. But the information you need often arrives locked inside a PDF, a slide deck, a spreadsheet, a scanned image, or a web page — formats a language model can't read cleanly. [Microsoft MarkItDown](https://github.com/microsoft/markitdown) is a lightweight utility that converts those formats into Markdown that preserves structure (headings, lists, tables, links) while stripping the binary noise. This skill is the bridge: it gets the content *out* of the file and into a form you can actually think about.

This is a tool-use skill, not a reasoning framework. Its job is to produce faithful Markdown — then hand off to whatever analysis the content calls for.

---

## When to use

- You have a **PDF, Word (.docx), PowerPoint (.pptx), or Excel (.xlsx)** file and need its content as text.
- You need to **extract text from an image** (EXIF metadata + OCR) or **transcribe audio**.
- You want to convert an **HTML page, CSV, JSON, XML, ZIP archive, EPub, or YouTube URL** into Markdown.
- You're about to **summarize, search, or reason over** a document and need clean input first.
- You want **structure preserved** — tables as Markdown tables, headings as headings — not just a flat text dump.

## When NOT to use

- **You already have clean text or Markdown.** Don't round-trip plain text through a converter; just read it.
- **You need a pixel-perfect visual reproduction** (exact layout, fonts, page geometry). MarkItDown optimizes for *semantic* content for LLMs, not for faithful visual rendering — use a PDF renderer or the original application for that.
- **The file is a source-code or config file** you can simply open and read — use the normal file tools, not a converter.

---

## Your Process

**Step 1: Identify the source and format**
Determine what you're converting: a single file path, a directory of files, a URL (HTML page, YouTube), or content piped via stdin. Note the format — it determines which optional dependencies are needed and whether OCR/transcription is involved.

**Step 2: Ensure MarkItDown is installed**
Check first, then install only if missing:

```bash
markitdown --version || pip install 'markitdown[all]'
```

- Requires **Python 3.10+**.
- `markitdown[all]` pulls in every optional dependency. To keep it lean, install only what you need, e.g. `pip install 'markitdown[pdf,docx,pptx,xlsx]'`.
- If `pip` isn't available or installs are restricted, say so and ask how to proceed rather than forcing it.

**Step 3: Choose conversion options**
Match the option to the document:

- **Plain digital documents** (text-based PDFs, Office files) → no extra options needed.
- **Scanned PDFs / images with text** → basic OCR is built in, but for high-fidelity extraction of complex layouts use **Azure Document Intelligence**: `markitdown file.pdf -d -e "<endpoint>"`.
- **Images you want *described*** (not just OCR'd) → use the Python API with an LLM client (see below).
- **Third-party format support** → enable plugins with `--use-plugins`.

**Step 4: Run the conversion**

CLI (best for one-off conversions):

```bash
# Write to a file
markitdown report.pdf -o report.md

# Or capture stdout
markitdown slides.pptx > slides.md

# Or pipe content in
cat data.xlsx | markitdown
```

Python API (best for batch jobs, programmatic handling, or LLM image descriptions):

```python
from markitdown import MarkItDown

md = MarkItDown()                       # add enable_plugins=True to use plugins
result = md.convert("quarterly.xlsx")
print(result.text_content)
```

With LLM-generated image descriptions:

```python
from markitdown import MarkItDown
from openai import OpenAI

md = MarkItDown(llm_client=OpenAI(), llm_model="gpt-4o")
result = md.convert("diagram.png")
print(result.text_content)
```

**Step 5: Verify the output**
Conversion is rarely perfect. Before relying on the result, check:

- **Empty or near-empty output** → likely a scanned/image-only PDF. Re-run with Azure Document Intelligence or OCR.
- **Garbled or merged tables** → complex spreadsheets and multi-column PDFs can lose structure; note it and spot-check against the source.
- **Missing images/diagrams** → images become OCR text or descriptions, not embedded pictures; visual-only information may be lost.
- **Truncation** → very large files may need to be processed in parts.

**Step 6: Hand off**
Save the Markdown if it's a deliverable, or pass it straight into the next step — summarization, search, a thinking skill, or your own analysis. State clearly what was converted and flag any fidelity caveats you found in Step 5.

---

## Supported Formats (reference)

| Category | Formats |
|---|---|
| Documents | PDF, Word (.docx), PowerPoint (.pptx), Excel (.xlsx) |
| Media | Images (EXIF + OCR), audio (transcription) |
| Web | HTML, YouTube URLs |
| Data | CSV, JSON, XML |
| Archives | ZIP, EPub |

---

## Output Format

Report the result concisely:

**Converted:** [source file/URL → output destination]
**Format:** [detected input format]
**Options used:** [plugins / Azure DI / LLM image descriptions / none]

**Markdown output:**
[the converted Markdown, or a path to where it was saved]

**Fidelity notes:**
- [Anything lost or degraded — scanned pages, complex tables, dropped images — or "Clean conversion, no issues observed"]

---

## Notes

- **MarkItDown runs with the privileges of the current process** and reads local files directly — only convert sources you trust, and be mindful when handling sensitive documents.
- It optimizes for **token-efficient, structure-preserving Markdown for LLMs**, not for visual reproduction. Treat the output as faithful *content*, not a faithful *rendering*.
- A clean-looking conversion is not a guarantee of completeness. For anything where accuracy matters (legal, financial, medical), spot-check the Markdown against the original before reasoning over it.

---

## What's Next

After delivering the Markdown, use `AskUserQuestion` to offer the next move:

- **Question:** "Converted to Markdown. What's next?"
- **Header:** "Next"
- **Options:**
  - `/sensory-signal-detection` — Pull the meaningful signal out of the converted content
  - `/writing-argument` — Build an argument from the extracted material
  - `/investigation-evidence-audit` — Assess the quality of evidence in the document
  - **Done** — Hand back the Markdown as-is
