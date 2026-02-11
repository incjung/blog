---
name: blog-format
description: Format and validate blog posts, convert between Markdown and Org-mode
license: MIT
compatibility: opencode
metadata:
  audience: blog authors
  workflow: formatting
---

## What I do
- Validate Hugo frontmatter YAML syntax
- Format Org-mode content (tables, code blocks, lists)
- Convert between Markdown and Org-mode formats
- Fix image paths (relative ↔ absolute)
- Check for common formatting issues

## When to use me
Use this when you want to:
- Fix formatting issues in a post
- Convert a file from Markdown to Org-mode (or vice versa)
- Validate frontmatter before deployment
- Standardize image references

## Supported Operations

### 1. Validate Frontmatter
Check Hugo frontmatter for:
- Valid YAML syntax
- Required fields: title, date
- Proper date format (ISO 8601)
- Boolean values for draft field
- Valid tag format (array of strings)

### 2. Format Org-mode
- Re-align tables
- Normalize code block syntax (`#+BEGIN_SRC` / `#+END_SRC`)
- Fix heading levels (consistent spacing)
- Standardize list markers
- Remove trailing whitespace

### 3. Convert Format
**Markdown → Org-mode:**
- `# Heading` → `* Heading`
- `## Subheading` → `** Subheading`
- `[text](url)` → `[[url][text]]`
- `![alt](path)` → `#+CAPTION: alt` + `[[file:path]]`
- Code fences → `#+BEGIN_SRC lang` blocks

**Org-mode → Markdown:**
- Reverse of above transformations
- Preserve Hugo frontmatter

### 4. Fix Image Paths
- Convert absolute URLs to relative paths when possible
- Ensure images are in `static/images/` directory
- Fix broken image references
- Update Hugo figure shortcodes if needed

## Usage Workflow

### Format Current File
1. Ask user which file to format (or use current file)
2. Read and validate frontmatter
3. Apply formatting rules
4. Show diff of changes
5. Save formatted file

### Convert File Format
1. Identify source format (check file extension and content)
2. Ask target format (org or markdown)
3. Convert content
4. Save with appropriate extension
5. Update internal links if needed

## Example Commands
```
"Format this post" → Validates and formats current file
"Convert to org-mode" → Converts markdown file to org
"Fix image paths" → Updates all image references
```

## Validation Checks

### Frontmatter
- [ ] Title is present and not empty
- [ ] Date is valid ISO format
- [ ] Draft is boolean (true/false)
- [ ] Tags is an array
- [ ] No syntax errors in YAML

### Content
- [ ] No broken internal links
- [ ] Images exist in static directory
- [ ] Code blocks have language specified
- [ ] Tables are properly formatted
- [ ] No mixed line endings

## Error Handling
- Report specific line numbers for YAML errors
- Suggest fixes for common issues
- Create backup before major conversions
- Warn about potential data loss in conversions

## Best Practices
- Always validate after manual edits
- Use consistent heading levels (h1 → h6)
- Prefer relative paths for internal links
- Use descriptive alt text for images
- Keep frontmatter at the top of the file
