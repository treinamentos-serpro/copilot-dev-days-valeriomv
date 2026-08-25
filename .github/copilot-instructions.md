# Copilot Workspace Instructions

## Development Checklist

Before committing any changes, ensure:

- [ ] `uv run ruff check .` passes with no errors
- [ ] `uv run pytest` passes
- [ ] Code follows Python conventions (snake_case, type hints)
- [ ] No unused variables or imports

## Project Overview

**Soc Ops** is a Social Bingo game built with Python (FastAPI + Jinja2 + HTMX). Players find people who match questions to mark squares and get 5 in a row.

## Architecture

```
app/
├── templates/       # Jinja2 HTML templates
│   ├── base.html
│   ├── home.html
│   └── components/  # bingo_board, bingo_modal, game_screen, start_screen
├── static/          # CSS & JS assets
├── models.py        # Pydantic models (GameState, BingoSquare)
├── game_logic.py    # Board generation & bingo detection
├── game_service.py  # Session management (GameSession)
├── data.py          # Question bank
├── main.py          # FastAPI routes & HTMX endpoints
└── __init__.py

tests/
├── test_api.py      # API endpoint tests (httpx + TestClient)
└── test_game_logic.py  # Game logic unit tests
```

## Key Commands

```bash
uv sync                                            # Sync dependencies
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000  # Run dev server
uv run pytest                                       # Run tests
uv run ruff check .                                 # Lint
```

## Design Guide

### Frontend Principles

- Favor distinctive, polished interfaces over generic AI-style defaults.
- Keep the experience playful and context-aware for a social event app.
- Use thoughtful contrast, spacing, and hierarchy rather than cluttered or over-designed layouts.
- Prefer restrained motion and subtle polish over noisy animations.

### Visual Style

- Use a cohesive theme with strong accent colors and clean supporting neutrals.
- Lean on layered backgrounds, gradients, and soft shadows to create atmosphere.
- Make type feel intentional: readable, high-contrast, and visually confident without relying on default system fonts.
- Keep the interface approachable for workshop participants while still feeling premium and designed.

### CSS and UI Implementation

- Prefer reusable utility classes from `app/static/css/app.css` before introducing custom CSS.
- Follow the project utility patterns for spacing, layout, color, shadow, and typography.
- Use CSS variables for theme values when a design needs consistency across multiple components.
- Keep selectors low-specificity and avoid adding broad global styles that fight the existing utility approach.

### Interaction Guidance

- Use hover, focus, and active states to reinforce actions without making the UI feel busy.
- Favor high-impact moments: a clear highlighted board state, a celebratory bingo moment, or a subtle reveal when the game starts.
- Keep transitions smooth and brief; they should support clarity, not distract from the game.

### Accessibility and Quality

- Preserve readable contrast ratios for text and controls.
- Ensure buttons, links, and form elements have clear focus styling.
- Maintain layout consistency across templates and game states.
- Test interactive flows in the browser to confirm the visual hierarchy still reads clearly after changes.

## Styling

Uses custom CSS utility classes (Tailwind-like) in `app/static/css/app.css`:
- Layout: `.flex`, `.grid`, `.items-center`
- Spacing: `.p-4`, `.mb-2`, `.mx-auto`
- Colors: `.bg-accent`, `.bg-marked`, `.text-gray-700`

## State Management

- `GameSession` manages game state server-side
- State persisted via signed cookies (itsdangerous)
- HTMX handles partial page updates without full reloads
