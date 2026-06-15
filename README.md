# 🎬 Media Toolkit – YouTube Downloader, OCR & Audio Extractor

A FastAPI-based media toolkit that lets you download YouTube videos/playlists, extract audio, pull text from images using OCR, and manage media files via a database.

## ✨ Features

- 📥 **YouTube Video Download** – Download single videos via URL (powered by `pytubefix`)
- 📃 **YouTube Playlist Download** – Download entire playlists
- 🎵 **Audio Extraction** – Extract audio from a YouTube video or playlist
- 🖼️ **Image OCR (Text Extraction)** – Upload an image (PNG/JPEG/HEIC/etc.) and extract text using **Tesseract OCR**
- 🗄️ **File Management** – Tracks downloaded videos/audio per user with **SQLAlchemy** + PostgreSQL
- 📤 **Streaming/File Responses** – Retrieve downloaded video/audio files via API endpoints

## 🛠️ Tech Stack

- **FastAPI** – Web framework / REST API
- **Uvicorn** – ASGI server
- **pytubefix** – YouTube video/playlist downloading
- **moviepy** + **ffmpeg-python** – Video/audio processing
- **pydub** – Audio manipulation
- **Pillow** + **pytesseract** – Image processing & OCR
- **SpeechRecognition** – Text-to-speech / speech utilities
- **SQLAlchemy** – ORM / database layer
- **PostgreSQL** – Database

## 📋 Prerequisites

- Python 3.10+
- [Tesseract OCR](https://github.com/UB-Mannheim/tesseract/wiki) installed separately on your system
  - Windows: Download and install from the link above, then add the install path (e.g. `C:\Program Files\Tesseract-OCR`) to your system `PATH`, or set `pytesseract.pytesseract.tesseract_cmd` in code.
- [FFmpeg](https://ffmpeg.org/download.html) installed and available on `PATH` (required by `moviepy`/`pydub`)
- PostgreSQL server running locally (or update `DATABASE_URL` for your own DB)

## ⚙️ Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/IbrahimPopatiya/image_generator.git
   cd image_generator
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   source .venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirments.txt
   ```

4. **Configure environment variables**

   Create a `.env` file in the project root:
   ```env
   DATABASE_URL=postgresql://<username>:<password>@localhost:5432/<database_name>
   ```

5. **Create required folders** (if not already present)
   ```bash
   mkdir data audio videos
   ```

## ▶️ Running the App

Run with Uvicorn directly:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Or run the script directly:
```bash
python main.py
```

The API will be available at `http://localhost:8000`, with interactive docs at `http://localhost:8000/docs`.

## 📡 Key API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/get_text` | Upload an image and extract text via OCR |
| `POST` | `/download_yt_video` | Download a YouTube video by URL |
| `GET`  | `/get_video/{uuidname}` | Retrieve a downloaded video file |
| `GET`  | `/get_user_files/{username}` | List files downloaded by a user |
| `POST` | `/get_yt_playlist` | Download a YouTube playlist |
| `POST` | `/get_audio_of_video` | Extract audio from a YouTube video |
| `GET`  | `/get_audio/{id}` | Retrieve a downloaded audio file |
| `POST` | `/get_audio_of_playlist` | Download audio for an entire playlist |

## 📂 Project Structure

```
image_generator/
├── main.py          # FastAPI app & routes
├── crud.py           # Core logic: OCR, YouTube download, audio extraction
├── models.py         # SQLAlchemy models
├── schemas.py         # Pydantic schemas
├── database.py        # DB engine/session setup
├── data/             # Uploaded images & downloaded videos (gitignored)
├── audio/            # Extracted/downloaded audio (gitignored)
├── videos/           # Downloaded videos (gitignored)
└── requirments.txt    # Python dependencies
```

## ⚠️ Notes

- `.env`, database files, and downloaded media (`data/`, `audio/`, `videos/`) are excluded from version control via `.gitignore`.
- Update `DATABASE_URL` in `.env` with your own PostgreSQL credentials before running.
