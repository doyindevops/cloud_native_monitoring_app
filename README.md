README

ITS GETTING BETTER
TESTING FOR BUILD IN JENKINS

 Python application deployed to run in Docker container


(Things to have before starting the projects)

- [x]  AWS Account.
- [x]  Programmatic access and AWS configured with CLI.
- [x]  Python3 Installed.
- [x]  Docker and Kubectl installed.
- [x]  Code editor (Vscode)


PROJECT STEPS
Part 1: Deploying the Flask application locally

Step 1: Clone the code

Clone the code from the repository:

git clone <repository_url>


### **Step 2: Install dependencies**

The application uses the **`psutil`** and **`Flask`, Plotly, boto3** libraries. Install them using pip:


pip3 install -r requirements.txt


### **Step 3: Run the application**

To run the application, navigate to the root directory of the project and execute the following command:


$ python3 app.py


This will start the Flask server on **`localhost:5000`**. Navigate to [http://localhost:5000/](http://localhost:5000/) on your browser to access the application.

## **Part 2: Dockerizing the Flask application**

### **Step 1: Create a Dockerfile**

Create a **`Dockerfile`** in the root directory of the project with the following contents:


Use the official Python image as the base image
FROM python:3.9-slim-buster

Set the working directory in the container
WORKDIR /app

Copy the requirements file to the working directory
COPY requirements.txt .

RUN pip3 install --no-cache-dir -r requirements.txt

Copy the application code to the working directory
COPY . .

Set the environment variables for the Flask app
ENV FLASK_RUN_HOST=0.0.0.0

Expose the port on which the Flask app will run
EXPOSE 5000

Start the Flask app when the container is run
CMD ["flask", "run"]


### **Step 2: Build the Docker image**

To build the Docker image, execute the following command:


$ docker build -t <image_name> .


### **Step 3: Run the Docker container**

To run the Docker container, execute the following command:


$ docker run -p 5000:5000 <image_name>


This will start the Flask server in a Docker container on **`localhost:5000`**. Navigate to [http://localhost:5000/](http://localhost:5000/) on your browser to access the application.

## **Part 3: Pushing the Docker image to ECR**

### **Step 1: Create an ECR repository**

Create an ECR repository using Python:


import boto3

Create an ECR client
ecr_client = boto3.client('ecr')

Create a new ECR repository
repository_name = 'my-ecr-repo' response = ecr_client.create_repository(repositoryName=repository_name)

Print the repository URI
repository_uri = response['repository']['repositoryUri'] print(repository_uri)


### **Step 2: Push the Docker image to ECR**

Push the Docker image to ECR using the push commands on the console:

