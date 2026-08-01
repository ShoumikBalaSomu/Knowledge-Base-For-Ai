# Contributing to Knowledge Base For AI

Thank you for considering a contribution! This document explains
how to suggest changes, add new guides, or improve existing ones.

---

## How to Contribute

### 1. Fork and Clone
    git clone https://github.com/YOUR_USERNAME/Knowledge-Base-For-Ai.git
    cd Knowledge-Base-For-Ai

### 2. Create a Branch
    git checkout -b feat/your-topic
    git checkout -b fix/typo-in-guide-01
    git checkout -b docs/improve-examples

### 3. Make Your Changes
Follow the writing guidelines below.

### 4. Commit
    git add .
    git commit -m "feat: add section on WebAuthn to Guide 01"

Use conventional commits:
- feat: new content or section
- fix: correction of wrong information
- docs: formatting, typos, clarity
- refactor: restructure without changing meaning

### 5. Push and Open a Pull Request
    git push origin feat/your-topic

Open a PR against main. Describe what you changed and why.

---

## Writing Guidelines

### Structure
- Every guide follows the same format:
  - Title with number prefix (e.g., "01 - Cybersecurity Guide")
  - One-sentence philosophy quote in a blockquote
  - Table of Contents
  - Numbered sections with ## headings
  - Checklist at the end
- Use tables for comparisons.
- Use code blocks for commands, configs, and architecture diagrams.
- Use checklists (- [ ]) for actionable items.

### Tone
- Direct and practical. No fluff.
- Write for a junior developer who is smart but inexperienced.
- Every recommendation must be actionable (not "consider security"
  but "use Argon2id with memory cost 64MB, time cost 3, parallelism 4").

### Accuracy
- Cite sources for version numbers, free tier limits, and algorithm names.
- If a free tier changes, update the guide. These files must stay current.
- Test every command you include.

### What NOT to Do
- Do not add promotional content for paid services without free alternatives.
- Do not remove security recommendations to simplify.
- Do not add platform-specific advice to the wrong guide.

---

## Review Process

1. A maintainer reviews within 7 days.
2. We check: accuracy, clarity, structure, tone.
3. We may request changes. This is normal and not personal.
4. Once approved, your PR is squashed and merged.

---

## Adding a New Guide (06, 07, etc.)

If you want to add a completely new knowledge file:

1. Open an issue first to discuss the topic.
2. Follow the existing structure exactly.
3. Include a checklist at the end.
4. Update README.md to list the new file.
5. Cross-reference relevant sections in existing guides.

---

## Code of Conduct

- Be respectful. Disagree with ideas, not people.
- Assume good intent.
- No harassment, trolling, or personal attacks.
- Violations result in removal from the project.

---

## Questions?

Open an issue with the label "question" and we will respond.

Thank you for making this knowledge base better for everyone.
