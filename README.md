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

Step 3: Start Minikube cluster

$ minikube start

Step 4: Deploy MongoDB

Navigate to the kubernetes directory

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

Minikube Service Tunnel(optional):

$ minikube tunnel

This command will run in the foreground and requires administrative privileges. It creates a network route to expose services with type LoadBalancer and should allow you to access the service externally.

Access the application:

  Open new terminal and navigate to project root directory 
  
  1.Forward port 5000 on localhost to the Flask service:

  $ kubectl port-forward service/flask-service 5000:80

  2.Access the application by navigating to:

  http://localhost:5000

  Using the URL you can access the flask application

Step 7: Testing Autoscaling

Deploy Horizontal Pod Autoscaler (HPA):

$ kubectl apply -f hpa.yaml

###This `README.md` file is structured to guide users step-by-step through the deployment process###
