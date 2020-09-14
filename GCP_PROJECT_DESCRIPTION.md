## PROJECT DESCRIPTION

- In one organization there are multiple teams, like the development team, production team, etc. So create two projects one for the production team (prod_project) and one project for the development team (dev_project).

- Create VPC in two different regions for both the projects. VPC for dev team is in the Singapore region and VPC for Prod team is in the US region. Establish a connection between two VPC's using VPC peering.

- Create a Kubernetes cluster in Dev VPC where developers can create and host their front end PHP application. Also due to data regulatory compliance, we don't want our production team data to go out form the US. So create SQL DB in Production VPC.

- Configure one External Load Balancer to manage the load when the client hits the website.

- Connect MySQL database to the web application running in the Kubernetes cluster. So a client can see the website but data is coming from database running in the US.

- The complete infrastructure is built on Google Cloud Platform.

### Pre-requisites:

- You must have your GCP account verified. Go to this link, https://console.cloud.google.com/, create your account and verify your credit card.

- To login using CLI and use gloud command, you must have gcloud SDK installed. Go to https://cloud.google.com/sdk/docs/quickstart-windows and install.

- You must have Kubectl program installed in your system. Go to https://kubernetes.io/docs/tasks/tools/install-kubectl/ and install it.

### STEPS:

- Create two projects, devproject and prodproject, from CLI using gcloud command.

```
    gcloud projects create devproject-1029384756 --name=devproject

    gcloud projects create prodproject-1029384756 --name=prodproject
    
```

  ![](/screenshots/Screenshot(56).png)


- Enable billing for both projects. Go to billing section and set billing account.


  ![](/screenshots/Screenshot(57).png)


  ![](/screenshots/Screenshot(58).png)


- Create VPC in both brojects. In devproject create VPC in Singapore region. In prodproject create vpc in US region.


  ![](/screenshots/Screenshot(60).png)


  ![](/screenshots/Screenshot(61).png)


- Enable VPC network peering in both the VPC's to connect both the VPC's.As soon as you enable VVPC peering in both the projects, the status turns active.


  ![](/screenshots/Screenshot(63).png)


  ![](/screenshots/Screenshot(64).png)


  ![](/screenshots/Screenshot(66).png)


- In dev project create Kubernetes cluster using GKE(Google Kubernetes Engine) service.


  ![](/screenshots/Screenshot(67).png)
  
  
  1.1 Select Kubernetes Engine service on console. Go to Node pools and set size=1. And in Node-pools select Nodes and set machine configuration series as N1.
  
  
  ![](/screenshots/Screenshot(69).png)
  
  
  ![](/screenshots/Screenshot(70).png)
  
  
  1.2 Next Give cluster a name, Location type=Regional and select asia-southeast-1 (Singapore) region and select all the zones [1a,1b,1]. Click on create cluster.
  
  
  ![](/screenshots/Screenshot(68).png)
  
  
  1.3 After cluster is created click on connect and copy gcloud command and run in your local system command prompt. This will update kubeconfig file. Now you can connect to your kubernetes cluster using kubectl command. To test connectivity with cluster type this command:
  
  
  ![](/screenshots/Screenshot(71).png)
  
  
  ![](/screenshots/Screenshot(72).png)
  
  
  ![](/screenshots/Screenshot(73).png)
  
  
  ```
  kubectl.exe get pods -o wide
  
  ```
  1.4 Create a deployment using wordpress image. Expose deployment so that outside world can connect to cluster and also for scaling through load balancing.
  
  ```
  kubectl create deployment myweb1 --image=wordpress
  
  kubectl expose deploy myweb1 --type=LoadBalancer --port=80
  
  kubectl get services   //to get external IP so that outside users can hit to this IP and connect to website
  
  ```
  
  
  ![](/screenshots/Screenshot(74).png)
  
  
  
- In prod project, select SQL service to create MYSQL database for our front end application. Give instance id, set passowrd and region where you want to launch your MYSQL database.


![](/screenshots/Screenshot(75).png)


  ![](/screenshots/Screenshot(76).png)


  ![](/screenshots/Screenshot(77).png)


- Then go to Databases and create a database. Also go to Overview --> edit Configuration --> Connectivity --> add network --> add 0.0.0.0/0 CIDR. 


  ![](/screenshots/Screenshot(83).png)


- Copy external IP from CLI and paste in browser. Then enter db_name (which you created inside MYSQL DB server, db_password, username as root and Database Host as publicIp. If you see this page, you have successfully connected your database with wordpress application. Click on run the installation.


  ![](/screenshots/Screenshot(84).png)


- Give title, username, copy passoword to notepad as it won't be accessible later, and give email id. Click on install wordpress.


  ![](/screenshots/Screenshot(85).png)
  

Congracts..!! You have successfully deployed your front-end app on Kubernetes cluster running in Singapore region and the database is hosted in US South California region. So all the data is coming from US and Singapore clients can access my website. Although app is deployed on Kubernetes cluster, but internally GKE service contacted to GCE (Google Compute Engine) and launch our app on Compute instances.


  ![](/screenshots/Screenshot(86).png)


### Concepts Learned and Integrated:

- GCE (Google Compute Engine)
- GKE (Google Kubernetes Engine)
- SQL (MYSQL Database service)
- VPC (Virtual Private Network) and VPC Network Peering
- Projects, Regions, Zones, firewall rules
 
