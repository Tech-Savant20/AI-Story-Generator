# AI Story Generator with Flask 📚✨

A feature-rich Flask web app powered by GPT-2, designed to turn your story prompts into full-length narratives. Includes user accounts, story enhancement tools, export options, and a creative dashboard.

## 📸 Screenshots

![Story generator home page](images/Screenshot_3-7-2025_232616_127.0.0.1.jpeg)
![Story generator screenshot 2](images/Screenshot_3-7-2025_232842_127.0.0.1.jpeg)
![Story generator screenshot 3](images/Screenshot_3-7-2025_232952_127.0.0.1.jpeg)
![Story generator screenshot 4](images/Screenshot_3-7-2025_233219_127.0.0.1.jpeg)
![Story generator screenshot 5](images/Screenshot_3-7-2025_233234_127.0.0.1.jpeg)
![Story generator screenshot 6](images/Screenshot_3-7-2025_233248_127.0.0.1.jpeg)

## 🚀 Features

### 🤖 AI Story Writing

* **Powered by GPT-2 Medium**
* **Genre Selection**: Fantasy, Sci-fi, Romance, Mystery, Horror, Adventure, Comedy
* **Custom Settings**: Control length, creativity (temperature), and coherence (top\_p)
* **Story Enhancer**: Add more depth, emotion, or action
* **Alternative Endings**: Create multiple outcomes for a story

### 👤 User Accounts

* Register, login, and manage stories securely
* Save stories privately or share with the community
* View genre preferences and story stats

### 📦 Export & Community

* **PDF Export** for beautifully formatted downloads
* **Community Hub**: Browse stories other users have made public

### ✨ Creative Toolbox

* **Prompt Generator**
* **Writing Analytics** (word count, genre distribution)
* **Model Status Monitor**

---

## 🛠️ Installation

### Prerequisites

* Python 3.7+
* `pip` installed

### Quick Start (Windows)

```bash
# Clone/download the project and run
setup.bat
```

This sets up a virtual environment, installs dependencies, launches the app, and opens your browser.

### Manual Setup (All Platforms)

```bash
python -m venv venv
# Activate
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install packages
pip install -r requirements.txt

# Run app
python app.py
```

Visit [http://localhost:5000](http://localhost:5000)

---

## 📚 Project Structure

```
AI-Story-Generator/
├── app.py               # Main application
├── requirements.txt     # Dependencies
├── setup.bat            # Windows setup
├── templates/           # HTML UI
├── static/              # CSS & JS
├── images/              # README screenshots
├── models/              # GPT-2 model files (downloaded on first run)
└── stories.db           # SQLite database (created on first run)
```

---

## 🧪 API Overview

### Story APIs

* `POST /generate` – Create a new story
* `POST /enhance` – Add improvements
* `POST /multiple-endings` – Generate alternate endings

### User APIs

* `POST /register`, `POST /login`, `POST /logout`

### Story Management

* `GET /my-stories`, `GET /public-stories`, `GET /story-stats`

### Utilities

* `GET /random-prompt`, `GET /model-info`, `GET /health`, `GET /export-pdf/<story_id>`

---

## 🧩 Dependencies

```text
Flask, torch, transformers, reportlab, numpy, tokenizers,
huggingface-hub, accelerate, protobuf, requests, Pillow, Werkzeug
```

---

## ⚙️ Configuration

### Model Setup

```python
self.model_name = "gpt2-medium"
self.models_dir = "./models"
```

### Secret Key (update for production)

```python
app.secret_key = 'your-secret-key-change-this'  # replace with a long random value
```

---

## 🧾 Database Overview

### Tables

**Users**: id, username, email, password\_hash, created\_at
**Stories**: id, user\_id, title, prompt, story, genre, word\_count, rating, created\_at, is\_public
**Favorites**: id, user\_id, story\_id, created\_at (table is created, but no favorites feature uses it yet)

---

## 🛠 Troubleshooting

* **Model Download Fails**: Retry or check disk/internet
* **CUDA Issues**: The GPU is used automatically when CUDA is available; otherwise the app runs on CPU
* **Port Conflicts**: Change port in `app.py`
* **DB Errors**: Delete `stories.db` to reset

### Performance Tips

* First run may be slow (model loading)
* Lower `max_length` for faster results
* Use GPU for significant speed boost

---

## 🤝 Contributing

Improvements welcome:

* Add new models or genres
* UI/UX enhancements
* Collaborative storytelling
* Mobile support

---

## 📞 Support

Having issues?

* Recheck installation steps
* Review terminal errors
* Ensure Python 3.7+ is installed
* All dependencies installed?

---

## 🧠 Technical Info

* **Model**: GPT-2 Medium (355M parameters)
* **Frameworks**: Flask + Hugging Face Transformers
* **Storage**: Local (500MB model, \~2GB RAM use)
* **Performance**: \~2–10s per generation

---

**✨ Let your creativity run wild. Build worlds with AI. Happy writing!**
