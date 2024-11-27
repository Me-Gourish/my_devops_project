# Base Image: Use a Linux base image with Python and Jenkins dependencies
FROM python:3.9-slim

# Install required tools
RUN apt-get update && \
    apt-get install -y openjdk-11-jre git curl docker.io && \
    apt-get clean

# Install Jenkins CLI (optional if required for scripting)
RUN curl -L https://updates.jenkins.io/download/war/2.414.3/jenkins.war -o /jenkins.war

# Copy the Flask app files into the container
WORKDIR /app
COPY web-app/ ./web-app/

# Install Python dependencies for the Flask app
RUN pip install --no-cache-dir -r web-app/requirements.txt

# Copy the Jenkins pipeline file (Jenkinsfile)
WORKDIR /jenkins-pipeline
COPY Jenkinsfile ./app

# Install Docker CLI permissions for Jenkins
RUN groupadd docker && useradd -m -s /bin/bash jenkins && \
    usermod -aG docker jenkins

# Expose ports for Flask (5000) and Jenkins (8080)
EXPOSE 5000 8080

# Start a shell with everything installed
CMD ["bash"]
