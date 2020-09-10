## PROJECT DESCRIPTION

- In one organization there are multiple teams, like development team, production team, etc. So create two **projects** one for production team (prod_project) and one project for development team (dev_project).

- Create **VPC** in two different region for both the projects. VPC for dev team is in Singapore region and VPC for Prod team is in US region.Establish a connection between two VPC's using **VPC peering**.

- Create **kubernetes cluster** in Dev VPC where developers can create and host their **front end PHP application**. Also due to data regulatory compliance, we don't want our production team data to go out form USA. So create **SQL DB** in Production VPC.

- Configure one External Load Balancer to manage the load when client hits the website.

- Connect MySQL database to the web application running in Kubernetes cluster. So client can see the website but data is coming from database running in US.

- The complete infrastructure is build on Google Cloud Platform.
