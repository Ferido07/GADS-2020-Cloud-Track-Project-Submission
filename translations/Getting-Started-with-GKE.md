# Google Cloud Fundamentals: Getting Started with GKE

### Objectives  
  - In this lab, you learn how to perform the following tasks:
  - Provision a Kubernetes cluster using Kubernetes Engine.
  - Deploy and manage Docker containers using kubectl.


#### Task 1: Confirm that needed APIs are enabled  
  - Run the following command and confirm that both Kubernetes Engine API and Container Registry API are enabled:  
        `gcloud services list`  
     If they are not on the list run the following command to enable them:  
     For Kubernetes Engine API  
        `gcloud services enable container.googleapis.com`  
     For Container Registry API   
        `gcloud services enable containerregistry.googleapis.com` 

#### Task 2: Start a Kubernetes Engine cluster  
  - Place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command: 
        `export MY_ZONE=`
     followed by the zone that Qwiklabs assigned to you. Your complete command will look similar to this:  
        `export MY_ZONE=us-central1-a`

  - Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster `webfrontend` and configure it to run 2 nodes:  
        `gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2`

  - After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
        `kubectl version`

  - View your running nodes  
        `gcloud compute instances list`


#### Task 3: Run and deploy a container  

  - From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)  
        `kubectl create deploy nginx --image=nginx:1.17.10`

  - View the pod running the nginx container:  
        `kubectl get pods`

  - Expose the nginx container to the Internet:  
        `kubectl expose deployment nginx --port 80 --type LoadBalancer`

  - View the new service:  
        `kubectl get services`

  - You can use the displayed external IP address to test and contact the nginx container remotely  
        `curl http://EXTERNAL_IP`

  - Scale up the number of pods running on your service:  
        `kubectl scale deployment nginx --replicas 3`

  - Confirm that Kubernetes has updated the number of pods:  
        `kubectl get pods`

  - Confirm that your external IP address has not changed:  
        `kubectl get services`

  - To confirm that the nginx web server is still responding run:  
        `curl http://EXTERNAL_IP`
