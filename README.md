# Minti English — the content engine for a Hanoi exam-prep product

Public pitch brief for the Poke × Cognition Devin Bots challenge.

## The product

Minti English is a responsive web app for grade-5 students preparing for English entrance exams into Hanoi's high-quality grade-6 schools. It focuses on the real exam scope: Grammar, Vocabulary, and 11 recurring question types — not IELTS, TOEIC, Listening, Speaking, or essay Writing.

The v1.0 build covers the full learning loop:

- placement
- targeted practice
- school-specific mock and past papers
- automatic scoring and error analysis
- progress, streaks, rewards, and a growing character

Stack: Next.js, TypeScript, Prisma, Playwright. 9 golden-path student journeys are covered by E2E tests. The codebase is private; a walkthrough is available on request.

## The bottleneck

The moat is not another practice UI. The moat is a validated, school-tagged question bank across years and question types. Producing it is manual content ops: sourcing papers, segmenting questions, classifying the 11 types, checking answers, tagging school/year/difficulty, and catching duplicates.

That work does not fit into a sprint, and it does not scale with a solo founder.

## The bot: Minti Exam Ops

An always-on Devin Bot that turns source papers into product-ready content.

Every night:

1. Pick up a new paper from a watched folder (PDF or photos).
2. OCR and segment it into individual questions.
3. Classify each question into one of the 11 exam types.
4. Tag school, year, difficulty, and source page.
5. Cross-check the answer with a second pass; assign a confidence score.
6. Validate the structured JSON against the content schema; check duplicates and coverage.
7. Open a PR with the questions, source citations, and a review queue for low-confidence items.
8. Post a 07:00 digest: new questions, coverage gaps by school/type, flagged items.

Weekly:

- assemble a school-specific mock exam with balanced coverage
- ship it as a draft PR
- report coverage against the target school list

## Guardrails

- Every question must cite a source page.
- No invented questions, answers, schools, or exam years.
- Low-confidence items go to a human review queue; they never ship automatically.
- No student data or PII enters the pipeline.
- Schema validation, duplicate detection, and coverage checks run on every PR.
- Daily budget cap, max questions per run, and a kill switch.
- If the source is ambiguous, stop and flag; do not guess.

## 30-day pilot

| Phase | Scope | Success |
|---|---|---|
| Week 1 | Pipeline + 10 papers | 500 validated questions, 1 mock draft |
| Week 2 | 20 papers | 800 validated questions, coverage dashboard |
| Week 3 | 30 papers | 1,200 validated questions, 3 mock exams |
| Week 4 | Final batch + report | 1,500 validated questions, coverage report |

Success metrics:

- 500 validated questions and 1 school-specific mock in week 1.
- 1,500 validated questions and 3 mocks in 30 days.
- <5% flagged as incorrect after review.
- Zero questions without a source citation.
- Zero student PII in any artifact.

## Credit math

`$200 ≈ 30 nightly runs`

Each run can process one paper (~40–60 questions). Thirty papers ≈ 1,200–1,800 questions. At $20–30/hour for manual digitization, that is $600–900 of content work, before counting the compounding value of a proprietary question bank.

## The ask

The full $200 credit tier.

## Commitment

If week 1 does not produce 500 validated questions and one school-specific mock exam, I will return the unused credits and publish a public postmortem explaining which assumption failed.

## Status

- Product: v1.0 built, private repo, 9 E2E journeys.
- Bot: spec complete; ready to wire to a source folder and the content schema.
