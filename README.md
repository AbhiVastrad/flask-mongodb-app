# flask-mongodb-app

This repository contains all necessary resources and instructions to deploy a Flask application with MongoDB on a Kubernetes cluster using Minikube.

## Prerequisites

Before you start, ensure you have the following installed on your local machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Getting Started

Step 1: Clone the Repository 

$ git clone https://github.com/AbhiVastrad/flask-mongodb-app.git
$ cd flask-mongodb-app

Step 2: Build and Push Docker Image

$ docker build -t flask-mongodb-app:latest .
$ docker push -t flask-mongodb-app:latest .

Step 3: Start Minikube cluster:

$ minikube start

Step 4: Deploy MongoDB
Create a Persistent Volume and Persistent Volume Claim:

Apply the mongodb-pv.yaml and mongodb-pvc.yaml:

$ kubectl apply -f mongodb-pv.yaml
$ kubectl apply -f mongodb-pvc.yaml

Deploy MongoDB using a StatefulSet:

$ kubectl apply -f mongodb-statefulset.yaml

Step 5: Deploy Flask Application
Deploy the Flask application:

$ kubectl apply -f flask-deployment.yaml

Expose the Flask application using a NodePort service:

$ kubectl apply -f flask-service.yaml

Step 6: Access the Flask Application
Get the Minikube IP address:

$ minikube ip

Access the application:

Navigate to http://<minikube-ip>:<node-port> in web browser. Replace <minikube-ip> with the IP address from the previous step, and <node-port> with the port number assigned to your service (usually 32181).

Step 7: Testing Autoscaling

Deploy Horizontal Pod Autoscaler (HPA):

$ kubectl apply -f hpa.yaml

###This `README.md` file is structured to guide users step-by-step through the deployment process###
