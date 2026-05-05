# AI Real-time Gym Coach

A Streamlit app for real-time exercise tracking and AI voice coaching. The app uses webcam video, MediaPipe pose landmarks, exercise-specific detectors, local workout persistence, and optional Groq-powered coaching feedback.

## Features

- Real-time webcam analysis with `streamlit-webrtc`
- Pose landmark detection using MediaPipe
- Exercise counters and form metrics for squats, push-ups, biceps curls, shoulder press, and lunges
- Sidebar workout planning for sets and reps
- Local user/session persistence with SQLite
- Optional AI coaching feedback with Groq and text-to-speech

## Project Structure

```text
.
|-- main.py
|-- requirements.txt
|-- core/
|-- detectors/
|-- ml_models/
|   `-- pose_landmarker_full.task
|-- services/
|   |-- auth/
|   |-- coaching/
|   |-- config/
|   |-- persistence/
|   |-- state/
|   |-- tracking/
|   |-- ui/
|   `-- vision/
|-- statics/
`-- .streamlit/
```

## Setup

1. Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install dependencies:

```powershell
pip install -r requirements.txt
```

3. Add your environment variables in `.env`:

```env
GROQ_API_KEY=your_groq_api_key_here
```

The Groq key is used for AI coaching feedback. The core video tracking app can still be developed locally without committing `.env`.

## Run

```powershell
streamlit run main.py
```

Then open the local Streamlit URL in your browser, enter a username, choose an exercise plan in the sidebar, and start the workout to enable camera-based tracking.

## Deploy on Streamlit Community Cloud

This project includes `packages.txt` for Linux runtime libraries needed by OpenCV/MediaPipe on Streamlit Community Cloud.

The requirements are set up for Streamlit Cloud's Python 3.14 environment. If you deploy with an older Python version, recreate the environment and reinstall dependencies from `requirements.txt`.

Add your Groq key in the app's Streamlit secrets:

```toml
GROQ_API_KEY = "your_groq_api_key_here"
```

If Groq or text-to-speech is temporarily unavailable, the app will continue running and show text coaching fallback messages.

## Notes

- `data.db` is created locally for user and exercise history and is ignored by Git.
- `ml_models/pose_landmarker_full.task` is required by the video processor and should stay available in the project.
- Streamlit theme settings live in `.streamlit/config.toml`.
