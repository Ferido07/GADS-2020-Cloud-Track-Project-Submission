# Google Cloud Fundamentals: Getting Started with Compute Engine

### Objectives
In this lab, you will learn how to perform the following tasks:  
  - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
  - Create a Compute Engine virtual machine using the gcloud command-line interface.
  - Connect between the two instances.

#### Task 1 - Create a Compute Engine Virtual Machine my-vm-1 using the gcloud command-line interface.
```
        gcloud compute instances create my-vm-1 --zone=us-central1-a --machine-type=e2-medium --subnet=default --tags=http-server --image=debian-9-stretch-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=my-vm-1 
        gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server
```

#### Task 2 - Create a Compute Engine Virtual Machine my-vm-2 using the gcloud command-line interface.
```
        gcloud config set compute/zone us-central1-b
        gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"
```

#### Task 3 - Connect between the two instances.
  - Connect to my-vm-2:  
        `gcloud compute ssh my-vm-2`

  - Ping my-vm-1 from my-vm-2  
        `ping my-vm-1`

  - Use the ssh command to open a command prompt on my-vm-1 from my-vm-2  
        `ssh my-vm-1`

  - At command prompt on my-vm-1, install the ngix web server  
        `sudo apt-get install nginx-light -y`

  - Use nano text editor to add a custom message to the home page of the web server  
        `sudo nano /var/www/html/index.nginx-debian.html`

  - Use arrow keys to add text like this below the h1 tag, and replace YOUR_NAME with your name  
        `Hi from YOUR_NAME`

  - Exit the editor and confim your server is servering your new page  
        `curl http://localhost/`  
        result will be the html source of the web server home page with your custom text

  - To exit the command prompt on my-vm-1, execute this command:  
        `exit`

  - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:  
        `curl http://my-vm-1/`  
        result will again be the HTML source of the web server's home page, including your line of custom text
    
  - Get the External IP address for my-vm-1 instance by running  
        `gcloud compute instances list --zones us-central1-a`
    
  - Open a new browser tab and paste the external IP  
        result will again be the HTML source of the web server's home page, including your line of custom text
        