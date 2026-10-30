# Day 49: Personal AI Playbook

A personalized, single-file AI prompt toolkit for software developers. Instead of rewriting the same prompts, you keep reusable workflows, fill in a few blanks, and copy the result into any AI chat.

![Poster](poster.png)

## What it is

The Personal AI Playbook is one HTML file (`personal-ai-playbook.html`) built with plain HTML, CSS and JavaScript. It has no libraries, no accounts and no network calls, so it works offline. Your data stays in your browser's local storage.

## How it was made

Claude interviewed me one question at a time, then generated the app around my answers.

| Question | My answer |
|---|---|
| Role | Software developer / engineer |
| Main AI uses | Writing and debugging code, code review and refactoring, docs and technical writing, learning and architecture decisions |
| Repetitive tasks | Tests and failing builds, commit messages and PR descriptions, boilerplate and scripts, explaining unfamiliar code |
| Biggest bottleneck | I don't know how to structure prompts for complex tasks |
| Preferred models | I switch between several |
| Experience level | Beginner |
| Desired outcome | Save time on repetitive work |

Because of these answers, the app focuses on developer workflows, teaches prompt structure through building blocks, and includes tips for Claude, ChatGPT and Gemini.

## The four sections

| Section | What it is for |
|---|---|
| **Dashboard** | Your saved workflows, favorites and a "Start here" guide at a glance |
| **My Workflows** | Reusable prompt templates with dropdown variables, one-click copy, search and filters |
| **Prompt Builder** | Assemble a prompt from labeled building blocks with a live preview |
| **Loop Builder** | Turn any prompt into a self-improving loop with scoring and stop conditions |

## Features

- **16 starter workflows in 6 categories**
  - Debug and test: debug an error, write unit tests, fix a failing CI build
  - Review and refactor: review my code, refactor safely
  - Git and pull requests: commit message, PR description, release notes
  - Boilerplate and scripts: generate boilerplate, automation script, config file
  - Understand code: explain unfamiliar code, map a legacy codebase
  - Docs, architecture and learning: README, compare design options, learning plan
- **Editable templates** with `{{variable}}` blanks, dropdown options, an example and a best-practice tip for each workflow
- **Prompt Builder blocks (9):** role, objective, context, constraints, reasoning strategy, output format, tone, examples, quality checks. Each block explains what it does and why it matters, both in the picker and after it is added.
- **Loop Builder blocks (5):** goal, evaluation criteria, improvement strategy, stop conditions, safety rules
- **Your own workflows:** create, edit, duplicate, favorite, search, filter and delete, saved in local storage
- **Model tips:** choose Claude, ChatGPT or Gemini to append a short model-specific tip to your prompts
- **Polish:** dark mode, responsive layout, import and export as JSON, a permanent "What is this?" button, and keyboard shortcuts

## How to use it

1. Download `personal-ai-playbook.html`.
2. Double-click it to open it in your browser.
3. Open **My Workflows**, choose a workflow, and fill in the variables.
4. Click **Copy prompt** and paste it into your AI tool.
5. For harder tasks, open **Prompt Builder** and add blocks one by one.
6. Click **Make a loop** to send a prompt to the **Loop Builder**.
7. Use **Export backup** in the sidebar to save your library as a JSON file.

## Keyboard shortcuts

| Key | Action |
|---|---|
| `/` | Search workflows |
| `n` | New workflow |
| `1` to `4` | Switch section |
| `d` | Toggle dark mode |
| `?` | Open the "What is this?" help |
| `Esc` | Close any dialog |

## What I learned

- A good prompt is a set of parts (role, context, constraints, format, checks), not one long sentence.
- Variables turn a one-off prompt into a reusable system.
- A loop prompt needs measurable criteria and a stop condition, or it never knows when it is done.

## Folder contents

```
Day49/
├── day49.md
├── personal-ai-playbook.html
├── ai-playbook-backup.json
├── poster.png
└── screenshots/
```

## Ideas for next time

- Add a guided first-run tour
- Add prompt chains that pass one output into the next prompt
- Add a prompt quality score
- Add more presets for each building block
