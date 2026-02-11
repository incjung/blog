---
name: blog-post-create
description: Create new blog post with AI-generated content, Hugo frontmatter and auto-start local preview server
license: MIT
compatibility: opencode
metadata:
  audience: blog authors
  workflow: hugo
---

## What I do
- Create a new blog post file with format `YYYY-MM-DD-title.org`
- Generate Hugo frontmatter with title, date, draft status, and tags
- **Generate comprehensive blog post content** combining technical tutorial and learning notes style
- Convert title to URL-friendly slug (spaces → hyphens, lowercase)
- Automatically start `hugo server -D` in background for live preview
- Validate that we're in the correct blog repository

## When to use me
Use this when you want to:
- Write a new blog post with AI-generated content
- Create a technical tutorial or learning note
- Start a draft that will be previewed locally before publishing

## Prerequisites
- Hugo must be installed (`hugo version`)
- Must be in `/home/incjjung/github/blog` directory or its subdirectories
- Port 1313 should be available (or specify different port)

## Usage Workflow

### 1. Get User Input
Ask the user for:
- Post title/topic (e.g., "learning Go", "Kubernetes deployment")

### 2. Create File Structure
1. Convert title to slug (e.g., "Learning Go" → "learning-go")
2. Generate filename: `YYYY-MM-DD-learning-go.org`
3. Create file in `content/post/` directory
4. Add Hugo frontmatter:
   ```yaml
   ---
   title: "Learning Go"
   date: YYYY-MM-DDTHH:MM:SS+13:00
   draft: true
   tags: ["go", "programming", "tutorial"]
   ---
   ```

### 3. Generate Content (CRITICAL STEP)
**After creating the file with frontmatter, I MUST generate comprehensive content following this structure:**

**Content Style:** Technical Tutorial + Learning Notes (hybrid)
**Length:** 2000-3000 characters total
**Format:** Org-mode with proper heading hierarchy

**Required Sections:**

1. **소개 (Introduction)** - 200-300 characters
   - Topic overview and importance
   - Why readers should care
   - Target audience

2. **사전 준비 (Prerequisites)** - 100-200 characters
   - Required tools and versions
   - Environment setup needs

3. **핵심 개념 (Core Concepts)** - 500-700 characters
   - Technical concept explanations
   - Key terminology
   - Underlying principles
   - Learning notes style with clear explanations

4. **단계별 튜토리얼 (Step-by-Step Tutorial)** - 600-800 characters
   - Installation/Setup steps
   - Hands-on usage instructions
   - Practical examples
   - Technical tutorial style with commands and actions

5. **코드 예시 (Code Examples)** - 300-400 characters
   - Practical, runnable code snippets
   - Org-mode code blocks with language specification
   - Real-world applicable examples

6. **실전 활용 (Real-world Applications)** - 200-300 characters
   - Actual use cases
   - When and where to apply
   - Industry examples

7. **팁과 모범 사례 (Tips and Best Practices)** - 200-300 characters
   - Common pitfalls to avoid
   - Optimization suggestions
   - Best practices from experience

8. **마무리 및 참고자료 (Conclusion and References)** - 100-200 characters
   - Summary of key points
   - Official documentation links
   - Further reading suggestions

**Content Generation Guidelines:**
- Write in **English**
- Use **Org-mode syntax**:
  - Headings: `*`, `**`, `***`
  - Code blocks: `#+BEGIN_SRC language` / `#+END_SRC`
  - example blocks: `#+BEGIN_EXAMPLE` / `#+END_EXAMPLE`
  - quote blocks: `#+BEGIN_QUOTE` / `#+END_QUOTE`
  - Lists: `-` or `1.`
  - Links: `[[URL][description]]`
- Include **specific, actionable** instructions (not vague generalities)
- Provide **real version numbers** and **actual commands** when applicable
- Ensure code examples are **runnable and tested**
- Balance between technical depth and accessibility

### 4. Write Complete File
Combine frontmatter and generated content into the org file.

### 5. Start Hugo Server
- Start Hugo server with drafts enabled: `hugo server -D &`
- Print the local preview URL: http://localhost:1313

### 6. Server Management
- Hugo server runs in background
- User can stop it with `Ctrl+C` or by running `skill blog-deploy`
- If server is already running on port 1313, skip starting a new one

## File Location
Posts are created in: `content/post/YYYY-MM-DD-slug.org`

## Example
```
User: "Create a post about learning Go"
→ Creates: content/post/2026-02-12-learning-go.org
→ Generates: Comprehensive content with all 8 sections
→ Starts: hugo server -D on http://localhost:1313
```

## Error Handling
- Check if Hugo is installed before proceeding
- Verify we're in the blog repository
- Handle port conflicts (suggest using different port)
- Ensure content/post directory exists
- If content generation fails, create file with frontmatter only and notify user
