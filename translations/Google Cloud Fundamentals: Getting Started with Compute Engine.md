# LAB: GCP Fundamentals: Getting Started with Compute Engine
 
## Objectives

In this lab, you will learn how to perform the following tasks:

   - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
   - Create a Compute Engine virtual machine using the gcloud command-line interface.
   - Connect between the two instances.

## Steps:

1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console
        
        gcloud compute instances create --zone=us-central1-a --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http

        gcloud compute firewall-rules create myruler --action= ALLOW --direction=INGRESS --rules=http:80 --target-tags=http

        
2. Create a Compute Engine virtual machine using the gcloud command-line interface
      
      To set your default zone to the one you just chose, enter this partial command gcloud config set compute/zone followed by the zone you chose:

       gcloud config set compute/zone us-central1-b

       To create a VM instance called my-vm-2 in that zone, execute this command:

       gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image"debian-9-stretch-v20190213" --subnet "default"

3. Connect between the two instances
   
   1. To open a command prompt on the my-vm-2 instance:

    gcloud compute ssh my-vm-2


   2. Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:

        ping  -c 5 my-vm-1

   3. Use the ssh command to open a command prompt on my-vm-1:

        ssh my-vm-1

   5. At the command prompt on my-vm-1, we install the Nginx web server:

         sudo apt-get install nginx-light -y

   6.  Use the arrow keys to move the cursor to the line just below the h1 header.Add text like this, and replace YOUR_NAME with your name:
        
        Hi from BERNARD

   7. We save and exit the nano editor and then we confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
        
        curl http://localhost/

       Results: The result will be the HTML source of the web server's home page,including your line of custom text.

    8. To exit the command prompt on my-vm-1, execute this command:

        exit

    9. To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

       curl http://my-vm-1/

       Results: Again,the result will be the HTML source of the web server's home page,including your line of custom text.

    10. we need to get the external ip of my-vm-1 so we list first the instances:

          gcloud compute instances list --zone=us-central1-a

    11. We copy the external IP of my-vm-1 and we paste it in a new browser windows and hit enter:

         Results: we see the web server's page home page that include your line of custom text.
     
# END OF THE LAB