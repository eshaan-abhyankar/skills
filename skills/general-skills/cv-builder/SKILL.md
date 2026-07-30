---
name: cv-ats-tailor
description: Tailor a CV to a specific job description using the user's own 7-step recruiter-style workflow — JD extraction, full CV rewrite, bullet-level rewrite, role-fit matrix, gap analysis + summary realignment, hiring-manager verdict, and full application pack. Use this whenever the user pastes a job description alongside their CV (or references an uploaded CV) and asks to tailor, rewrite, score, check ATS-friendliness, build a role-fit matrix, get a hiring-manager verdict, or build an application pack. Always use this instead of an ad-hoc rewrite — it knows which of the 7 steps to run and applies the user's fixed formatting rules automatically.
---

# CV / JD Tailoring Skill

The user has a tested 7-step workflow for tailoring CVs to job descriptions. This skill routes requests to the right step(s) rather than always running everything. Read `references/steps.md` for the exact content/structure of each step — follow it closely, it's the user's own tested prompt language.

## Step index

1. JD Extraction (recruiter lens, structured table)
2. Full CV Rewrite
3. Bullet-Level Rewrite (action + task + result)
4. Role-Fit Matrix
5. Gap Analysis + Summary Realignment
6. Hiring Manager Verdict (shortlist/maybe/reject)
7. Full Application Pack (CV summary, skills, cover letter, recruiter DM, follow-up email)

## Routing logic — decide which step(s) to run

**Specific ask** ("give me a role-fit matrix", "just rewrite these bullets for the PM role", "give me the hiring manager verdict") → run only that step. Use whatever CV/JD/prior output is already in the conversation; don't ask the user to re-paste something already provided, and don't re-run earlier steps unless their output is actually needed as input and missing.

**Explicit "full pack" / "everything" / "all of it"** → run all 7 in order (1→7), each output presented separately, in sequence.

**Generic ask** ("tailor my CV to this JD", "check my CV against this job", pastes both CV and JD without specifying a step) → this is the common case. Default to the core chain, in order:
- Step 1 (JD extraction) — gives shared context for everything after
- Step 2 (full rewrite)
- Step 5 (gap analysis + summary realignment) — sanity-checks the rewrite
- Step 6 (hiring manager verdict) — honest final check

This is 4 of the 7 steps, not all 7 — it's the bundle that answers "tailor this for me" without also generating a role-fit matrix, bullet-only rewrite, or full application pack the user didn't ask for. Mention at the end that the role-fit matrix, bullet-level rewrite, and full application pack (cover letter, DM, follow-up email) are available if wanted — don't generate them unprompted in the generic case.

If genuinely unsure which case applies, ask which step(s) rather than guessing — but the three cases above should cover most real phrasing.

## Applies to every step

Read `references/formatting-rules.md` before producing any CV text (Steps 2, 3, 5, 7) — these are fixed defaults (no em dashes, black text only, right-aligned dates, title conventions, no Storybook mentions). Apply without asking.

Read `references/ats-checklist.md` for Steps 1, 2, and 5 — parsing-safe formatting and keyword-matching mechanics.

**Never invent experience, skills, or metrics** the user hasn't evidenced, in any step. If a JD requirement isn't supported, surface it as a gap (Steps 1, 4, 5, 6) rather than papering over it in the rewrite.

## File exports

When a step produces a CV or cover letter the user will actually use (Steps 2, 3, 5's summary, 7's CV summary and cover letter), also offer or produce file exports:
- **`.docx` by default** — read `/mnt/skills/public/docx/SKILL.md` and follow it (docx-js). Apply formatting rules as real document formatting (correct text colors including the grey exception, actual right-tab alignment), not visual approximation. Font: Calibri, Arial, or Times New Roman only, 10–12pt body text. Single column, no headers/footers, no tables-as-layout, no images/icons/text boxes.
- **PDF only if the user specifically asks for one**, or the JD/posting specifically requires it — per `references/ats-checklist.md`, PDF is not the default because plain `.docx` is the safer ATS upload format. If producing one, convert from the `.docx` via the docx skill's `soffice.py --headless --convert-to pdf`, and actually look at the rendered pages as a QA pass.
- Plain text is always fine as a quick working draft alongside the docx.

**File naming**: name the docx `FirstName_LastName_JobTitle_Company_CV.docx`, using the actual role title and company from the JD — not a generic name.

Save to `/mnt/user-data/outputs/` and use `present_files`. For steps that are analysis-only (1, 4, 6 verdict/analysis portion) or short-form (recruiter DM, follow-up email in Step 7), plain chat text is enough — don't manufacture files for a two-paragraph DM.

## Presentation order within any run

Analysis/diagnostic output (Steps 1, 4, 5's gap list, 6) is chat text, shown before any rewritten material. Rewritten deliverables (Steps 2, 3, 5's summary, 7) follow, with files via `present_files` after the user can see what changed and why.
