# ATS Parsing Checklist

Two separate things matter for "ATS friendly": (1) the document parses cleanly into text, (2) the text contains the right keywords in a form the parser and a human reviewer both recognize. Check both.

Formatting rules below are adapted from a table shared by [Mohini Goyal (@Mohiniuni)](https://x.com/Mohiniuni) on X.

## Parsing-safe formatting

**Do:**
- **File format**: `.docx` by default. Only produce a PDF if the user specifically asks for one, or the job posting specifically requires it.
- **Font**: Calibri, Arial, or Times New Roman.
- **Font size**: 10–12pt for body text.
- **Layout**: single column only.
- **Margins**: standard 1 inch / 2.54cm.
- **Bullet points**: standard round bullets (•) — never custom glyphs, icons, or emoji as bullets.
- **Section headers**: clear, conventional labels — "Experience", "Education", "Skills" (or fully capitalized equivalents). Avoid cute or nonstandard renamings ("My Journey", "What I Bring").
- **Contact info**: plain text at the top of the document body, not inside a header/footer.
- **File naming**: `FirstName_LastName_JobTitle_Company_CV.docx` — tailor the filename to the specific role/company being applied to, not a generic "CV_final_v3".

**Don't:**
- **Headers/footers**: don't put any content there — many ATS parsers skip it entirely, including contact info.
- **Images, logos, photos**: ATS can't parse images; anything conveyed only visually is invisible to the parser.
- **Tables or columns**: breaks parsing order — use tab stops (e.g. a right-aligned date via positional tab), not table cells, for role/date/location lines.
- **Fancy templates**: Canva-style visual templates commonly fail ATS parsing even when they look polished.
- **Icons or infographics**: not readable by ATS, same failure mode as images.
- **Unusual fonts**: may not render or extract correctly.
- **Text boxes**: content inside a text box can be skipped entirely by the parser.
- **Hyperlink-only text**: if a link is included (portfolio, LinkedIn), also include the full URL or plain text version — don't rely solely on a hyperlinked word like "here".
- **Special characters**: may not parse correctly across ATS systems; keep to standard characters and punctuation (this also lines up with the no-em-dash rule in formatting-rules.md).

## Keyword matching

- Match the JD's actual phrasing where truthful, not just a synonym. If the JD says "cross-functional collaboration" and the CV says "worked with other teams," align the phrasing — ATS keyword matching is often literal.
- Include both the acronym and the expanded form at least once if the JD uses one (e.g. "user experience (UX)") so both search patterns hit.
- Mirror the JD's required skills section in the CV's own Skills section using the same terms, in addition to showing them in context within bullets — parsers commonly weight a dedicated skills list highly.
- Don't keyword-stuff invisibly (white text, hidden repetition) — modern ATS systems and human reviewers both penalize this, and it's excluded here on principle, not just risk.

## Gap analysis specifics

When scoring match %, weight it by:
- **Must-have requirements** (usually stated explicitly, e.g. "5+ years," a specific tool) — missing these matters most
- **Nice-to-haves** — missing these is a minor gap, note but don't over-flag
- Don't conflate "not mentioned in CV" with "candidate doesn't have it" — ask the user if unsure before assuming a gap is real, rather than reporting a false negative as a hard gap.

