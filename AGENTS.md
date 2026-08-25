# Agent Instructions

## Mandatory checklist

- [ ] `uv run ruff check .` passes
- [ ] `uv run pytest` passes
- [ ] Application build/start check passes with `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`

## Project

Soc Ops is a FastAPI/Jinja2 Social Bingo game enhanced with HTMX. Sync dependencies with `uv sync`; use an external browser at `http://localhost:8000`, never Simple Browser.

## Architecture

`app/main.py` owns FastAPI routes and session lookup; `app/game_service.py` owns in-memory `GameSession` transitions; `app/game_logic.py` owns pure board/bingo rules; `app/models.py` defines frozen Pydantic models; `app/data.py` contains questions; `app/templates/` and `app/static/` contain the UI. Tests live in `tests/test_game_logic.py` and `tests/test_api.py`.

## Implementation guidance

Keep rules pure in `game_logic.py`, state transitions in `GameSession`, and `BingoSquareData` immutable via Pydantic `model_copy`. Route or HTMX changes require API tests and rendered HTML checks. Use type hints/snake_case, follow [app.css](app/static/css/app.css) and [.github/instructions](.github/instructions/), and do not modify `.solutions/` unless explicitly requested.

## Documentation

Docs: [README.md](README.md), [workshop/GUIDE.md](workshop/GUIDE.md), and [CONTRIBUTING.md](CONTRIBUTING.md).
