## Helmet Violation Alert System

Real-time safety enforcement using YOLOv8 for helmet detection and `face_recognition` for identity. When a person is detected without a helmet, the system identifies them and emails a challan (fine notice) to their registered address.

## Features

- Helmet detection with YOLOv8
- Face recognition from one image per person
- Automated email challan via SendGrid
- Simple CSV-based student registry
- Modular scripts for helmet-only or face-only testing

## Project Layout

- [main.py](main.py): Combined helmet + face workflow and email alerting
- [helmetdetection.py](helmetdetection.py): Helmet-only YOLO demo
- [face_de.py](face_de.py): Face recognition demo
- [student_data.csv](student_data.csv): Student roll number to email mapping

## Requirements

- Windows with a webcam
- Python 3.10 or 3.11 recommended (best support for `dlib`/`face_recognition`)
- A trained YOLOv8 model file `best.pt` in the project root
- SendGrid account and verified sender email

## Setup

1. Create a virtual environment.
   ```bash
   py -3.11 -m venv .venv
   .venv\Scripts\activate
   ```
2. Install dependencies.
   ```bash
   pip install -r requirements.txt
   pip install sendgrid
   ```
   Note: On Python 3.13, `dlib`/`face_recognition` may fail to install.

## Configuration

1. Add known faces in a folder (one PNG per student, named by roll number).
   - Example: `C:\Users\known_faces\21CS001.png`
2. Update paths and keys in [main.py](main.py):
   - `KNOWN_FACES_DIR`
   - `SENDGRID_API_KEY`
   - `FROM_EMAIL`
3. Update [student_data.csv](student_data.csv) with columns:
   - `Roll Number`
   - `Email`

## Run

```bash
python main.py
```

Optional demos:

```bash
python helmetdetection.py
python face_de.py
```

## Notes

- The email is sent after a continuous 5-second violation window per person.
- If you see install errors for `dlib`, use Python 3.10/3.11 and reinstall.
- `student_data.csv` currently contains placeholder text; replace with real data.
