# Project Guidelines for Claude

## Linting Requirements

### Markdown Files

After creating or editing ANY markdown file (.md), ALWAYS run:

```bash
markdownlint '**/*.md' --config .markdownlint.json
```

Or for a specific file:

```bash
markdownlint <filename>.md --config .markdownlint.json
```

If there are any linting errors, fix them immediately.

## Project-Specific Context

### Litestream LTX Testing

This project is for testing the new Litestream LTX (Log Transaction) format implementation.

Key files:

- `LITESTREAM_LTX_TESTING_REPORT.md` - Comprehensive testing report
- `TODO.md` - Current task list based on Ben Johnson's feedback
- `docs/images/` - Contains properly named screenshots referenced in documentation
- `.screenshots/` - Original screenshots directory (kept for reference)

### Common Commands

- Build: `go build ./cmd/litestream`
- Test markdown: `markdownlint '**/*.md' --config .markdownlint.json`

## Code Style

- Use consistent formatting in markdown files
- Always ensure proper spacing around headings
- End files with a single newline
- Use proper URL formatting in markdown (avoid bare URLs)

## Git Commit Requirements

- ALWAYS sign commits using `-S` flag
- Example: `git commit -S -m "Your commit message"`
- This ensures commit authenticity and security
