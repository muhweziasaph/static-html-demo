# static-html-demo

operating system containerization assignment 

TASK 1 ASSIGNMENT SOLUTION, EXPLAINING THE CONCEPT OF CONTAINERISATION

QN1 Explain the concept of containerization.

(a)What are the key use cases of containerization?

(b)Explore different containerization technologies such as Docker, Podman, and Kubernetes. 

(c)how do they differ from Virtual Machines? 

(d)Create a Docker container for a simple web application (e.g., a Python Flask app or a static HTML server).

(e)Install Git and Create GitHub repository to work on this task.

(f)Walk through the process of containerizing a basic web application using Docker.

(g)Show the role of Kubernetes in container orchestration. 

(h)Share the GitHub Repository Link. The repository should include: The Dockerfile, Application source code, README.md


Containerization is a lightweight form of virtualization that allows applications to be packaged with all their dependencies into a standardized unit called a container. This ensures that applications run consistently across different computing environments.
Unlike virtual machines (VMs), which include an entire OS, containers share the host OS kernel, making them more efficient, faster, and lightweight.


(a) Key use cases of containerization

•	Microservices architecture. Containers are enable breaking down applications into smaller, independently deployable services.

•	Continuous integration/continuous deployment pipelines. Containers are used in continuous integration/continuous deployment workflows for faster application development and deployment.

•	Cloud computing. Containers are used to improve scalability and portability in cloud environments like AWS, Google Cloud, and Azure.

•	DevOps (development operations) and development environments. Developers create consistent environments across development, testing, and production using containerization.

•	Hybrid and multi cloud deployments Containers are used to deployed applications seamlessly across multiple cloud providers.

(b) Different containerization technologies

•	Docker. It is a platform that enables developers to automate the deployment of applications inside lightweight containers. It provides tools and resources to create, deploy, and run applications using containerization.

	Key features

	Simplifies application deployment.

	Offers docker hub, a repository for sharing container images.

	Supports multi-stage builds for optimized images.

•	Podman. It is a daemon less container engine that allows users to run containers as regular processes without requiring a background service.

	Key features

	Rootless mode enhances security by allowing unprivileged users to run containers.

	Compatible with docker CLI, making it easier for users to transition.

	Supports Kubernetes YAML, facilitating orchestration.

•	Kubernetes. It’s often abbreviated as K8s and it is a container orchestration platform designed for automating the deployment, scaling, and management of containerized applications.

Key features

•	Provides self-healing by automatically restarting failed containers.

•	Facilitates load balancing and service discovery.

•	Manages storage orchestration and automated rollouts/rollbacks.



(c)How containers differ from virtual machines (VMs)

Containerization uses compute resources more efficiently. A container creates a single executable package of software that bundles application code together with all of its dependencies required for it to run. Unlike virtual machines, however, containers do not bundle in a copy of the operating system. Instead, the container runtime engine is installed on the host system’s operating system, becoming the conduit through which all containers on the computing system share the same OS. They are often called “lightweight” simply because they share the machine’s operating system kernel and do not require the overhead of associating an OS within each application as in case of virtual machine. Other container layers (common bins and libraries) can also be shared among multiple containers, making containers inherently smaller in capacity than a virtual machine and faster to start up. Multiple containers can run on the same compute capacity as a single virtual machine, driving even higher server efficiencies and reducing server and licensing costs.

Whereas

Virtualization utilizes a hypervisor, a software layer placed on a physical computer or server that allows the physical computer to separate its operating system and applications from its hardware. Virtualization technology allows multiple operating systems and software applications to run simultaneously and share a single physical computer or host machine’s resources such as CPU (central processing unit), storage and memory. for example, with virtualization,  one server can run both windows and Linux or multiple versions of an operating system, along with various applications Each application and its related file system, libraries and other dependencies including a copy of the operating system are packaged together as a virtual machine.

 In summary.
 
•	Containers share host kernel of the operating system overhead whereas virtual machines require full operating system for each instance

•	Containers are faster and lightweight in performance where as virtual machines are heavier due to full operating system.

•	Containers isolation is at process level where as virtual machines is at full machine level

•	Containers start up time is in seconds whereas virtual machines take minutes to boot

•	Containers are highly portable across systems whereas virtual machines require specific configuration


(d) Docker file attached

(e) you’re on the created repository

(f) Containerizing a Basic Web Application Using Docker

I will use the approach i used to containerize a static HTML server using docker and deploy it on Google Kubernetes Engine (GKE) but almost procedures are the same even using other approaches. its all about creating a project directory then an application file for example HTML file, then docker file using Nginx to serve created HTML file, copying the HTML file to the Nginx server directory and exposing port 80, building docker image, and then running docker container. Below are the steps i personally used.
    
Steps i used to produce the one in this assignment

•	Setting up Goggle cloud project

	I created a project and enabled billing.

	I installed the Google Cloud SDK and authenticated it with the created project

•	Creating a static HTML Application.

	I created an index.html file.
<!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Static HTML Server</title>
     </head>
     <body>
         <h1>Hello, World! welcome to my static website </h1>
         <p>This is a static HTML page hosted on google cloud using Docker container and kubernetes.</p>
     </body>
     </html>
     
	I created a dockerfile to serve the HTML file using Nginx.
# i used  an official Nginx image as the base image
     FROM nginx:alpine
# i Copied the static HTML file to the Nginx web root directory
     COPY index.html /usr/share/nginx/html/index.html
# i exposed port 80
     EXPOSE 80
# i started Nginx
     CMD ["nginx", "-g", "daemon off;"]
     
•	Building and running the docker container locally

	I build the docker image:

       
          docker build -t static-html-server.
          
	I ran the container:

       
          docker run -p 8080:80 static-html-server
          
•	Pushing the docker image to Google container registry.

	I tagged and pushed the image using:

          
          docker tag static-html-server gcr.io/<PROJECT_ID>/static-html-server:latest
          docker push gcr.io/<PROJECT_ID>/static-html-server:latest
          
•	Deploying the application on Kubernetes.

	I created a Goggle Kubernetes engine cluster using:

          
          gcloud container clusters create static-html-cluster --num-nodes=3
          
          
	I deployed the application using:

          
          kubectl create deployment static-html-app --image=gcr.io/<PROJECT_ID>/static-html-server:latest
          kubectl expose deployment static-html-app --type=LoadBalancer --port=80 --target-port=80
          
          
	I accessed the app at the external IP provided by Goggle Kubernetes engine


(g) The Role of Kubernetes in Container orchestration

Kubernetes is a powerful orchestration system for automating the deployment, scaling, and management of containerized applications. It abstracts the underlying infrastructure, allowing developers to focus on application development without worrying about the complexities of the environment.

Key features

•	Load Balancing.  Distributes traffic across containers.

•	Scaling. Automatically increases or decreases containers based on demand.

•	Self-healing. Restarts failed containers automatically.

•	Rolling updates. Deploys updates with zero downtime.

