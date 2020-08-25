# GCP-Google-Cloud-Platform

Google has tons of Datacenters across world. It has global infrastructure and Google is providing their Infrastructure as a service through cloud computing i.e. **Google Cloud Platform (GCP)**

## WHY WE NEED INFRASTRUCTURE ?

 To run a business we create an app, and to run that app we need one OS. Now for booting and running OS we need RAM & CPU (Computing Unit) and for installing OS we need Block storage(Storage Unit). So wither you purchase your own RAM, CPU & Hdisk to host website for your business. 
- But here, we don't know our infra needs in prior. If we talk about startup, they cna't predict how many clients will come, maybe very low or maybe their plan goes viral and huge client hit their wesite. 
- Also, a lot of money and time is invested in the management of IT infra, like we need to hire technical guys to manage servers, databases, cables, wiring, Routers, switches, load balancing, etc. So huge invstment goes in IT infra. 
- Even if we buy infra then we can't resell it at the same price for which you purchased.
- Also for a company, their app is their business and they want to focus more on the development on the app. Their focus area should not be on management of infrastructure.

So rather than investing upfront on IT infra, we outsource our infra to some other company, which has unlimited pool of resources, and they have the best engineers and technical guys who are specialized in management of this infra, and they have best security. These companies are known as **service providers** and they prvovide you Infrastructure as a service(IAAS). And we don't have to pay upfront, rather we have a pay-as-you-go model. **AWS, GCP, ALI BABA, Azure, etc all are service providers for public cloud computing.**

So we now are going to utilize computing power of Google Global Infrastructure through GCP. As of now, GCP has **24 Regions(Country, Area or Continent)** & **73 Zones(Data Centes)**. Every region has min3 and max 4 zones, mainly for disaster recovery. Some services are available in specific regions, eg Google App Engine is not available in Singapore region.

### Why 3-4 zones in one region or Why Google provide Global Infrastructure Service?
- Due to natural disaster if anything happen and one zone goes down, we have other zones located at some distance that are up and running. So this gives us facility of disaster recovery. We as cloud architect can plan disaster recovery.
- To mininize latency and Delay while using serivces.
- Other reason can be some regulatory compliance. Some companies don't allow their data to go outside their country.
- More secure, as Google has its own personal private network of  fibre optic cables which allows us to transfer data with high speed, low latency and since data wont travel over public internet so its highly secured.

### Projects, Oragnization and API'S:

- For every service in GCP, google has one API. Before using any service we have to enable that API. Basically every service is one program/application for which google has given some interface. So its called API and user always connect to API. Most of the API's are disabled. So we have to manually enable the API of the service which we want to work on.
-  3 ways to connect to API
   1. CLI- using gclooud command on your base laptop console. Also GCP offers one feature to use interactive shell on cloud to run CLI commands directly IN GCP, that is called **Active Cloud shell**. In this they launch one Linux OS behind the scene and they activate command prompt or shell for you where we can run all commands of linux.
   2. Web UI of GCP
   3. SDK- using some app you can connect to API.

- Oragnization is nothing but company name. So normally in a comapny we have many teams (or ENVIRONMENTS), eg DEVELOPER, PRODUCTION, TESTING, etc. Production team is very critical.. give more RAM, CPU, Storage, tight Security. Can't compromise with anything. But in Development environment, can give just one server to test our app. Don't give much  RAM, CPU to this team coz we have to manage billing. So, in GCP we can create different different teams or **Projects** and set quotas/limit on the project. This is a good way of management of resources. So, to use any resource in GCP we have to create a project & associate it with a billing account. By default one project is alreay created for us. So project is a good way to manage resources and set some limits & quotas and its a way to isolate your resources. One click entire project delete and all resources delete.

- Project is always managed inside organization. In one organization your project ID must be unique.

```
#gcloud projects list   //to see all projects

#gcloud projects --help  // to see what all options they support

#gcloud projects create devproject-1234567890 --name prodproject  // to create project using CLI

#gcloud services list --project devproject-1234567890   // to check how many services(API's) are active in this project

#gcloud services list --available --project devproject-1234567890  // to check all the services available in GCP (active+inactive)

#gcloud services list --available --project devproject-1234567890  | grep compute  // to check if compute service is enabled or not

#gcloud services  enable compute.googleapis.com --project prodproject-1234098765    //enable Compute API from CLI (Billing account must be associated with the project)

```
## Google Compute Engine (GCE):

- It provides Compute as a Service. Can launch VM's

- Select Machine configuration or Machine type depending upon requirement of app.
  1. Memory optimized - More RAM
  2. Compute Optimized - More CPU
  3. General Purpose - Basic Workload
