## Prompt 1 - build

In the folder C:\Users\admin\Documents\Harsh Vanguard\Vscode\28. BSERC AI Projects\16-One-Page-Revision-Skill, create an agent skill called one-page-revision for Claude Code, at .claude/skills/one-page-revision/SKILL.md.

What it should do: I run /one-page-revision <chapter file> (a PDF, Markdown or text notes file). It reads the chapter and writes a revision sheet that fits on one A4 page (about 450 words max), saved as revision-sheets/<chapter-name>-revision.md in the current folder. The sheet has: the 5-7 key ideas as short bullets, the key formulas with what each symbol means, must-know definitions, common mistakes or exam traps, and 5 quick self-check questions with the answers at the bottom. It must stay faithful to the notes and not add topics that aren't in the chapter. If a PDF can't be read directly, it should extract the text with Python (pypdf).

Write the description so it triggers when I ask for a revision sheet, a one-page summary or quick revision notes of a chapter.

Add a short README.md: what the skill does, how to install it (copy the folder into a project's .claude/skills or into ~/.claude/skills), how to run it, and the 'Done when' list: it starts correctly in a fresh session; it works well on 3 different inputs; the same task without the skill is compared and what got better is shown. Don't run git commands. First save this message word for word in prompts.md under '## Prompt 1 - build'. When you're done, reply with the file list.

## Prompt 2 - without the skill (separate agent, no skill loaded)

Make a revision sheet of this chapter: C:\Users\admin\Documents\Harsh Vanguard\AIML Notes\15. Logistic Regression .pdf

Save it as C:\Users\admin\Documents\Harsh Vanguard\Vscode\28. BSERC AI Projects\16-One-Page-Revision-Skill\examples\without-skill\logistic-regression.md. Don't run git. Reply with just the file path and its word count.

## Prompt 3 - with the skill (fresh session opened in this folder)

/one-page-revision "C:\Users\admin\Documents\Harsh Vanguard\AIML Notes\15. Logistic Regression .pdf"

After that sheet is done, run the same skill on these two chapters, one at a time:
- "C:\Users\admin\Documents\Harsh Vanguard\AIML Notes\17. KNN - K Nearest Neighbors.pdf"
- "C:\Users\admin\Documents\Harsh Vanguard\AIML Notes\18. SVM Kernels.pdf"

Don't run git. At the end, reply with the 3 output paths, their word counts, and whether the one-page-revision skill loaded on its own.
