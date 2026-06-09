---
name: exam-creator
description: Create an exam PDF (LaTeX) plus solutions using only provided context unless the user permits internal knowledge.
license: MIT
---

## Exam Creator — Skill Definition
This skill generates a complete exam in LaTeX, compiles it to PDF, and returns the PDF to the user. The generated document must include the exam questions, an optional attachment (if requested), and a solutions section appended at the end.

## Required Output
- A `.tex` source file that compiles cleanly with common LaTeX engines (pdfLaTeX or LuaLaTeX).
- A compiled `PDF` of the exam.
- If requested, any attachments included in the PDF and a solutions section at the end.

## File Structure and Contents
The produced exam PDF must contain, at minimum:
- **Title page:** subject name, date/term (if provided), and a table listing tasks with available points and empty fields for awarded points.
- **Instructions:** exam duration, allowed materials, and grading rules (if provided by the user).
- **Questions:** clearly numbered tasks, with optional sub-parts and point values.
- **Attachments (optional):** any user-provided attachments inserted after the questions.
- **Solutions:** a solutions section after all questions and attachments. Solutions must reference the question numbers and clearly indicate final answers and short supporting steps.

## Knowledge & Context Policy (Important)
- You MUST NOT use internal or external knowledge to invent content unless the user explicitly permits it. Always prefer files and context the user provides.
- If no relevant context files are provided, ask the user to either upload lecture material, example exams, or explicitly permit using internal knowledge.

## Workflow / Interaction Rules
1. Validate input: confirm the subject, target audience (e.g., course level), exam length, point distribution, allowed materials, and whether the user uploaded any reference files or old exams.
2. If the user provided reference exams or lecture materials, analyze them to infer structure and question style, then propose a draft structure to the user for approval before generating the full exam.
3. After user approval, generate the LaTeX source, compile to PDF, and return both the `.tex` and the compiled PDF.
4. If compilation fails, return the `.tex` plus the compilation log and a short list of required packages or fixes.

## LaTeX Requirements and Recommendations
- Use a minimal, portable set of packages (e.g., `geometry`, `babel`/`polyglossia`, `amsmath`, `amssymb`, `graphicx`, `hyperref`) unless the user requests otherwise.
- Keep the document class generic (e.g., `article` or a simple custom exam class) and avoid system-specific fonts.
- Provide well-formed input metadata so compilation is reproducible.

## Input Format (from user)
- Required: `subject` (string) and `exam_type` or `level` (e.g., "midterm", "final", "exercise sheet").
- Preferred: `duration`, `total_points`, `point_breakdown` (list), `allowed_materials`, `attachments` (files), `reference_exams` (files), `lecture_notes` (files), and any explicit instructions about difficulty or learning outcomes.

## Examples (user prompts)
- "Create a 90-minute midterm for Calculus I. I uploaded lecture slides and last year's exam. Use their style and provide full solutions." 
- "Make a 60-minute programming exam (intro level). Allow one cheat sheet. Use only the attached lecture notes; do not invent questions."

## Error Handling
- If required input is missing, ask a concise clarifying question listing only the missing items.
- If a provided file is unreadable or cannot be parsed, report which file and why (e.g., binary, unsupported format).

## Security & Privacy
- Only use user-provided files. Do not exfiltrate or send content to external services.

## Validation & Testing
- After generation, compile the LaTeX file to ensure the PDF builds without errors. If errors occur, include the `.log` and minimal guidance to fix package or syntax issues.
