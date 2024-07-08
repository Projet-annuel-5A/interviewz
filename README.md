![Interviewz logo](images/interviewz.png)

## Overview
Interviewz is a comprehensive application designed to analyze sentiments detected from video interviews across different sources:
* Audio (voice tone and pitch)
* Text (dialogues)
* And video (facial expressions)
 
It uses advanced machine learning models to detect sentiments from the interview data.

## Modules
The application is divided into four main modules, each with a specific focus and functionality.

### 1. Middleware Module
**Purpose**: The Middleware module acts as an orchestrator, coordinating the processing tasks across the audio, text, and video modules.

**How It Works**:
- **Initialization**: The FastAPI app sets up the necessary routes and initializes CORS middleware.
- **Preprocessing Endpoint (`/preprocess`)**:
  - Receives session and interview IDs.
  - Initializes a `Process` class instance that manages the workflow.
  - Downloads audio files, performs diarization (speaker identification), and converts speech to text.
- **Prediction Endpoint (`/predict`)**:
  - Coordinates with external APIs for audio, text, and video analysis.
  - Aggregates results and updates the database.

**Key Components**:
- `app.py`: Defines the FastAPI application, routes, and the main processing logic.
- `Process` class: Handles downloading, preprocessing, and interfacing with other APIs for complete interview analysis.
- `utils/utils.py`: Provides utility functions for logging, file handling, and database interactions.

### 2. Audio Module
**Purpose**: The Audio module processes audio data to extract and analyze emotions.

**How It Works**:
- **Initialization**: Sets up the FastAPI application and model loading.
- **Audio Analysis Endpoint (`/analyse_audio`)**:
  - Fetches audio segments from the database.
  - Splits the audio into segments and predicts emotions using a deep learning model.
  - Updates the results in the database.

**Key Components**:
- `app.py`: Defines the FastAPI application and the main endpoint for audio analysis.
- `audioEmotions.py`: Contains the `AudioEmotions` class responsible for splitting audio and predicting emotions.
- `utils/utils.py`: Manages file operations, logging, and interactions with the Supabase database.

### 3. Text Module
**Purpose**: The Text module analyzes text data to detect emotional content.

**How It Works**:
- **Initialization**: Sets up the FastAPI application and model loading.
- **Text Analysis Endpoint (`/analyse_text`)**:
  - Fetches text data from the database.
  - Processes each text entry to predict emotions using an NLP model.
  - Updates the results in the database.

**Key Components**:
- `app.py`: Defines the FastAPI application and the main endpoint for text analysis.
- `textEmotions.py`: Contains the `TextEmotions` class responsible for processing text and predicting emotions.
- `utils/utils.py`: Provides utility functions for logging, file handling, and database interactions.

### 4. Video Module
**Purpose**: The Video module processes video data to detect emotions through facial recognition.

**How It Works**:
- **Initialization**: Sets up the FastAPI application and model loading.
- **Video Analysis Endpoint (`/analyse_video`)**:
  - Fetches video segments from the database.
  - Splits the video into frames and predicts emotions using facial recognition models.
  - Updates the results in the database.

**Key Components**:
- `app.py`: Defines the FastAPI application and the main endpoint for video analysis.
- `videoEmotions.py`: Contains the `VideoEmotions` class responsible for splitting video frames and predicting emotions.
- `utils/utils.py`: Manages file operations, logging, and interactions with the Supabase database.

## API Endpoints
### Middleware Module
- **GET /health**: Check the health status of the API.
- **POST /preprocess**: Preprocess the provided audio file.
- **POST /predict**: Start the complete processing of the audio data.

### Audio Module
- **GET /health**: Check the health status of the API.
- **POST /analyse_audio**: Process audio data to analyze emotions.

### Text Module
- **GET /health**: Check the health status of the API.
- **POST /analyse_text**: Process text data to analyze emotions.

### Video Module
- **GET /health**: Check the health status of the API.
- **POST /analyse_video**: Process video data to analyze emotions.

### Directory Structure
```plaintext
interviewz/
│
├── middleware/
│ ├── app.py
│ └── utils/
│   ├── process.py
│   ├── utils.py
│
├── audio/
│ ├── app.py
│ ├── audioEmotions.py
│ └── utils/
│   ├── models.py
│   ├── utils.py
│
├── text/
│ ├── app.py
│ ├── textEmotions.py
│ └── utils/
│   ├── models.py
│   ├── utils.py
│
├── video/
│ ├── app.py
│ ├── videoEmotions.py
│ └── utils/
│   ├── models.py
│   ├── utils.py
```

## Contact
For any questions, please contact the project maintainers at [contact@interviewz.online](mailto:contact@interviewz.online).