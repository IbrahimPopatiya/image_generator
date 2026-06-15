![Media Toolkit](https://placehold.co/1200x300/831843/fbcfe8?text=Media+Toolkit)

# 🎬 Media Toolkit – YouTube Downloader, OCR & Audio Extractor

> A FastAPI-powered all-in-one toolkit for **downloading YouTube videos/playlists**, **extracting text from images via OCR**, and **extracting/managing audio** — all backed by a database for per-user file tracking.

---

## ✨ Features

- 📥 **YouTube Video Download** – Download single videos via URL (powered by `pytubefix`)
- 📃 **YouTube Playlist Download** – Download entire playlists in one go
- 🎵 **Audio Extraction** – Extract audio from a YouTube video or playlist
- 🖼️ **Image OCR (Text Extraction)** – Upload an image (PNG/JPEG/HEIC/etc.) and extract text using **Tesseract OCR**
- 🗄️ **File Management** – Tracks downloaded videos/audio per user with **SQLAlchemy** + PostgreSQL
- 📤 **Streaming/File Responses** – Retrieve downloaded video/audio files via simple API endpoints
- 🔊 **Speech Utilities** – Built-in support for speech recognition / TTS workflows

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| 🌐 Web Framework | **FastAPI**, **Uvicorn** |
| 📺 YouTube | **pytubefix** |
| 🎞️ Media Processing | **moviepy**, **ffmpeg-python**, **pydub** |
| 🖼️ OCR | **Pillow**, **pytesseract** |
| 🎙️ Speech | **SpeechRecognition** |
| 🗄️ Database | **SQLAlchemy**, **PostgreSQL** |

---

## 📡 Key API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/get_text` | 🖼️ Upload an image and extract text via OCR |
| `POST` | `/download_yt_video` | 📥 Download a YouTube video by URL |
| `GET`  | `/get_video/{uuidname}` | 🎬 Retrieve a downloaded video file |
| `GET`  | `/get_user_files/{username}` | 📋 List files downloaded by a user |
| `POST` | `/get_yt_playlist` | 📃 Download a YouTube playlist |
| `POST` | `/get_audio_of_video` | 🎵 Extract audio from a YouTube video |
| `GET`  | `/get_audio/{id}` | 🔊 Retrieve a downloaded audio file |
| `POST` | `/get_audio_of_playlist` | 🎶 Download audio for an entire playlist |

---

## 📂 Project Structure

```
image_generator/
├── main.py            # FastAPI app & routes
├── crud.py            # Core logic: OCR, YouTube download, audio extraction
├── models.py          # SQLAlchemy models
├── schemas.py         # Pydantic schemas
├── database.py        # DB engine/session setup
├── data/              # Uploaded images & downloaded videos (gitignored)
├── audio/             # Extracted/downloaded audio (gitignored)
├── videos/            # Downloaded videos (gitignored)
└── requirments.txt    # Python dependencies
```

---

## 🖼️ Demo / Screenshots

> 📌 *Placeholder images below — replace with real screenshots of the running app/API docs.*

![API Demo](https://placehold.co/800x400?text=API+Demo)

![OCR Demo](https://placehold.co/800x400?text=OCR+Text+Extraction)

![YouTube Download Demo](https://placehold.co/800x400?text=YouTube+Download)

---

## ⚠️ Notes

- `.env`, database files, and downloaded media (`data/`, `audio/`, `videos/`) are excluded from version control via `.gitignore`.
- Update `DATABASE_URL` in `.env` with your own PostgreSQL credentials before running.

---

## 🛠️ Setup

### 📋 Prerequisites

- 🐍 Python 3.10+
- 🔤 [Tesseract OCR](https://github.com/UB-Mannheim/tesseract/wiki) installed separately on your system
  - **Windows**: Download and install from the link above, then add the install path (e.g. `C:\Program Files\Tesseract-OCR`) to your system `PATH`, or set `pytesseract.pytesseract.tesseract_cmd` in code.
- 🎞️ [FFmpeg](https://ffmpeg.org/download.html) installed and available on `PATH` (required by `moviepy`/`pydub`)
- 🐘 PostgreSQL server running locally (or update `DATABASE_URL` for your own DB)

### 1️⃣ Clone the repository

```bash
git clone https://github.com/IbrahimPopatiya/image_generator.git
cd image_generator
```

### 2️⃣ Create and activate a virtual environment

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

### 3️⃣ Install dependencies

```bash
pip install -r requirments.txt
```

### 4️⃣ Configure environment variables

Create a `.env` file in the project root:

```env
DATABASE_URL=postgresql://<username>:<password>@localhost:5432/<database_name>
```

### 5️⃣ Create required folders (if not already present)

```bash
mkdir data audio videos
```

---

## 🚀 Run

Run with Uvicorn directly:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Or run the script directly:

```bash
python main.py
```

The API will be available at `http://localhost:8000`, with interactive docs at `http://localhost:8000/docs`. 🎉

### Example Usage

```bash
# Extract text from an image
curl -X POST "http://localhost:8000/get_text" -F "file=@image.png"

# Download a YouTube video
curl -X POST "http://localhost:8000/download_yt_video" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://www.youtube.com/watch?v=xxxxxxxxx", "username": "demo"}'
```
