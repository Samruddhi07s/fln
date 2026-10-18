# FLN Onboarding Document — Ravi Bhatt

## 1. What is FLN?

FLN stands for Foundational Literacy and Numeracy. It refers to the basic reading, writing, language, and mathematical skills that children develop during their early years of education.

These skills are essential because they provide the foundation for future learning. If children struggle with basic concepts, they may find it difficult to understand more advanced topics.

A digital FLN platform can help teachers assess students, identify learning gaps, provide suitable practice activities, and track their progress. The goal is to make foundational learning more accessible, structured, and effective.

## 2. What do you understand by FLN (as a system)?

I understand FLN as a system that connects students, teachers, learning content, assessments, and progress tracking.

The system can follow a continuous learning cycle:

1. Assess the student's current understanding.
2. Identify the concepts where the student needs improvement.
3. Provide appropriate questions and learning activities.
4. Record the student's responses or teacher observations.
5. Evaluate progress and plan further learning activities.

An effective FLN system should support different learning levels and assessment methods. Some skills can be assessed through written answers, while others require teachers to observe a child's performance.

Question quality, correct assessment modes, and reliable progress data are important for ensuring that the system provides meaningful educational support.

## 3. Current State of the Repository — What Has Been Done So Far

During onboarding, I started exploring the repository structure and understanding how the backend operates.

The initial files I inspected include:

- `backend/src/index.ts`
- `backend/src/db.ts`
- `backend/src/config/environment.ts`

I attempted to run the backend locally and investigated a MongoDB connection problem. During this process, I observed that the backend could fall back to file-based storage when the remote database connection failed.

I also reviewed issues related to Balvatika question generation, question-bank imports, and Hindi text rendering in worksheet PDFs.

These initial explorations helped me identify important areas for further investigation, including question templates, assessment modes, question generation, and PDF generation. I am continuing to trace the relevant code and tests to understand their current implementation.

## 4. Gaps Observed in the Code

The following gaps are reported in the issues I reviewed and need to be verified against the current implementation.

### A. Question Generation for Balvatika Levels

**Related issue:** [#760](https://github.com/vicharanashala/fln/issues/760)

The issue reports that question generation needs to support ten questions per Balvatika level and avoid placeholder or repeated questions.

A fixed question count can limit flexibility, while placeholder questions and duplicates can reduce assessment quality.

**Proposed direction:** Inspect the question generator and its callers, make the question count configurable where appropriate, validate generated content, and add tests for supported levels and missing templates.

### B. Hindi Text in Worksheet PDFs

**Related issue:** [#757](https://github.com/vicharanashala/fln/issues/757)

The issue concerns Hindi text not rendering correctly in worksheet PDFs. This may involve font support, Unicode handling, or PDF text rendering.

**Proposed direction:** Inspect the PDF-generation implementation and its font configuration, reproduce the problem with Hindi text, and add regression coverage after confirming the cause. The related [PR #830](https://github.com/vicharanashala/fln/pull/830) should also be reviewed before starting work.

### C. Balvatika Question-Bank Import

**Related issue:** [#761](https://github.com/vicharanashala/fln/issues/761)

The issue reports problems with assessment-mode handling during bulk imports and duplicated or incomplete question-bank content.

If assessment modes are not preserved, questions may be used in an unsuitable assessment format. Incomplete or duplicated questions can also affect the quality of generated assessments.

**Proposed direction:** Review the import route, existing template validation, and seed data. Ensure that supported assessment modes are validated and preserved, and that changes to question-bank content are tested and reviewed.

## 5. Ideas for the Project

Based on the reported issues, I propose the following improvements:

### A. Reliable Question Generation

Make question generation predictable by respecting the requested count, avoiding invalid placeholder content, detecting duplicates, and handling missing templates clearly. Add tests to verify behavior across supported Balvatika levels.

### B. Improved Multilingual PDF Generation

Investigate Hindi font support and text rendering in worksheet PDFs. Add a reproducible test or sample worksheet to verify that Devanagari text displays correctly without breaking existing PDF generation.

### C. Better Question-Bank Validation

Improve bulk-import validation so that assessment modes and required fields are preserved. Validate imported records and provide useful errors for invalid data.

### D. Safer Data Seeding and Testing

Follow the repository's existing seeding conventions and use a dry-run process where supported or approved. Add tests for imports, question generation, and other affected behavior before submitting changes.

These ideas should be refined after inspecting the current source code and discussing dependencies or content-approval decisions with the maintainers.

## 6. Your Contribution

During my initial onboarding, I have:

- Explored the local FLN repository.
- Inspected the backend entry point, database configuration, and environment configuration.
- Attempted to run the backend locally and investigated the MongoDB connection issue.
- Reviewed the descriptions of issues #760, #757, and #761.
- Identified relevant areas of the codebase that require further investigation.
- Started understanding the relationship between question templates, assessment modes, question generation, and worksheet rendering.

I have not yet completed a code fix for these issues. My next step is to verify the reported gaps against the current implementation, review related pull requests and tests, and obtain mentor feedback before proceeding with code contributions.

I aim to make focused, tested, and issue-linked contributions while following the repository's conventions and considering the educational purpose of the platform.