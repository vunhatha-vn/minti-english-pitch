# Pilot metrics

## Primary

- **Week 1:** 500 validated questions and 1 school-specific mock draft.
- **30 days:** 1,500 validated questions and 3 mock exams.
- **Review error rate:** below 5% after human review.
- **Source coverage:** 100% of questions cite a source page.

## Secondary

- Validated questions per paper.
- Auto-approval rate at the confidence threshold.
- Human review minutes per flagged question.
- Duplicate rate.
- Coverage by school, year, and question type.

## Guardrails

- Zero student PII in any artifact.
- Zero auto-merges below the confidence threshold.
- Zero questions without a source citation.
- Zero invented schools, years, or answer explanations.

## Reporting

Every nightly run writes a JSON record with:

- paper ID and source
- questions extracted
- questions validated
- auto-approved vs. flagged
- duplicate count
- coverage delta
- minutes of Devin compute used

The 30-day report aggregates these records and compares the result against the primary metrics.
