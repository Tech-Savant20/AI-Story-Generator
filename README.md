# AI Story Generator

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white)
![Hugging Face Transformers](https://img.shields.io/badge/Transformers-GPT--2%20Medium-FFD21E?logo=huggingface&logoColor=black)

A Flask web app that turns a short prompt into a story using GPT-2 Medium, running locally on your own machine. You pick a genre and tune how creative the output is, then extend the story, rewrite it in a different style, or generate alternative endings. Signed-in users get their stories saved and can share them with others.

![Home page](images/Screenshot_3-7-2025_232616_127.0.0.1.jpeg)

<details>
<summary>More screenshots</summary>

![Screenshot 2](images/Screenshot_3-7-2025_232842_127.0.0.1.jpeg)
![Screenshot 3](images/Screenshot_3-7-2025_232952_127.0.0.1.jpeg)
![Screenshot 4](images/Screenshot_3-7-2025_233219_127.0.0.1.jpeg)
![Screenshot 5](images/Screenshot_3-7-2025_233234_127.0.0.1.jpeg)
![Screenshot 6](images/Screenshot_3-7-2025_233248_127.0.0.1.jpeg)

</details>

## Features

- **Story generation** with GPT-2 Medium (355M parameters) through the Hugging Face `text-generation` pipeline.
- **Seven genres:** fantasy, sci-fi, mystery, romance, horror, adventure and comedy. Each one adds a genre-specific opening line to your prompt.
- **Generation controls:** length (up to 1,000 tokens), temperature and top-p.
- **Story enhancer:** rewrites a story with more detail, dialogue, emotion or action.
- **Alternative endings:** up to five endings, each generated at a slightly different temperature for variety.
- **Random prompt generator** for when you need an idea.
- **Accounts:** register and log in (passwords hashed with Werkzeug). Stories generated while logged in are saved to SQLite and can be kept private or made public.
- **Community page** listing the latest public stories, and per-user stats (story count, total and average word count, stories per genre).
- **PDF export** of any saved story (ReportLab).

## How it works

```
Browser (HTML/CSS/JS) ──► Flask routes ──► StoryGenerator ──► GPT-2 Medium (transformers + PyTorch)
                                │
                                └──► SQLite (users, stories)
```

On first start the app downloads GPT-2 Medium from Hugging Face and saves it to `models/gpt2_medium/`, so later starts load it from disk. It uses the GPU automatically when CUDA is available and the CPU otherwise.

## Getting started

**Requirements:** Python 3.9 or newer, about 2 GB of free RAM, and roughly 1.5 GB of disk space for the model. The first run needs an internet connection to download it.

### Windows (one step)

```bat
setup.bat
```

This creates a virtual environment, installs the dependencies, starts the server and opens http://127.0.0.1:5000 in your browser.

### Any platform

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Then open http://localhost:5000. The first start is slow while the model downloads.

## API

| Method | Route | Purpose |
|--------|-------|---------|
| `POST` | `/generate` | Generate a story from `prompt`, with optional `genre`, `max_length`, `temperature`, `top_p` |
| `POST` | `/enhance` | Rewrite `story` with `type` = `detail`, `dialogue`, `emotion` or `action` |
| `POST` | `/multiple-endings` | Generate `num_endings` (max 5) endings for `story` |
| `GET` | `/random-prompt` | Random story prompt |
| `POST` | `/register`, `/login`, `/logout` | Account management |
| `GET` | `/my-stories`, `/public-stories`, `/story-stats` | Saved stories and stats |
| `GET` | `/export-pdf/<story_id>` | Download a story as PDF |
| `GET` | `/model-info`, `/health` | Model location/size and health check |

## Project structure

```
AI-Story-Generator/
├── app.py            # Flask app, StoryGenerator class, database helpers, routes
├── templates/        # index.html
├── static/           # css/styles.css, js/app.js
├── images/           # README screenshots
├── requirements.txt
└── setup.bat         # Windows setup-and-run script
```

`models/` and `stories.db` are created on first run.

## Limitations

- GPT-2 Medium is a 2019 model, so stories can drift off topic or repeat themselves, especially at high temperature or long lengths.
- On CPU a story takes a few seconds or more to generate.
- The secret key in `app.py` (`app.secret_key`) is a placeholder and the server runs in debug mode, so this setup is for local use only. Set a real secret key and turn off debug mode before deploying it anywhere.
- The database has a `favorites` table, but no feature uses it yet.

## Tech stack

Python, Flask, Hugging Face Transformers, PyTorch, SQLite, ReportLab, HTML/CSS/JavaScript.
