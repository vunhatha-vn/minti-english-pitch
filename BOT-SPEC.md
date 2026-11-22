# Minti Exam Ops — bot specification

## Mission

Turn source exam papers into a validated, school-tagged question bank that Minti English can ship without inventing content.

## Inputs

- A watched folder with PDFs or photos of past papers.
- The content schema and the 11-question-type taxonomy.
- The target school and exam-year list.
- The existing question bank, for duplicate detection and coverage gaps.

## Nightly loop

1. **Ingest** — pick the oldest unprocessed paper from the queue.
2. **Extract** — OCR and segment the paper into individual questions and answer choices.
3. **Classify** — assign one of the 11 question types.
4. **Tag** — school, year, difficulty, source page, and source image crop.
5. **Verify** — solve each question independently, compare with the printed answer, and assign a confidence score.
6. **Validate** — run schema validation, duplicate detection, and coverage checks.
7. **Open a PR** — structured JSON plus source citations and a review queue.
8. **Report** — post the 07:00 digest with yield, gaps, and flagged items.

## Confidence policy

- `>= 0.90` and schema-valid: eligible for auto-merge.
- `0.70–0.89`: open a PR and put the item in the human review queue.
- `< 0.70`: do not ship; attach the source crop and a one-line reason.

## Weekly loop

- Build a school-specific mock with balanced coverage across question types and difficulty.
- Open it as a draft PR.
- Report coverage against the target school list and the next content batch.

## Pull request format

Every content PR includes:

- a one-line summary of the paper
- question count by type
- source citations for every question
- the review queue with reasons
- coverage delta by school and type
- validation results
- a rollback note: revert the PR to remove the batch

## Guardrails

- Every question cites a source page and image crop.
- No invented questions, answers, schools, years, or explanations.
- No student data or PII in the pipeline, logs, or PRs.
- No answer changes without human review.
- No auto-merge below the confidence threshold.
- Max 60 questions per run; daily budget cap; kill switch.
- If OCR or segmentation is ambiguous, stop that question and flag it.

## Success metrics

- Validated questions per paper.
- Auto-approval rate at the confidence threshold.
- Human review minutes per flagged question.
- Duplicate rate.
- Coverage by school, year, and question type.
- Zero unsourced questions and zero PII incidents.
