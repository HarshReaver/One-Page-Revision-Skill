# one-page-revision

A Claude Code skill that turns a chapter (PDF, Markdown or text notes) into a one-page A4 revision sheet of about 450 words max.

The sheet contains: 5-7 key ideas, key formulas with symbol meanings, must-know definitions, common mistakes / exam traps, and 5 self-check questions with answers at the bottom. It uses only what is in the chapter and adds no outside topics. Unreadable PDFs are extracted with Python (`pypdf`).

## Install

Copy the `one-page-revision` folder into either:

- a project: `<project>/.claude/skills/one-page-revision/`
- all projects: `~/.claude/skills/one-page-revision/`

PDF fallback needs `pip install pypdf` (the skill will install it if missing).

## Run

```
/one-page-revision path/to/chapter.pdf
```

Output: `revision-sheets/<chapter-name>-revision.md` in the current folder. It also triggers from plain requests such as "make a revision sheet for this chapter" or "quick revision notes of chapter 3".

## Done when

- [x] It starts correctly in a fresh session (the skill is listed and `/one-page-revision <file>` runs without extra setup).
- [x] It works well on 3 different inputs (for example a PDF, a Markdown file and a text file): each sheet is at most about 450 words, has all sections, and contains nothing outside the chapter.
- [x] The same task without the skill is compared, and what got better is shown (for example length control, fixed structure, faithfulness, 5 questions with answers).

## Test results

Tested in a fresh Claude Code session opened in this folder. The skill was listed at startup and ran on 3 chapters from my AIML notes (all PDFs):

| Chapter | Sheet | Words |
|---|---|---|
| Logistic Regression | `revision-sheets/15.-logistic-regression--revision.md` | 420 |
| KNN | `revision-sheets/17.-knn---k-nearest-neighbors-revision.md` | 388 |
| SVM Kernels | `revision-sheets/18.-svm-kernels-revision.md` | 325 |

## With vs without the skill

Same chapter (Logistic Regression), same agent. Without the skill I only asked "make a revision sheet of this chapter" (`examples/without-skill/logistic-regression.md`, 417 words).

What got better with the skill:

1. **Active recall.** The skill adds 5 self-check questions with answers at the bottom. The plain version has none, so it is only for re-reading.
2. **Exam traps.** The skill has a "Common mistakes / exam traps" section (MSE is non-convex, multinomial vs ordinal, a confident wrong prediction gives a very high loss). The plain version mixes these into the text.
3. **Same layout every time.** All 3 sheets have the same sections in the same order and stay under 450 words, so they print as one page each. The plain version picked its own layout (a table, a full chain-rule derivation) that would change from chapter to chapter.

What the plain version did better: it kept the full gradient derivation, which is useful for a long answer question.
