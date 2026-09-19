# Freeze: Video Content Search Engine

**Freeze** is a video content search engine designed to analyze and extract insights from video using object detection, classification, and scene segmentation. The tool features an Apple Silicon-accelerated pipeline utilizing YOLO models and a Streamlit interactive interface.

<img width="80%" alt="FREEZE-Poster-1" src="https://github.com/user-attachments/assets/1ba47d03-7971-4a39-8bae-3890f2d347e0" />


---

## Core Features

- **Video Upload and Processing**: Upload videos for automatic analysis.
- **Object Detection**: YOLOv8 identifies objects in video frames.
- ⭐️**Performance Optimization**⭐️: Apple Silicon-accelerated pipeline with PyTorch MPS and CoreML exports.
- **Scene Segmentation**: Identifies scene changes using `scenedetect` for better content organization.
- **Database Integration**: Saves video metadata to a PostgreSQL database for querying and retrieval.
- **Interactive Web Interface**: Streamlit-powered UI for uploading videos, viewing results, and interacting with the system.

---

## Requirements

### Python Packages

Install these required Python libraries:

- `streamlit`: For building the interactive web application.
- `ultralytics`: To utilize YOLO models for object detection.
- `opencv-python-headless`: For processing video files.
- `scenedetect`: For detecting scene transitions in videos.
- `psycopg2`: For PostgreSQL database integration.
- `moviepy`: For advanced video processing.
- `torch`: PyTorch library for backend computations.
- `tqdm`: For progress bar display during video processing.

### Additional Tools

- **PostgreSQL**: Database management system for storing video metadata.
- **FFmpeg**: Required for video processing by MoviePy and OpenCV. Install it using your system's package manager:
  - On macOS: `brew install ffmpeg`
  - On Ubuntu/Debian: `sudo apt install ffmpeg`
  - On Windows: Download from [FFmpeg](https://ffmpeg.org).

---

## Setting up PostgreSQL

### Step 1: Install PostgreSQL
- **On macOS**: Use Homebrew:
  ```bash
  brew install postgresql
  brew services start postgresql
  ```
- **On Ubuntu/Debian**:
  ```bash
  sudo apt update
  sudo apt install postgresql postgresql-contrib
  ```
  Start PostgreSQL:
  ```bash
  sudo systemctl start postgresql
  ```
- **On Windows**: Download and install from the [official PostgreSQL website](https://www.postgresql.org/download/).

### Step 2: Configure PostgreSQL Database
1. Open the PostgreSQL shell or use a database client like pgAdmin.
2. Create a new user with a password:
   ```sql
   CREATE USER video_user_1 WITH PASSWORD 'user1password';
   ```
3. Create a database:
   ```sql
   CREATE DATABASE video_metadata;
   ```
4. Grant the user access to the database:
   ```sql
   GRANT ALL PRIVILEGES ON DATABASE video_metadata TO video_user_1;
   ```

### Step 3: Update Database Details
Update the database connection details in `streamlit3_location.py`:

```python
DB_HOST = "localhost"
DB_NAME = "video_metadata"
DB_USER = "video_user_1"
DB_PASS = "user1password"
```

---
## Pixi
If you haven't installed Pixi, I recommend using it to manage your environment rather than the standard Python venv.
> **Learn More:** [Read about latest Pixi, installation steps for Windows, and how it compares to other tools](https://pixi.prefix.dev/latest/).
1. To install pixi on MacOS/Linux, run:
```bash
curl -fsSL https://pixi.sh/install.sh | bash
```
Restart your terminal.

2. Confirm:
```bash
pixi --version
```
*(You should see the installed Pixi version printed in the terminal.)*

## Run the App

1. Clone the repository:
   ```bash
   git clone git@github.com:brittho/freeze-video-vision.git
   cd freeze-video-vision
   ```
2. Initialize a Pixi workspace:
   ```bash
   pixi init freeze-ws
   cd freeze-ws
   ```
4. Add Your Dependencies:
   ```
   pixi add streamlit opencv ultralytics tqdm psycopg2 moviepy pytorch torchvision
   ```
   <img width="621" height="105" alt="image" src="https://github.com/user-attachments/assets/4d456547-d673-442f-906c-cd1e3a8c20a8" />

   ```
   pixi add --pypi scenedetect
   ```
5. Launch the Streamlit app:
   ```
   pixi shell
   streamlit run streamlit3_location.py
   ```
4. Upload a video file in the app and view results.

---

## Directory Structure

```
.
├── yolo_models/
│   └── YOLOv8x.pt          # YOLO model weights
├── streamlit3_location.py  # Main Streamlit application
├── pyscene_optimized_location.py  # Backend video processing
├── requirements.txt        # Python dependencies
└── README.md               # Documentation
```

---

## Troubleshooting

- Ensure PostgreSQL is running before launching the app.
- Check the YOLO model weights path and file name (`yolo_models/YOLOv8x.pt`).
- If FFmpeg errors occur, verify its installation using `ffmpeg -version`.

---

## Contributors

- **Britt** - Developer and Project Lead
