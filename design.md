# InSightX – System Design Document

---

## 1. System Overview

InSightX is a multi-modal AI-based video analysis platform designed to extract structured insights from social media videos.

The system integrates:
- Computer Vision
- Speech Processing
- Natural Language Processing
- Cloud Infrastructure

The architecture follows a modular pipeline approach to ensure scalability and maintainability.

---

## 2. High-Level Architecture

User Interface  
↓  
Backend API Layer  
↓  
Video Processing Module  
↓  
AI Processing Layer  
↓  
Insight Aggregation Engine  
↓  
Results Dashboard  

---

## 3. Component Design

### 3.1 Frontend Layer

- Built using React / HTML-CSS
- Accepts video link or upload
- Displays structured results in dashboard format
- Communicates with backend via REST APIs

---

### 3.2 Backend API Layer

- Implemented using FastAPI / Flask
- Handles:
  - Video download
  - Request validation
  - Model orchestration
  - Response formatting

---

### 3.3 Video Processing Module

Responsibilities:
- Download video from provided URL
- Extract frames using OpenCV
- Extract audio using MoviePy
- Store temporary data in cloud storage

---

### 3.4 AI Processing Layer

This layer consists of independent modules:

#### Face Detection Module
- Uses MTCNN or AWS Rekognition
- Detects and crops faces from frames
- Optional recognition using trained embeddings

#### Outfit Classification Module
- CNN-based classifier (ResNet)
- Identifies clothing type and dominant colors
- Generates style category suggestions

#### Speech Processing Module
- Uses Whisper or AWS Transcribe
- Converts extracted audio into text transcript

#### NLP Summarization Module
- Uses Transformer model (BART/T5)
- Generates concise summary from transcript

#### Mood & Scene Detection Module
- Scene classification model
- Emotion tone estimation

---

## 4. Data Flow

1. User submits video link.
2. Backend downloads video and stores in S3.
3. Video frames and audio are extracted.
4. AI models process:
   - Frames (vision tasks)
   - Audio (speech-to-text)
5. NLP model generates summary.
6. All outputs are aggregated.
7. Structured response sent to frontend.
8. Results displayed to user.

---

## 5. Cloud Architecture (AWS Integration)

- Amazon S3 → Video storage
- Amazon EC2 → Backend hosting
- Amazon SageMaker → Model deployment
- Amazon Rekognition → Face detection
- Amazon Transcribe → Speech-to-text
- DynamoDB / PostgreSQL → Metadata storage

---

## 6. Scalability Strategy

- Modular microservice architecture
- Independent model scaling
- Cloud-based deployment
- Horizontal scaling via load balancer
- Containerization (Docker) support

---

## 7. Security Considerations

- Secure REST API endpoints
- Temporary video storage with auto-deletion
- Encrypted cloud storage
- Role-based cloud access control

---

## 8. Performance Optimization

- Frame sampling instead of processing full video
- Asynchronous processing for large videos
- Caching frequent model outputs
- GPU acceleration for model inference

---

## 9. Future Enhancements

- Real-time live stream analysis
- Multi-language summarization (Indian languages)
- Influencer analytics dashboard
- Fashion recommendation integration with e-commerce APIs
