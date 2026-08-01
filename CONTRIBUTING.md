# Contributing to Knowledge Base For AI

Thank you for your interest in contributing! This document provides guidelines and information for contributors.

---

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How to Contribute](#how-to-contribute)
3. [Development Setup](#development-setup)
4. [Writing Standards](#writing-standards)
5. [Pull Request Process](#pull-request-process)
6. [Content Guidelines](#content-guidelines)
7. [Review Process](#review-process)
8. [Recognition](#recognition)

---

## Code of Conduct

### Our Pledge

We pledge to make participation in this project a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

Positive behavior:
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other members

Unacceptable behavior:
- Trolling, insulting/derogatory comments, personal or political attacks
- Public or private harassment
- Publishing others private information without permission
- Other conduct which could be considered inappropriate

---

## How to Contribute

### Types of Contributions

| Type | Description |
|------|-------------|
| Content Addition | Add new sections, examples, or resources |
| Content Update | Update outdated information, fix errors |
| New Module | Propose and write an entirely new knowledge module |
| Bug Fix | Fix broken links, formatting issues, typos |
| Translation | Translate content to other languages |
| Review | Review and provide feedback on PRs |

### Getting Started

1. Fork the repository
2. Clone your fork locally
3. Create a feature branch
4. Make your changes
5. Commit with a descriptive message
6. Push to your fork
7. Open a Pull Request

---

## Development Setup

### Prerequisites

- Git
- A Markdown editor (VS Code recommended)
- Markdownlint extension (for formatting)

### Local Setup

Clone the repository and create a feature branch:

    git clone https://github.com/YOUR_USERNAME/Knowledge-Base-For-Ai.git
    cd Knowledge-Base-For-Ai
    git checkout -b feature/your-feature-name

### File Structure

    Knowledge-Base-For-Ai/
      README.md                      (Project overview)
      CONTRIBUTING.md                (This file)
      LICENSE                        (MIT License)
      01_Cybersecurity_Guide.md      (Security module)
      02_UI_UX_Design_Guide.md      (Design module)
      03_Cost_Optimization_Guide.md  (Cost module)
      04_Multi_Platform_Guide.md     (Platform module)
      05_AI_Development_Framework.md (AI module)

---

## Writing Standards

### Markdown Formatting

- Use ATX-style headers (# for H1, ## for H2, etc.)
- One blank line before and after headers
- Use tables for structured comparisons
- Use code blocks with language identifiers
- Keep lines under 120 characters where practical
- Use relative links for internal references
- Use descriptive link text (not 'click here')

### Content Style

- Write in present tense
- Use active voice
- Be specific and actionable
- Include examples for every recommendation
- Cite sources for claims and statistics
- Keep paragraphs short (3-5 sentences)
- Use bullet points for lists of 3+ items
- Define acronyms on first use

### Naming Conventions

- Files: XX_Category_Name.md (numbered, PascalCase)
- Headers: Sentence case
- Code examples: Use realistic variable names
- Placeholders: Use YOUR_VALUE format

---

## Pull Request Process

### Before Submitting

1. Ensure your content is accurate and up-to-date
2. Check for spelling and grammar errors
3. Verify all links are working
4. Ensure consistent formatting with existing content
5. Add yourself to the contributors section if desired
6. Test that Markdown renders correctly (GitHub preview)

### PR Template

When opening a PR, include:

- Title: Clear description of change (prefix with type: docs, fix, feat)
- Description: What changed and why
- Related Issues: Link any relevant issues
- Checklist: Confirm all standards are met

### Commit Messages

Follow Conventional Commits:

- docs: Add section on quantum encryption
- fix: Correct outdated TLS recommendation
- feat: Add new module on DevOps practices
- style: Fix formatting in cost guide
- refactor: Reorganize security checklist

---

## Content Guidelines

### Accuracy

- All recommendations must be current (within 12 months)
- Security practices must reference established standards (NIST, OWASP)
- Cost information must be verified against current pricing
- Tool recommendations must be actively maintained
- Include version numbers for specific tool references

### Completeness

- Each section should be actionable (reader can implement immediately)
- Include both 'what' and 'why' for every recommendation
- Provide alternatives for different budgets and scales
- Include common pitfalls and how to avoid them
- Add references/further reading for deep dives

### Objectivity

- Present multiple options where appropriate
- Disclose any affiliations or biases
- Base recommendations on evidence, not opinion
- Acknowledge trade-offs honestly
- Update when better alternatives emerge

---

## Review Process

### Review Criteria

1. Accuracy: Is the information correct and current?
2. Completeness: Does it cover the topic sufficiently?
3. Clarity: Is it easy to understand and follow?
4. Consistency: Does it match the style of existing content?
5. Actionability: Can a reader implement the advice?

### Timeline

- Initial review: Within 7 days
- Revision requests: Address within 14 days
- Merge: After approval from 1 maintainer

---

## Recognition

All contributors will be recognized:

- Listed in the CONTRIBUTORS section of README
- Credited in commit history
- Mentioned in release notes for significant contributions

---

## Questions?

Open an issue or contact the maintainer:

- GitHub: @ShoumikBalaSomu
- Email: somu2305101657@diu.edu.bd

---

Thank you for contributing to making this knowledge base better for everyone!

*Last Updated: August 2026*