# Partnership Accounts — Quiz Hub

A static, GitHub Pages-friendly quiz site — same pattern as the Principles of
Management and Fundamentals of Management sites. Name-based login, per-module
MCQ quizzes, a shared leaderboard, a full review of wrong answers at the end
of every attempt, and a standalone **Read** page for every module's notes
(sidebar index + prev/next navigation, mobile-friendly).

## Status

- **Quizzes — real content.** All 5 modules (200 questions total) are
  written from your syllabus and ready to use.
- **Reading material — still placeholder.** `reads/*.json` holds dummy
  sections until you send the Word documents with your module notes; see
  "Replacing the reading material" below.

## What's included

```
index.html          Home page — quiz list + reading-material list
quiz.html             Quiz runner (?id=<quiz-id>)
read.html             Standalone reading page (?id=<module-id>) — TOC + prev/next
leaderboard.html       Standalone leaderboard view (?id=<quiz-id>)
css/style.css          Shared styling (includes the read-page layout)
js/app.js              Login, header, leaderboard read/write
js/quiz-engine.js      Quiz rendering, scoring, review screen
js/read-engine.js      Reading page: TOC, active-section highlighting, prev/next
js/firebase-config.js  Firebase keys (same project as the other two sites)
quizzes/manifest.json  List of published quizzes
quizzes/*.json          One quiz per module — real questions, 200 total
reads/manifest.json    List of published reading modules
reads/*.json            One placeholder reading module per module (4 dummy sections each)
firestore.rules.txt    Security rules (same rules as the other two sites)
```

## 1. Publish it on GitHub Pages

1. Create a new repo, e.g. `learnwithrk/Partnership-Accounts`, and push every
   file above into it (keep the folder structure).
2. In the repo: **Settings → Pages → Source → Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
3. Your site will be live at:
   `https://learnwithrk.github.io/Partnership-Accounts/`

## 2. Leaderboard (Firebase)

`js/firebase-config.js` points at the same Firebase project already used by
the Fundamentals of Management and Principles of Management sites
(`quiz-hub-836f8`), and `firestore.rules.txt` is unchanged. Scores are
namespaced by `quizId`, so all three sites can safely share one Firebase
project. Don't edit the Firestore rules in only one repo — they're shared.

## 3. The 5 modules

| # | Module | Questions | Covers |
|---|--------|-----------|--------|
| I | Admission of a Partner | 45 | New & sacrificing ratio, revaluation, goodwill, capital adjustment, AS 10, AS 26, Ind AS 38 |
| II | Retirement of Partners | 40 | New & gaining ratio, revaluation, goodwill, settlement of dues, admission cum retirement |
| III | Death of Partners and Sale of Partnership Firm | 40 | Mode of payment, deceased partner's share of profit, Joint Life Policy, sale of firm to a company |
| IV | Dissolution | 40 | Dissolution of partnership vs. of the firm, modes of dissolution, settlement of accounts (Sec. 48), accounting entries |
| V | Insolvency of Partners | 35 | Garner vs Murray, insolvency of all partners, piecemeal distribution, proportionate capital method, maximum loss method |

Every source question in the original question bank had its correct answer
listed as the same option, so the options have been shuffled (each module
reshuffled with its own fixed seed) before being saved — the `answer` index
in each JSON file reflects the shuffled order, not the original.

## 4. Replacing the reading material

Open `reads/<module-id>.json` and replace the `sections` array. Each section
is one page of the Read view:
```json
{ "id": "s1", "heading": "Section title", "html": "<p>Paragraph…</p>" }
```
`html` accepts basic HTML — paragraphs, `<strong>`/`<em>`, lists, and
`<table>` (already styled). Update `sectionCount` in `reads/manifest.json`
to match the new number of sections. Send me the Word documents and I'll
convert them into this format directly.

## 5. Editing or extending a quiz

Open `quizzes/<module-id>.json` and edit the `questions` array. Each
question:
```json
{ "q": "Question text?", "options": ["A","B","C","D"], "answer": 0 }
```
`answer` is the zero-based index of the correct option. Update
`questionCount` in `quizzes/manifest.json` to match.
