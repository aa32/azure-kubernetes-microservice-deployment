# Azure Kubernetes Service (AKS): Deploying Microservices


# Q :     How Microservices fit into Kubernetes Infrastructure ?
Ans : Since Microservices are small, independent applications that fulfill a specific business /customer function, which you can scale in or out independently.which you can update or manage independently, each one of them.
** Before you deploy your microservice in Kubernetes, you need to package your microservice, its dependencies, configuration into a container image.
** This way you can deploy (and scale the service as demand increases) in Kubernetes cluster almost instantaneously 

# Q2: What is AKS(Azure Kubernetes Service)?
Ans : Azure Kubernetes service is a managed kubernetes orchestration software, 
that provides a means to deploy, manage and scale multiple containers.
It can automatically discover the services you deploy,
Allocate appropriate computing resources
Expose your services securely to the internet using a load balancer

  # Social Media App’s Architecture

# USER MANAGEMENT:
User account registration/ sign out
User Authentication to post or comment the posts
Authentication occurs via JSOn Web token, which is signed during login activity or sign up.
This token is stored at the client side and would be verified by other microservices that receive HTTP request to create a data record.


# POST and COMMENT MICROSERVICE:
Whenever user tries to create a post/comment, the HTTP request is sent to POST microservice⇒ it verifies the user using JWT_SECRET stored in Kubernetes CLUSTER.
If user is not authenticated while creating post or comment⇒ the action fails
POST MICROSERVICE also publish the posts to Event bus, so that comments microservice will have post IDs and will link future comments to this post

# POSTHUB MICROSERVICE:
Posthub microservice is a subscriber to post Event BUs, It also stores , Post IDs, User IDs, Comment Ids in its database.
UI only displays post and comments from PostHub Microservice.
This way even if POST or Comment Microservie is unavailable , users may not create POSTS or Comments but they can view the posts and comments created before the downtime.
Whenever a comment is made on the post , the post microservice will update the record with comment ID only while the POSThub microservice will update the record with Comment ID as well its content.

# UI Microservice


NATS and Kafka are both open-source messaging systems. NATS is a lightweight, efficient system that's suitable for moderate to high message rates. Kafka is a distributed streaming platform that's designed for high-throughput, fault-tolerant message processing.

 Here NATS Streaming server is user for PUB/SUB. Events
Other events based messaging platforms can be used like RabbitMQ, Azure Service BUS. *****We will see Manifest files for NATS streaming server and MongoDB containers*****

 To expose our application to internet we need to deploy 
	a). Ingress Controller 
	b). Ingress Resource
# Ingress controller is a special load balancer for Kubernetes Cluster.

It applies traffic Rules defined inside Ingress

It allows to expose the applications inside the cluster to outside the cluster.
Here Azure Application Gateway and enable the Application gateway Ingress Controller (AGIC) which integrates with kubernetes service.
This works as only 1 LOAD balancer with only 1 public IP address for a the requests.
Ingress controller has all the rules defied inside Manifest file also . 
Application gateway routes the request ( based on URL endpoint) to appropriate service.








