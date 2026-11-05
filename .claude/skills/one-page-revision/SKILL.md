---
name: one-page-revision
description: Turns a chapter (PDF, Markdown or text notes) into a one-page A4 revision sheet of about 450 words max, saved to revision-sheets/<chapter-name>-revision.md. Use when the user asks for a revision sheet, a one-page summary, quick revision notes, a cheat sheet or last-minute revision of a chapter or set of notes.
argument-hint: <chapter file>
allowed-tools: Read, Write, Bash, Glob
---

# One-Page Revision

Create a single-page revision sheet from one chapter file. Argument: `$ARGUMENTS` (path to a `.pdf`, `.md` or `.txt` file).

## Steps

1. **Resolve the input.** If no path is given, or the file does not exist, ask the user for it (use Glob to suggest nearby `.pdf`/`.md`/`.txt` files). Do not guess.
2. **Read the chapter.**
   - `.md` / `.txt`: read directly with Read.
   - `.pdf`: try Read first. If it fails or returns no usable text, extract with Python:
     ```
     python -c "import sys,pypdf; r=pypdf.PdfReader(sys.argv[1]); print('\n\n'.join((p.extract_text() or '') for p in r.pages))" "<file.pdf>"
     ```
     If `pypdf` is missing, run `pip install pypdf` once and retry. If the text is still empty (scanned images), tell the user the PDF has no text layer and stop; do not invent content.
3. **Pick the sheet name.** `<chapter-name>` = input filename without extension, lowercased, spaces replaced with hyphens. Output path: `revision-sheets/<chapter-name>-revision.md` in the current folder. Create the folder if needed. Overwrite an existing sheet of the same name.
4. **Write the sheet** using the template below.
5. **Check the length.** Count words (e.g. `python -c "import sys;print(len(open(sys.argv[1],encoding='utf-8').read().split()))" <file>`). If above 450, cut the least important items and re-check. Fits one A4 page means no tables wider than the page and no long paragraphs.
6. **Report** the output path, the word count, and any section left out because the chapter had no such content.

## Template

```
# <Chapter title> - Revision Sheet

## Key ideas
- (5-7 short bullets, one line each)

## Key formulas
- `formula` - symbol = meaning (units if the notes give them)

## Must-know definitions
- **Term**: one-line definition

## Common mistakes / exam traps
- (short bullets)

## Self-check (answer without looking)
1. ...
2. ...
3. ...
4. ...
5. ...

## Answers
1. ... 2. ... 3. ... 4. ... 5. ...
```

## Rules

- **Stay faithful.** Use only what is in the chapter. Do not add topics, formulas, examples or facts from outside knowledge, even if they are correct and related. Keep the chapter's own wording for definitions and symbols.
- **Mistakes and traps** must come from warnings, notes or worked examples in the chapter, or be a direct misreading of something it states (for example mixing up two terms it defines). Do not invent unrelated pitfalls.
- **No formulas in the chapter?** Keep the heading and write "None in this chapter." Same for definitions or traps. Do not pad.
- **Self-check questions**: exactly 5, each answerable from the chapter, mixing recall and one application question where possible. Answers go at the bottom, short.
- **Length**: about 450 words maximum for the whole file. Prefer fragments over sentences.
- Do not modify the input file. Write only inside `revision-sheets/`.
