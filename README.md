Secure File Sharing System
Backend Assessment for EZ Works
This project is a secure file-sharing system implemented as part of the backend engineer assessment for EZ Works. You can find the live project at: TODO (This will be taken down after the assessment)
It provides an API for secure file upload, download, and management between two types of users: Operation Users and Client Users.

Features
Technology Stack
Framework: Flask
Database: MongoDB
Authentication: JWT (JSON Web Tokens)
File Type Detection: python-magic
The file type is determined not only by the file extension but also by analyzing its contents.
Security Considerations
File types are verified by content, not just extension
Download URLs are encrypted and have a short expiration time
User passwords are hashed before storage
API Endpoints
Authentication
POST /signup: Sign up a new user
GET /verify-email/<token>: Verify user's email
POST /login: Log in a user
File Operations
POST /upload: Upload a file (Operation Users only)
GET /files: List all uploaded files
GET /download/<file_id>: Generate a download link for a file
GET /secure-download/<token>: Download a file using a secure token
Future Improvements
Implement rate limiting
Add file encryption at rest
Implement more granular user permissions
Add logging and monitoring
Testing
To run the test suite:

pytest -v tests/
You can check out a previous pytest log at tests/test_results.log

View the postman tests run summary at assets/Secure File Sharing System.postman_test_run.json.
<img width="878" height="859" alt="image" src="https://github.com/user-attachments/assets/690f273e-ebde-46ee-8442-acab31bf10cc" />
You can also import the Postman collection at assets/Secure File Sharing System.postman_collection.json

Setup and Installation
Make sure you are using Python 3.12 or later.
These instructions will help you get set up with a local development environment

Clone the repository:
git clone : https://github.com/saruuuuuu/Secure-File-Sharing-System.git
cd Secure-File-Sharing-System
Set up a virtual environment:
python -m venv venv
./venv/Scripts/activate  # On Linux use `source venv\bin\activate`
Install dependencies:
pip install -r requirements.txt
pip install python-magic-bin~=0.4.14 # only for Windows 
sudo apt update && sudo apt install -y libmagic-dev # only for Linux
Set up environment variables:
Create a .env file in the root directory and add the following:
SECRET_KEY=your_secret_key
MONGO_URI=your_mongodb_uri
UPLOAD_FOLDER=path_to_upload_folder
SMTP2GO_API_KEY=your_smtp2go_api_key
SMTP2GO_SENDER='sender_name <sender_email>'
BASE_URL='' # specify the base URL of your application or leave empty for 127.0.0.1:5000
Run the application:
python run.py
Deployment
Follow these steps to deploy the application using Docker

Create a Dockerfile
Create a file named Dockerfile in the root directory of the project with the following content:

FROM python:3.12-slim
WORKDIR /SFSS
COPY . .
RUN pip install -r requirements.txt
RUN apt update && apt install -y libmagic-dev
RUN pip install waitress
RUN mkdir uploads
EXPOSE 5000
CMD ["waitress-serve", "--port=5000", "--call", "app:create_app"]
Create a .dockerignore file
Create a .dockerignore file in the root directory to exclude unnecessary files:

.idea/
venv/
.pytest_cache
*.pyc
__pycache__/
.git/
.gitignore
uploads/
tests/
README.md
Dockerfile
.dockerignore
Build the Docker image
Run the following command in your terminal:

sudo docker build -t sfss .
Run the Docker container
To run the container with a mounted volume, use:

sudo docker run --name sfss -d -p 5000:5000 -v $(pwd)/uploads:/uploads sfss
This command does the following:
-d: Runs the container in detached mode. This means the container will keep running in the background.
-p 5000:5000: Maps port 5000 of the host to port 5000 on the container.
-v $(pwd)/uploads:/uploads: Mounts the uploads directory from your current working directory to /uploads in the container

Access your application
The application should now be accessible at http://localhost:5000

Contributing
This project was created as part of an assessment. However, if you have suggestions or improvements, please feel free to open an issue or submit a pull request.


