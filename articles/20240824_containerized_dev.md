---
title: "Containerize your app: how Uber moves big data in hours"
description: "Why is everyone talking about containerization these days and why is it loved by all ? Read along as we explore how and why companies are taking advantage of it."
date: 2024-08-24
author: "Hunain Ahmed"
tags: ["Containerization", "Containers", "Docker", "Kubernetes", "Uber", "Isolation"]
---
# Containerize your app: how Uber moves big data in hours

## What is a Container?
Imagine this. You have a project that is supposed to run seamlessly on every developer's machine and on every server, in every environment. How do you ensure consistency in everything—from code down to libraries and system configurations? This is where containers come in.

A container is like a digital shipping crate: it encapsulates everything an application needs to run—code, runtime, system tools, libraries—into one self-contained unit. 

 But the questions arise:  
 - why [containerize](https://www.daytona.io/definitions/c/containerization) applications at all?
 -  Isn’t this just adding more complexity? 
 - And how does containerizing benefit teams in the long run?

Come along as we take a close look at how industry leaders like Netflix and Uber profit from containerized development and why your team should think about migrating too.

## Case Studies

### Uber: Big Data on Docker
Uber operates one of the most complex and [data-intensive platforms](https://www.uber.com/blog/uber-big-data-platform/) in the world, processing billions of events daily. To manage this, Uber needed a [scalable](https://www.daytona.io/definitions/s/scalability), flexible solution that could handle their big data needs without compromising performance. **[Docker](https://www.daytona.io/definitions/d/docker)** became the solution.

Before employing Docker, Uber used **[Hadoop](https://hadoop.apache.org/)** - the big-data processing tool - on bare-metal. This meant that any automation scripts written to have effect on Hadoop would also **indirectly mutate the host**, striking the developers with surprises and broken functionalities in the future.

It was a disaster to manually implement fleet-wide updates to the OS and the software. **It would take months, if not years**. Additionally, it would be really hard to implement the same configuration across numerous servers, and once a misconfiguration was implemented, it would be a real pain to identify and then manually remove that configuration from each server. 

Uber knew this was NOT OK, and developers would have frequent freak-outs. Therefore it decided to **containerize Hadoop** and distribute it to the servers. They used Docker and isolated the beast; now it became easier to **point out misconfigurations** and fix before finalizing the container. Plus now they could make changes to the container and not the host itself; **leaving it untouched** from the data and scripts it's running.

[Containerizing Apache Hadoop Infrastructure at Uber](https://www.uber.com/blog/hadoop-container-blog/)



### Pinterest: Boosting Dev-productivity with Kubernetes

Pinterest—the image hosting platform—has employed many diverse services written in a variety of tech stacks, which means that developers would have a hard time getting familiar with the technologies used, consequently making the onboarding process long and tough for them.

Moreover, it became **too complicated to monitor the health** and usage of different services that used different management systems—especially when they faced huge traffic and needed to perform **[downtime](https://www.daytona.io/definitions/d/downtime) evaluations**.

This led them to containerize most of their services and use **[Kubernetes](https://www.daytona.io/definitions/k/kubernetes)** to manage those containers. Now, it was simpler to monitor the services and scale them accordingly. The developers loved it: a much better [developer experience](https://www.daytona.io/definitions/d/developer-experience-devex) was created, boosting their productivity. 

[Unlocking Developer Productivity](https://www.daytona.io/dotfiles/unlocking-developer-productivity)

[Read: Building a Kubernetes platform at Pinterest](https://medium.com/pinterest-engineering/building-a-kubernetes-platform-at-pinterest-fb3d9571c948)

### Netflix: Millions of Containers with Titus


Netflix’s story with containers is a tale of scale. The streaming giant, which serves content to millions of users globally, needed a way to handle their colossal traffic volumes with minimal [latency](https://www.daytona.io/definitions/l/latency). Enter **Titus**, Netflix’s own container management platform.

Titus is Netflix's first choice for **scalability**: the container only has to specify its resource requirements, and [Titus does the rest](https://netflixtechblog.com/auto-scaling-production-services-on-titus-1f3cd49f5cd7) - deciding how many EC2 instances to allocate and their sizes.

On top of that, by using containerized workloads, Netflix was able to implement **[multi-tenancy](https://kubernetes.io/docs/concepts/security/multi-tenancy/)** and **metadata proxy**, this means that many containers running on the same machine can share hardware resources (CPU, RAM, and disk storage) **without literally sharing them**: Titus ensures they don't get into each other's way and have their own slice. What metadata proxy does is hide the host's network info from the container and give it its own network identity - so the container knows nothing about the host, it also hides the **IAM credentials** of the machine; giving the container only the rights and credentials it's supposed to have.

[The Ultimate Guide to Container Security](https://www.netmaker.io/resources/container-security)

Such a level of **[isolation](https://www.daytona.io/definitions/i/isolation), encapsulation and security** would be a horrible nightmare to implement without containerization - especially when you are running **millions of jobs** every week.

[Read: The Evolution of Container Usage at Netflix](https://netflixtechblog.com/the-evolution-of-container-usage-at-netflix-3abfc096781b)


### Airbnb: Autoscaling with Kubernetes
Airbnb traffic varies greatly throughout the year due to seasonal factors, holidays, and events. That would mean that before the services were containerized, resources, allocated with a peak in mind, **sat unused in times of low traffic**; waste at its purest. Airbnb had to find a way to auto-scale based on the traffic, so they decided to use Kubernetes, containerize their workflows and use **[Kubernetes Cluster Autoscaler](https://github.com/kubernetes/autoscaler)**—the tool that is really good at **adjusting the size of a cluster based on the incoming pod requests**. That removed the need to scale each service manually and saved the cost of unallocated resources.

[Read: Airbnb's cluster scaling journey](https://engineering.01cloud.com/2024/02/14/airbnbs-dynamic-kubernetes-cluster-scaling-journey/)

## But why use Containers?

You read above about how the companies faced problems with scalability, efficiency, speed and organized build cycle - and were convinced to containerize their workflows, here's why you should consider that too:
- **Consistency**: Containers provide a consistent environment across all stages of development, reducing the chances of environment-specific bugs - as they can be spotted and reproduced before the container is shipped.

- **Portability**: You can run them anywhere—on a developer’s laptop, on-premises servers, or in the cloud—making them incredibly flexible. [Read More](https://www.infoworld.com/article/2255880/what-does-container-portability-really-mean.html)

- **Scalability**: Containers can be [easily scaled up or down](https://www.f5.com/company/blog/how-containers-change-scalability) to meet demand, as seen with Airbnb’s autoscaling with Kubernetes. Which is further glorified by the dedicated tools for auto-scaling.
- **Isolation**: By isolating services in containers, companies like Netflix and Uber can ensure that issues in one service don’t affect others, this reduces downtime.
- **Efficiency**: Containers allow for more efficient use of resources, reducing costs and enabling faster deployment cycles. The easy monitoring facility shows the health and usage at one place, helping you take the next action.

Other real-world examples include Google, which runs everything from Gmail to YouTube using containers, and Spotify, which deploys its microservices architecture with the help of Docker. These examples show that containers are not only niche technology but at the heart of modern software development.



## Getting Started

If you are a small team with not much time to transform the whole infrastructure - you should perhaps think about starting small, like Pinterest started migration in 2017 and kept making updates as the userbase grew. 

Here's are some things you should consider before starting the onboarding process:

- **Training**: Ensure that your team receives training in container technologies like Docker and Kubernetes. Provide practical trainings and documentations on how to overcome common difficulties.
[Deciding your Strategy](https://www.vmware.com/topics/containerization-strategy)

- **Tooling**: Choose the right tooling based on the workflow. While Docker is the king of containerization, and Kubernetes is ruling the orchestration area, maybe OpenShift, Mesos or Nomad will fit better your needs, like Titus did for Netflix.

- **Cultural Shift**: Very often, containers do require a culture shift in how teams think about development and deployment. Foster automation, continuous integration, and continuous deployment as a culture to maximize the benefits that containers can bring. Stress on friendly conversations to get the team familiar.

[Read: 5 Steps to Migrate your Application to Containers](https://opensource.com/article/22/2/migrate-application-containers)

## Understanding the Workflow
Containers can really streamline and standardize the CI/CD process, making deployments faster and more reliable. Let's have a look at the workflow in a containerized architecture:

1. **Code**: Developers write and commit code as usual, but now they define dependencies and configurations in **[Dockerfiles](https://docs.docker.com/reference/dockerfile/)**: 

```Dockerfile 

	# Use the official Node.js 16 LTS image as the base image
	FROM node:16

	# Set the working directory inside the container
	WORKDIR /app

	# Copy the package.json and package-lock.json files to the working directory
	COPY package*.json ./

	# Install the project dependencies
	RUN npm install

	# Copy the rest of the application code to the working directory
	COPY . .

	# Expose the port that the application will run on
	EXPOSE 3000

	# Define the command to run the application
	CMD ["npm", "start"]

```
2. **Build**: The CI system builds the code inside a Docker container, ensuring that the environment is consistent across all stages.
3. **Test**: Automated tests run inside containers, making sure that the code behaves as expected in an environment identical to production.
4. **Deploy**: The application is deployed using an **orchestration tool** like Kubernetes, which manages the lifecycle of the containers—scaling them up or down as needed.
5. **Monitor**: Monitoring tools like **Prometheus** and **Dynatrace** track the health of the containers, alerting the team to any issues that arise.

This workflow reduces the chances of ["it works on my machine"](https://www.daytona.io/definitions/w/works-on-my-machine-syndrome) problems, as containers ensure consistency across development, testing, and production environments. On top of that, it enables teams to roll out new features or bug fixes faster, with confidence that the environment won’t introduce unexpected issues due to a change in dependency versions and environment.



## Final Thoughts
Containerizing can be a game-changer especially if you see growth in future and are looking to scale in the most efficient way possible. But one thing to keep in mind is that *if it worked for them, doesn't necessarily mean it should work for you*. It does exponentially good in certain scenarios and you have to thing about yours. Remember, it would be a disaster and a great loss if you invested so much time and money on containerizing, only to find out later on that it wasn't necessary at all. So carefully plan your next move, and always do your research before taking such a decision.

 Start small, iterate, and don’t be afraid to learn from the successes—and the challenges—of the industry leaders who have gone before you. Good luck with containers!
