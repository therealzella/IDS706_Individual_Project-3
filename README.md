## Flask Project with Docker and Google Cloud Run ##

A simple Flask application with multiple API endpoints for various functionalities, fully containerized using Docker and deployed to Google Cloud Run.

![CI](https://github.com/therealzella/IDS706-python-github-template/actions/workflows/ci.yml/badge.svg)

### Features ###

- Dockerized Flask application for easy deployment.
- Hosted on Google Cloud Run for scalability and reliability.
- Includes endpoints for:
- Basic arithmetic operations.
- LLM-based text generation.
- Health check endpoint.
- Word cloud generation.
### Video demo link
```
https://youtu.be/144CNFthsOk
```
### Flask Website Link
```bash
https://flask-app-424823640221.us-east1.run.app
```


### Folder Structure
```bash
flask_project/
├── Dockerfile               # Docker configuration file
├── app.py                   # Main Flask application
├── requirements.txt         # Python dependencies
├── cloudbuild.yaml          # Google Cloud Build configuration
├── docker-compose.yml       # Docker Compose configuration
├── templates/
│   └── index.html           # HTML template for the Flask app
├── .gitignore               # Git ignore file
└── README.md                # Project documentation
```

### Setup and Installation
**Prerequisites**
1. Python 3.8+ installed on your local system.
2. Docker installed (Install Docker).
3. Google Cloud SDK installed (Install gcloud).

**Local Setup**
1. Clone this repository:
```bash
git clone https://github.com/yourusername/flask_project.git
cd flask_project
```
2. Install dependencies:
```bash
pip install -r requirements.txt
```
3. Run the Flask application locally:
```bash
python app.py
```
4. Access the application in your browser:
```arduino
http://localhost:8080
```
### Docker Setup
**Build and Run Locally**
1. Build the Docker image:
```bash
docker build -t flask-app .
```
2. Run the Docker container:
```bash
docker run -p 8080:8080 flask-app
```
3. Test the application: Access it in your browser: http://localhost:8080

### Google Cloud Run Deployment

**Step 1: Authenticate with Google Cloud**
Log in to Google Cloud:
```bash
gcloud auth login
```
Set your project:
```bash
gcloud config set project YOUR_PROJECT_ID
```
**Step 2: Build and Push the Docker Image**
Submit your container image to Google Container Registry:
```bash
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/flask-app
```
**Step 3: Deploy to Google Cloud Run**
Deploy your application:
```bash
gcloud run deploy flask-app \
    --image=gcr.io/YOUR_PROJECT_ID/flask-app \
    --platform=managed \
    --region=us-east1 \
    --allow-unauthenticated
```
**Step 4: Access the Application**
Once deployed, Google Cloud Run will provide a URL. Use it to access your app.

### API Endpoints

| Endpoint          | Method | Description                |
|-------------------|--------|----------------------------|
| `/`               | GET    | Welcome page              |
| `/health`         | GET    | Health check endpoint     |
| `/api/calculate`  | POST   | Perform calculations      |
| `/generate`       | POST   | Generate LLM-based text   |
| `/wordcloud`      | POST   | Generate word clouds      |

**Example Requests**
1. Health Check
```bash
curl http://localhost:8080/health
```
Response:
```bash
{
  "message": "The app is up and running!",
  "status": "healthy"
}
```
2. Arithmetic Operations
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"operation": "add", "num1": 10, "num2": 5}' \
http://localhost:8080/api/calculate
```
Response:
```
{
  "result": 15.0
}
```
3. Generate LLM-based Text
```
curl -X POST -H "Content-Type: application/json" \
-d '{"prompt": "Once upon a time"}' \
http://localhost:8080/generate
```
Response:
```
{
  "prompt": "Once upon a time",
  "response": "There was a brave knight..."
}
```
4. Generate Word Cloud
Upload a text file to generate a word cloud:
```
curl -X POST -H "Content-Type: multipart/form-data" \
-F "file=@yourfile.txt" \
http://localhost:8080/wordcloud
```
Response: Returns a word cloud image.
