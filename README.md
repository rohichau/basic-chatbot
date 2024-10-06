# Chatbot Project
This project contains two main components:

* Backend: A Flask API located in the /backend directory.
* Frontend: A React JS application located in the /frontend/chatbot directory.
The project is containerized using Docker Compose for easy setup and management of both the backend and frontend services.

## Prerequisites
Before starting, ensure you have the following installed:

* Docker
* Docker Compose

## Project Structure
```
/backend                # Flask API backend
  ├── app.py            # Main Flask application
  ├── requirements.txt  # Python dependencies
  ├── Dockerfile        # Dockerfile for backend
  └── ...               # Other backend files

/frontend/chatbot       # React JS frontend application
  ├── package.json      # Node.js dependencies
  ├── src/              # Frontend source code
  ├── Dockerfile        # Dockerfile for frontend
  └── ...               # Other frontend files

docker-compose.yml      # Docker Compose configuration
README.md               # This README file
```

# Getting Started
## Step 1: Clone the Repository
git clone https://github.com/yourusername/yourproject.git
cd yourproject

## Step 2: Set Up Environment Variables (Optional)
If your Flask backend or React frontend requires any specific environment variables, you can create an .env file in the root of the project. Here’s an example for the backend:
```
#Example .env for backend
FLASK_ENV=development
SECRET_KEY=your_secret_key
```
## Step 3: Build and Start the Services
Using Docker Compose, you can build and run both the backend and frontend services with a single command:
```
docker-compose up --build
```

This will:

* Build and run the Flask backend on port 5000.
* Build and run the React frontend on port 3000.

#### Running in Detached Mode
To run the services in detached mode (in the background), you can use:

```
docker-compose up --build -d
```

## Step 4: Access the Applications
Once the containers are up and running, you can access the applications:

* Backend (Flask API): http://localhost:5000
* Frontend (React App): http://localhost:3000

## Step 5: Stopping the Services
To stop the running services, use:

```
docker-compose down
```

This will stop and remove the containers but keep the Docker images.

# Detailed Setup Information

## Backend Setup
The backend is a Flask API built in Python. It has a few dependencies listed in the requirements.txt file, including spaCy. The Docker setup automatically installs these dependencies and downloads the en_core_web_md model, which is necessary for NLP processing.

1. Install Dependencies: The backend container automatically installs the required Python packages from requirements.txt and downloads the spaCy language model using the command:
```
python -m spacy download en_core_web_md
```

2. Start the Backend: The backend is started using the following command inside the Docker container:
```
flask run --host=0.0.0.0
```

3. Ports: The backend is exposed on port 5000. You can access the API at http://localhost:5000.

## Frontend Setup
The frontend is a React JS application. It uses npm to manage dependencies and start the development server.

1. Install Dependencies: The frontend container automatically installs the necessary Node.js dependencies by running:
```
npm install
```

2. Start the Frontend: The frontend is started using the following command inside the Docker container:
```
npm start
```

3. Ports: The frontend runs on port 3000. You can access the React app at http://localhost:3000.

### Volumes
Both the backend and frontend services are set up to use Docker volumes. This means that any code changes you make in your local environment are automatically reflected inside the running containers without needing to rebuild the images.

* Backend files are mapped to /app inside the backend container.
* Frontend files are mapped to /app inside the frontend container.

# Troubleshooting
* If the containers don't start properly, ensure that Docker and Docker Compose are installed and running.

* If the frontend or backend code changes are not reflected, try restarting the services:
```
docker-compose restart
```

* To view logs, use:

```
docker-compose logs -f
```

* If you face an issue with ports, ensure no other services are running on ports 3000 and 5000. You can modify the ports in the docker-compose.yml file if needed.

# Future Enhancements
* Add testing framework for backend and frontend.
* Setup CI/CD pipeline for automatic deployment.
* Implement additional security measures like HTTPS.
