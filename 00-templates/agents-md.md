# AGENTS.md Template

This file provides context for AI coding assistants working on this project.

---

## Project Overview

What is this project? What does it do?

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | |
| Framework | |
| Package Manager | |
| Testing | |
| Build Tool | |

## Project Structure

```
project/
├── src/
├── tests/
├── docs/
└── [build config files]
```

## Development Commands

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Run tests
npm test

# Build for production
npm run build

# Lint
npm run lint

# Type check
npm run typecheck
```

## Code Style

- Use [linter] with [config]
- Follow [style guide]
- Naming conventions: [conventions]

## Architecture

Brief description of the architecture and key patterns.

### Key Files

| File | Purpose |
|------|---------|
| `src/index.ts` | Entry point |
| `src/config.ts` | Configuration |
| `src/utils/helpers.ts` | Utility functions |

### Important Patterns

- Pattern 1: Description
- Pattern 2: Description

## Common Tasks

### Adding a New Feature

1. Create file in `src/`
2. Add tests in `tests/`
3. Update documentation

### Fixing a Bug

1. Write failing test
2. Fix the bug
3. Verify test passes

## Testing

```bash
# Run all tests
npm test

# Run specific test file
npm test -- path/to/test

# Run with coverage
npm run test:coverage
```

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `API_KEY` | API key for service | Yes |
| `DEBUG` | Enable debug logging | No |

## Known Issues

- Issue 1: Workaround

## AI Assistant Guidelines

- Always run `npm run lint` before committing
- Always run `npm test` before committing
- Follow existing code patterns
- Don't add new dependencies without checking if an alternative exists
- Use TypeScript strict mode
