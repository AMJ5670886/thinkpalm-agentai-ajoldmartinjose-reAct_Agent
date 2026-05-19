# thinkpalm-agentai-ajoldmartinjose-reAct_Agent

**AJOLD MARTIN JOSE**

## Lab 1 — ReAct Agent

Build a minimal Python ReAct agent that: takes a user query → reasons step-by-step → calls a tool → returns final answer. Run in Google Colab. Screenshot your working output.

---

## Overview

This project started as a **minimal ReAct film agent** for TMDB lookups via a terminal CLI, and has since been **enhanced into a full interactive Colab UI** for movie discovery and ticket booking.

### Two versions in this repo

| Version | What it does | Interface |
|---------|--------------|-----------|
| **v1 — ReAct Agent** (`src/minimal_react_agent.ipynb`) | LLM reasons Thought → Action → Observation → Final Answer, calls TMDB | Terminal `input()` / `print()` |
| **v2 — Movie Finder & Show Booking** (enhanced) | Two-tab GUI for searching films and booking running shows | ipywidgets + HTML cards in Colab |

---

## Lab 2 -  Enhanced Features

### Tab 1 · Movie Info (search & details)

- TMDB search with **title-relevance scoring** (filters out unrelated popular hits)
- **"Did you mean…?"** suggestion for fuzzy spellings (e.g. *Athiadi* → *Athiradi*)
- Rich result cards: poster, year, language, rating, director, main cast, plot
- Direct **View on TMDB** link

### Tab 2 · Book Shows (currently running movies)

- **City picker** for 15 Indian cities (Mumbai, Kochi, Bengaluru, …)
- **Now-playing poster grid** (TMDB `now_playing`, region IN)
- **Clickable posters** — reveals booking flow only after a movie is selected
- Demo **theatre / showtime / seat** selection
- **Booking confirmed** card with ID, seats, demo amount
- **Seat warning** under the Confirm button if no seats are chosen
- **Auto-scroll** to the booking section on poster click
- **Clear previous booking** automatically when a new movie is selected
- **"Back to movies"** to return to the poster grid

### Tech additions in v2

| Capability | Implementation |
|------------|----------------|
| Interactive UI | `ipywidgets.Tab`, `VBox`, `HBox`, `Dropdown`, `SelectMultiple`, `Output` |
| Poster click → Python | `google.colab.kernel.invokeFunction` + `output.register_callback("on_poster_click", ...)` |
| Smooth scroll | `IPython.display.Javascript` with `scrollIntoView` |
| HTML render | TMDB poster URLs (`POSTER_BASE`, `POSTER_BASE_LARGE`) |
| Fuzzy matching | `difflib.SequenceMatcher` + custom token / substring heuristics |
| Safe rendering | `html.escape` for user-derived text |

---

## Structure

```
.
├── README.md                          ← this file
├── src/
│   └── minimal_react_agent.ipynb      ← v1 ReAct agent (CLI)
├── enhanced/
│   └── movie_finder_show_booking.py   ← v2 Colab UI (paste in one Colab cell)
└── screenshots/                       ← v1 + v2 demo screenshots
```

---

## How to Run

### v1 — ReAct Agent (terminal CLI)

1. Open `src/minimal_react_agent.ipynb` in Google Colab.
2. In the **Secrets** panel (key icon), add:
   - `GROQ_API_KEY` — from [console.groq.com](https://console.groq.com)
   - `TMDB_API_KEY` — v4 token from [themoviedb.org](https://www.themoviedb.org/settings/api)
3. Run all cells. At the prompt, type a film name (e.g. `Manjummel Boys`) or `exit`.

### v2 — Movie Finder & Show Booking (Colab UI)

1. Open a fresh Colab notebook.
2. Install once:
   ```bash
   !pip install openai ipywidgets requests --quiet
   ```
3. Add the same **GROQ_API_KEY** and **TMDB_API_KEY** in **Secrets**.
4. Paste the enhanced Python file into one cell and run.
5. Use the **Movie Info** tab to search films and view details.
6. Switch to **Book Shows** → pick city → click a poster → choose seats → **Confirm Booking**.

### Run locally (advanced)

```bash
export GROQ_API_KEY="your_groq_api_key"
export TMDB_API_KEY="your_tmdb_api_key"
python src/film_agent.py        # v1 CLI
```

v2 is designed for Colab (uses `google.colab.output` callbacks); it will not run as-is in a plain terminal.

---

## API Keys

| Key | Purpose | Where to get it |
|-----|---------|-----------------|
| `GROQ_API_KEY` | LLM reasoning for v1 ReAct agent | [console.groq.com](https://console.groq.com) |
| `TMDB_API_KEY` | Movie search, posters, credits, now-playing | [themoviedb.org/settings/api](https://www.themoviedb.org/settings/api) |

Stored in Colab **Secrets** — never commit keys to git.

---

## Tools / Libraries

| Tool | Use |
|------|-----|
| **Groq API** (`llama-3.1-8b-instant`) | ReAct loop reasoning in v1 |
| **TMDB API** | Search movies, fetch credits and now-playing list |
| **`openai`** | OpenAI-compatible client pointed at Groq base URL |
| **`requests`** | HTTP calls to TMDB |
| **`ipywidgets`** | Tabs, dropdowns, buttons, HTML cards in v2 |
| **`IPython.display`** | `HTML`, `Javascript`, `clear_output` |
| **`google.colab.output`** | Bridge for poster-click → Python callback |
| **`difflib.SequenceMatcher`** | Title relevance scoring |
| **`re`, `json`, `html`** | Parsing, escaping, serialization |

---

## Demo Flow (v2)

```
Open notebook
   ↓
[Movie Info]  Search "Athiadi"
   ↓ "Did you mean Athiradi?"
   ↓ Poster + cast + director + plot card

[Book Shows]  Pick city "Kochi"
   ↓ Load running shows  →  Poster grid
   ↓ Click a poster
   ↓ Auto-scroll to Book Tickets
   ↓ Pick theatre + showtime + seats
   ↓ Confirm Booking  →  Booking Confirmed (Demo) card
```

---

## Screenshots

Add to `/screenshots`:

- `v1_react_agent.png` — terminal ReAct output for a film query
- `v2_movie_info.png` — search tab with result card
- `v2_book_shows.png` — poster grid + selected booking panel
- `v2_booking_confirmed.png` — booking confirmation card

---

## Productivity Note (Cursor AI)

The v2 enhancement was built incrementally with **Cursor AI**. Plain-language prompts ("fix search relevance", "add BookMyShow-style booking", "show warning under Confirm Booking", …) generated the widget wiring, HTML, callbacks, and scroll-to-section behavior, turning a ~250-line CLI script into a ~750-line Colab app while keeping the original ReAct agent intact.

---

## License

For internal lab / learning use.
