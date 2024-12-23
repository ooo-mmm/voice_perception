# Voice Perception System

A voice analytics system based on Vosk for call center analysis and speech processing.

![Main Interface](https://github.com/bogdal1993/voice_perception/blob/main/Annotation%202023-08-29%20210405.jpg?raw=true "Main Interface")

## Core Features

1. Automated Call Recognition
2. Mono Call Diarization (Speaker Separation)
3. Phrase-level Emotion Detection
4. Comprehensive Call Reporting
5. Full-text Call Search Capabilities
6. **Dialog Summarization using Mistral 7B LLM**
7. **Automatic Topic Detection**

## System Components

### Prerequisites
- PostgreSQL Database
- Docker and Docker Compose
- Nginx Web Server

## Installation Guide

### Database Setup
1. Install PostgreSQL database
2. Execute the initialization script: `initial.sql`

### Worker Node Configuration

1. Navigate to the worker node directory:
```bash
cd worker_node
```

2. Configure database connection in `docker-compose.yml`:
Replace the DSN parameter:
```yaml
postgresql://user:pass@host:port/db
```
with your database credentials.

3. Configure VOSK server:
- Set `VOSK_SERVER` to your machine's address
- Or replace `127.0.0.1` with `vosk` for local deployment

4. Download Required Models:

Navigate to the vosk directory:
```bash
cd vosk
```
Download and extract Vosk models using the links provided in `loadvosk.txt`

Navigate to the text processor directory:
```bash
cd text_processor/ruword2tags
```
Download `ruword2tags.db` using the link in `load.txt`

5. Launch the worker node:
```bash
docker-compose up -d
```

### Web Node Setup

1. Install and configure Nginx using the provided `default` configuration file
2. For distributed deployment, update the proxy_pass directives in the location sections with correct service addresses
3. For separate web node deployment, update the external address in `docker-compose.yml`:
```yaml
APIURL: "http://127.0.0.1/api/file/"
```

### LLM Node Setup

1. Download the language model:
```bash
./llm_node/summarization_server/load_model.sh
```

2. Launch the LLM server:
```bash
docker-compose up -d
```

## Audio File Upload

Two methods are available for uploading audio files:
1. Using the web interface upload form
2. Using the API endpoint (example provided in `load.curl`)

## Interface Screenshots

### Main Call Analysis Interface
![Main Interface](https://github.com/bogdal1993/voice_perception/blob/main/Annotation%202023-04-30%20143825.jpg?raw=true "Main Call Analysis Interface")

### Analytics Dashboard
![Analytics Dashboard](https://github.com/bogdal1993/voice_perception/blob/main/Annotation%202023-04-30%20143822.jpg?raw=true "Analytics Dashboard")

### Text Search Interface
![Search Interface](https://github.com/bogdal1993/voice_perception/blob/main/Annotation%202023-04-30%20143821.jpg?raw=true "Text Search Interface")

## Technology Stack

The system integrates several powerful models:
- Vosk (Speech Recognition)
- DeepPavlov (NLP Tasks)
- I.Koziev's Models
- Mistral 7B (Text Summarization)

## Community

Join our community for discussions and support:
- Telegram: https://t.me/voiceperce

## License

This project is open-source and available under the MIT License.

## Acknowledgments

Special thanks to the creators and maintainers of:
- Vosk
- DeepPavlov
- Mistral AI
- I.Koziev's NLP Tools
