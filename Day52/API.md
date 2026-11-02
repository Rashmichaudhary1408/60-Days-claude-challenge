# ShortlistIQ: API Design

Version 1.0 · Capstone Day 2 · Design only, no implementation. Items marked **🔶 PC-n** are proposed changes awaiting approval.

## 1. Overview

ShortlistIQ has **three HTTP endpoints**, all served by Next.js Route Handlers at `src/app/api/<name>/route.js`. Everything else (parsing, rules, scoring, ranking, history, export) happens in the browser, so there are no endpoints for drives, students, files or export. That is deliberate: it keeps student data off the server.

| # | Method and path | Purpose | Used on |
|---|---|---|---|
| 1 | `GET /api/health` | Prove the server can reach Gemini; deployment check | Day 3 setup, troubleshooting |
| 2 | `POST /api/extract-skills` | Extract role title, skills and eligibility hints from a JD | Wizard Step 2 |
| 3 | `POST /api/score-resume` | Return per-skill evidence, experience and explanation for one resume | Wizard Step 4 (once per eligible, readable student) |

## 2. Conventions shared by all endpoints

| Topic | Rule |
|---|---|
| Format | JSON in, JSON out. `Content-Type: application/json` required on POST |
| Authentication | **None** (PRD: no login). Public routes. Compensating controls below |
| Authorization | Not applicable; routes store nothing and read no user data |
| Body size | Maximum about 200 KB (resume text is capped far below this) |
| Rate limit 🔶 PC-3 | 150 requests per 10 minutes per IP, in memory per serverless instance. Enough for a 50-student run with retries; stops casual abuse |
| Timeout | `export const maxDuration = 30` seconds per route |
| Model settings | Temperature 0, JSON mode, response schema, model from `GEMINI_MODEL` |
| Logging | Server logs error codes and durations only; **never** JD or resume text |
| CORS | Not needed (same origin) |
| Idempotency | All calls are safe to retry; they change nothing |

### Error envelope (all non-2xx responses)

```json
{
  "error": "Human-readable message the UI can show",
  "code": "RATE_LIMITED",
  "retryable": true
}
```

🔶 PC-3 adds the string `code`. Codes:

| HTTP | `code` | Meaning | `retryable` | Client behaviour |
|---|---|---|---|---|
| 400 | `INVALID_INPUT` | Missing or out-of-range field | false | Show the message beside the field |
| 413 | `PAYLOAD_TOO_LARGE` | Body above the limit | false | Show message; shorten input |
| 415 | `UNSUPPORTED_MEDIA_TYPE` | Not JSON | false | Developer error; show generic message |
| 429 | `RATE_LIMITED` | Our per-IP limit exceeded | true | Wait and retry; fallback after retries |
| 429 | `AI_RATE_LIMITED` | Gemini free-tier limit | true | Backoff, then fallback or manual skills |
| 502 | `AI_UNAVAILABLE` | Gemini error, bad key, retired model | true | Backoff, then fallback or manual skills |
| 502 | `AI_BAD_OUTPUT` | Output not valid even after repair | true | Retry once; then fallback |
| 504 | `AI_TIMEOUT` | Function time budget exceeded | true | Retry; then fallback |
| 500 | `SERVER_ERROR` | Unexpected bug | false | Generic message; check logs |

---

## 3. `GET /api/health`

| Item | Detail |
|---|---|
| **Purpose** | Confirm the deployment is alive and the Gemini key and model work server-side |
| **Authentication** | None |
| **Request** | No body, no parameters |
| **Behaviour** | Sends one tiny JSON-mode prompt to Gemini ("return ok true and a one-word greeting") |
| **Validation** | None (the rate limiter still applies) |

**Success `200`**

```json
{ "ok": true, "model": "<value of GEMINI_MODEL>", "reply": "hello" }
```

**Errors**

| Case | Status and code | Body |
|---|---|---|
| `GEMINI_API_KEY` or `GEMINI_MODEL` missing | 500 `SERVER_ERROR` | `{ "ok": false, "error": "AI is not configured on the server", "code": "SERVER_ERROR", "retryable": false }` |
| Key invalid or model not found | 502 `AI_UNAVAILABLE` | `ok: false` plus envelope |
| Free-tier limit | 429 `AI_RATE_LIMITED` | envelope |
| Over our rate limit | 429 `RATE_LIMITED` | envelope |

---

## 4. `POST /api/extract-skills`

| Item | Detail |
|---|---|
| **Purpose** | Turn a pasted job description into an editable skills list, a role title and optional eligibility hints (PRD FR-8) |
| **Authentication** | None |

**Request**

```json
{ "jd": "Nimbus Labs - Associate Software Engineer ... (50 to 8000 characters)" }
```

**Validation**

| Field | Rule | Failure |
|---|---|---|
| `jd` | String; after trim 50 to 8000 characters | 400 `INVALID_INPUT` "Job description must be 50 to 8000 characters" |
| Body | Valid JSON object; size under limit | 400 / 413 |
| Extra fields | Ignored | n/a |

**Behaviour:** the prompt marks the JD as untrusted data and asks for up to 20 skills as short canonical names ("React", "Node.js"), tagged `required` for must-haves or core items and `preferred` for "good to have" items, plus eligibility hints only when explicitly stated (otherwise `null`). The server then runs `validateExtraction`: dedupe case-insensitively, trim, cap at 25, coerce unknown importance to `required`, range-check hints (CGPA 0 to 10, backlogs ≥ 0, year 2000 to 2100), uppercase branches.

**Success `200`**

```json
{
  "roleTitle": "Associate Software Engineer",
  "skills": [
    { "name": "JavaScript", "importance": "required" },
    { "name": "TypeScript", "importance": "preferred" }
  ],
  "eligibilityHints": {
    "minCgpa": 7.0,
    "branches": ["CSE", "IT", "ECE"],
    "maxBacklogs": 0,
    "graduationYear": 2027
  }
}
```

Hint fields are `null` when the JD does not state them. `branches` may be `null`.

**Errors**

| Case | Status and code |
|---|---|
| JD too short or too long | 400 `INVALID_INPUT` |
| Not JSON or wrong content type | 415 `UNSUPPORTED_MEDIA_TYPE` |
| Body too large | 413 `PAYLOAD_TOO_LARGE` |
| Gemini rate limit | 429 `AI_RATE_LIMITED` |
| Gemini down, bad key, retired model | 502 `AI_UNAVAILABLE` |
| Output unusable after repair | 502 `AI_BAD_OUTPUT` |
| Time budget exceeded | 504 `AI_TIMEOUT` |

**Client rule:** on any error the officer can still type skills manually (FR-10). The browser applies a 45-second timeout.

---

## 5. `POST /api/score-resume`

| Item | Detail |
|---|---|
| **Purpose** | Judge one resume against the finalized skills and return evidence, experience and a short explanation (FR-17). The numeric score is **not** returned; the browser computes it (FR-18) |
| **Authentication** | None |

**Request**

```json
{
  "roleTitle": "Associate Software Engineer",
  "skills": [
    { "name": "JavaScript", "importance": "required" },
    { "name": "Docker", "importance": "preferred" }
  ],
  "resumeText": "Priya Sharma ... extracted text of one resume"
}
```

**Validation**

| Field | Rule | Failure |
|---|---|---|
| `roleTitle` | String, 1 to 150 characters (trimmed) | 400 |
| `skills` | Array of 1 to 25 items; each `name` 1 to 60 characters; `importance` is `required` or `preferred` | 400 |
| `resumeText` | Non-empty string after trim; **truncated** server-side to 12000 characters (not an error) | 400 if empty |
| Body | Valid JSON; size under limit | 413 / 415 |

**Behaviour:** acts as a careful campus-hiring screener; for **each** listed skill returns `present` and short `evidence`; accepts clear aliases (ReactJS for React, Postgres for SQL) but does not infer from unrelated skills; returns up to 3 relevant projects or internships; a `relevanceRating` from 0 to 5; a neutral explanation of at most about 40 words. The prompt states that resume text is untrusted data and that embedded instructions (including requests for a score) must be ignored. The server then repairs the result.

**Repair rules (server)**
1. Every requested skill appears exactly once; missing ones are added with `present: false`.
2. `present: true` with empty `evidence` becomes `false`.
3. `relevanceRating` is rounded and clamped to 0 to 5.
4. `relevantExperience` is capped at 3 and `type` coerced to `project`, `internship` or `other`.
5. Strings are trimmed and length-capped.

**Success `200`**

```json
{
  "skillResults": [
    { "name": "JavaScript", "present": true, "evidence": "Built a React dashboard in JavaScript" },
    { "name": "Docker", "present": false, "evidence": "" }
  ],
  "relevantExperience": [
    { "title": "Logistics Tracker", "type": "project", "why": "Full-stack React and Node.js app" }
  ],
  "relevanceRating": 4,
  "explanation": "Strong web fundamentals with a full-stack project; no container experience shown."
}
```

**Errors:** same table as `/api/extract-skills`, plus 400 for an empty `resumeText`.

**Client rules (`runner.js`)**
- Retry a `retryable` failure up to 2 more times after waits of 2 s and 4 s, then call `fallbackScore`.
- After 3 consecutive 429s pause 10 s once.
- Concurrency 2; call only for eligible students whose PDF text is at least 150 characters.

---

## 6. Endpoint to requirement map

| Endpoint | Requirements |
|---|---|
| `/api/health` | FR-29 (deployment), setup verification |
| `/api/extract-skills` | FR-7, FR-8, FR-9 (editing is client-side), FR-10 |
| `/api/score-resume` | FR-15, FR-17, FR-19 (fallback on failure), FR-20, FR-21 |

All other functional requirements are served by client-side modules (Section 7).

---

## 7. Client-side module contracts (the "internal API")

These are the functions each day builds. Signatures are fixed so any day's AI helper can continue without redesign.

| Module | Function | Input → Output |
|---|---|---|
| `parseStudents.js` | `parseStudentsFile(file)` | File → `Promise<{ students, errors, warnings }>` |
| | `parseStudentRows(rows)` | array of row objects → `{ students, errors, warnings }` (pure) |
| `matchResumes.js` | `matchResumes(students, files)` | students, File[] → `{ students, unmatchedFiles, rejectedFiles, fileMap }` |
| `eligibility.js` | `defaultRules(students)` | students → `Rules` |
| | `evaluateStudent(student, rules)` | → `{ eligible, failedRules[] }` |
| | `applyRules(students, rules)` | → students with `eligibility` set |
| `skills.js` | `normalizeSkills(list)`, `validateExtraction(raw)` | clean, deduped, capped list; validated extraction |
| `aiClient.js` | `extractSkills(jd)` | → `{ ok: true, data }` or `{ ok: false, error, code, retryable }` |
| | `scoreResume(payload)` | same return convention |
| `pdfText.js` | `extractPdfText(file)` | File → `{ status: "ok"/"unreadable"/"error", text, pages }` |
| `scoring.js` | `computeScore({ skills, skillResults, relevanceRating })` | → `{ score, breakdown }` |
| `fallbackScore.js` | `fallbackScore({ skills, resumeText })` | → `{ score, breakdown, skillResults }` |
| `runner.js` | `runScreening({ drive, resumeFiles, onProgress, signal })` | → `Promise<Drive>` (completed) |
| `shortlist.js` | `rankStudents`, `getAutoShortlistIds`, `getFinalShortlistIds`, `getStudentState` | pure ranking and override logic |
| `storage.js` | `saveDrive`, `getDrive`, `listDrives`, `deleteDrive` | each returns `{ ok, ... }`; never throws |
| `exportXlsx.js` | `buildWorkbook(drive)`, `exportDriveToXlsx(drive)` | workbook (pure); file download |
| 🔶 PC-2 `server/gemini.js` | `generateJson({ prompt, schema, temperature })` | → parsed object; throws error with `status`, `code`, `retryable` |
| 🔶 PC-2 `server/apiGuard.js` | `guardRequest(request)` | → `{ ok: true, body }` or `{ ok: false, response }` (size, type, rate limit) |
| 🔶 PC-2 `server/prompts.js` | `extractSkillsPrompt(jd)`, `scoreResumePrompt(...)` | prompt strings and response schemas |
