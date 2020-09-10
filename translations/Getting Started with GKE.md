# LAB: Google Cloud Fundamentals: Getting Started with GKE

## Objectives
   In this lab, you learn how to perform the following tasks:
   - Provision a Kubernetes cluster using Kubernetes Engine.
   - Deploy and manage Docker containers using kubectl.

## Steps
  1.  Start a Kubernetes Engine cluster:
      1. At the Cloud Shell prompt,we place the zone that Qwiklabs assigned us to into an environment variable called MY_ZONE:
        export MY_ZONE=us-central1-a

      2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
         gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

         Results:
                     NAME         LOCATION       MASTER_VERSION  MASTER_IP       MACHINE_TYPE   NODE_VERSION   NUM_NODES  STATUS
					webfrontend  us-central1-a  1.15.12-gke.2   104.197.37.151  n1-standard-1  1.15.12-gke.2  2          RUNNING

	  3. After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

         kubectl version

  2. Run and deploy a container:

      1. From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.):

         kubectl create deploy nginx --image=nginx:1.17.10

         Results: deployment.apps/nginx created

      2. View the pod running the nginx container:

          kubectl get pods

          Results: 
                    NAME                     READY   STATUS    RESTARTS   AGE
					nginx-5f7d5d7689-9q7bw   1/1     Running   0          12s

	  3. Expose the nginx container to the Internet:

	      kubectl expose deployment nginx --port 80 --type LoadBalancer

	      Results:  service/nginx exposed

	   4. View the new service:

	       kubectl get services

	       Results: 
	                NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)        AGE
					kubernetes   ClusterIP      10.51.240.1     <none>           443/TCP        3m32s
					nginx        LoadBalancer   10.51.240.247   130.211.118.90   80:30667/TCP   52s

       5. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

       6. Scale up the number of pods running on your service:

         kubectl scale deployment nginx --replicas 3

         Results: deployment.extensions/nginx scaled

       7. Confirm that Kubernetes has updated the number of pods:

          kubectl get pods

          Results: 
          			NAME                     READY   STATUS    RESTARTS   AGE
					nginx-5f7d5d7689-9q7bw   1/1     Running   0          2m25s
					nginx-5f7d5d7689-cf4sf   1/1     Running   0          20s
					nginx-5f7d5d7689-zxbk7   1/1     Running   0          20s
       
       8. Confirm that your external IP address has not changed:

          kubectl get services

          Results: 	NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)        AGE
					kubernetes   ClusterIP      10.51.240.1     <none>           443/TCP        4m50s
					nginx        LoadBalancer   10.51.240.247   130.211.118.90   80:30667/TCP   2m10s
       9. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.

# END OF THE LAB







