
---

title:  "Containerized Development: Lessons learned from Uber, Pinterest and Netflix"

description:  "Why is everyone talking about containerization these days and why is it loved by all ? Read along as we explore how and why companies are taking advantage of it."

date:  2024-12-05

author:  "Hunain Ahmed"

tags: ["Containerization",  "Containers",  "Docker",  "Kubernetes",  "Uber",  "Isolation"]

---

# Containerized Development: Lessons learned from Uber, Pinterest and Netflix
  
## Introduction: What is a Container?

Imagine this. You have a project that is supposed to run seamlessly on every developer's machine and on every server, in every environment. How do you ensure consistency in everything—from code down to libraries and system configurations? This is where containers come in.

A container is like a digital shipping crate: it encapsulates everything an application needs to run—code, runtime, system tools, libraries, all of it—into one self-contained unit.

## TL;DR

- explore why [containerization](https://www.daytona.io/definitions/c/containerization)  is important
- discuss case studies from big companies
- get started with containerization

Come along as we take a close look at how industry leaders like Netflix and Uber profit from containerized development and why your team should think about migrating too.

## Case Studies

### Uber: Big Data on Docker

Uber operates one of the most complex and [data-intensive platforms](https://www.uber.com/blog/uber-big-data-platform/) in the world, processing billions of events daily.
To manage this, Uber needed a [scalable](https://www.daytona.io/definitions/s/scalability), flexible solution that could handle their big data needs without losing on performance. **[Docker](https://www.daytona.io/definitions/d/docker)** became the solution.

Before employing Docker, Uber used **[Hadoop](https://hadoop.apache.org/)** - the big-data processing tool - on bare-metal.
This meant that any automation scripts written to have effect on Hadoop would also **indirectly mutate the host**, striking the developers with surprises and broken functionalities in the future.

Manually updating the OS and software across an entire fleet was a complete headache. **It could take months—or even years.** Keeping the same configuration across all servers was a challenge, and if something got misconfigured, finding and fixing it on every single server was a bigger  nightmare.
  
Uber recognized that managing Hadoop effectively was essential for its developers.
To improve the situation, the company decided to **containerize Hadoop** and distribute it across their servers. They implemented Docker to isolate the application, making it easier to **identify misconfigurations** and rectify them before finalizing the container.
This approach allowed them to make changes to the container without affecting the host system itself, **keeping it untouched** from the data and scripts it was running.

### Pinterest: Boosting Dev-productivity with Kubernetes

Pinterest—the image hosting platform—has employed many diverse services written in a variety of tech stacks, which means that developers would have a hard time getting familiar with the technologies used, consequently making the onboarding process long and tough for them.

Moreover, it became **too complicated to monitor the health** and usage of different services that used different management systems—especially when they faced huge traffic and needed to perform **[downtime](https://www.daytona.io/definitions/d/downtime) evaluations**.

This led them to containerize most of their services and use **[Kubernetes](https://www.daytona.io/definitions/k/kubernetes)** to manage those containers. Now, it was simpler to monitor the services and scale them accordingly.
The developers loved it: a much better [developer experience](https://www.daytona.io/definitions/d/developer-experience-devex) was created, and the on-boarding became much simpler.

[Read: Unlocking Developer Productivity](https://www.daytona.io/dotfiles/unlocking-developer-productivity)

### Netflix: Millions of Containers with Titus

Netflix’s journey with containers showcases their need for scalability in handling massive traffic volumes while maintaining minimal  [latency](https://www.daytona.io/definitions/l/latency).
To address this challenge, they developed **Titus**, their proprietary container management platform, designed specifically for their unique streaming demands.

Titus is Netflix's first choice for **scalability**: the container only has to specify its resource requirements, and [Titus does the rest](https://netflixtechblog.com/auto-scaling-production-services-on-titus-1f3cd49f5cd7) - like deciding how many EC2 instances to allocate and their sizes.

Continuing from this, Netflix has taken advantage of containerized workloads to implement **[multi-tenancy](https://kubernetes.io/docs/concepts/security/multi-tenancy/)** and a **metadata proxy**.
This setup allows multiple containers to run on the same machine while efficiently sharing hardware resources—like CPU, RAM, and disk storage—**without actually sharing them**.
Titus manages the environment so that each container operates independently, ensuring they don’t interfere with one another and each has its own dedicated resources.

The metadata proxy also plays an important role by hiding the host's network information from the container, giving it a unique network identity.
This means the container doesn’t have to know anything about the host and has only the **IAM credentials** it really needs, keeping access tightly controlled.

[Read: The Ultimate Guide to Container Security](https://www.netmaker.io/resources/container-security)

Achieving such a high level of **[isolation](https://www.daytona.io/definitions/i/isolation), encapsulation, and security** would be quite a challenge without containerization—especially with **millions of jobs** running each week. By using these technologies,
Netflix not only strengthens its security but also boosts efficiency in its operations.

### Airbnb: Autoscaling with Kubernetes

Airbnb traffic varies greatly throughout the year due to seasonal factors, holidays, and events. That would mean that before the services were containerized, resources, allocated with a peak in mind, **sat unused in times of low traffic**,
which would be a great waste of resources.
Airbnb had to find a way to auto-scale based on the traffic, so they decided to use Kubernetes,
containerize their workflows and use **[Kubernetes Cluster Autoscaler](https://github.com/kubernetes/autoscaler)**—the tool that is really good at **adjusting the size of a cluster based on the incoming pod requests**.
That removed the need to scale each service manually and saved the cost of unallocated resources.

 Other real-world examples include Google, which runs everything from Gmail to YouTube using containers, and Spotify, which deploys its microservices architecture with the help of Docker. These examples show that containers are not only niche technology but at the heart of modern software development.

## Long-term benefits

Previously, we explored the challenges that companies encountered with scalability, efficiency, speed, and organized build cycles, which encouraged them to adopt containerization for their workflows. Here’s why you might want to consider this approach too:
- **Consistency**: Containers help maintain a consistent environment throughout development, reducing the chances of environment-specific bugs. This uniformity allows teams to identify and resolve issues before deployment, saving time and effort.

- **Portability**: Containers excel in portability, running seamlessly on a developer’s laptop, on-premises servers, or in the cloud. This adaptability ensures efficient workflows across different environments. [Read More](https://www.infoworld.com/article/2255880/what-does-container-portability-really-mean.html)

- **Scalability**: The ability to scale is another key advantage. Containers can be easily adjusted to meet varying demands, as demonstrated by Airbnb’s use of Kubernetes for autoscaling, which enhances performance without unnecessary resource allocation.

- **Isolation**: Container isolation ensures that issues in one service do not affect others, as seen with companies like Netflix and Uber. This reduces downtime and enhances security, leading to a more reliable system.

- **Efficiency**: Ultimately, these features contribute to greater efficiency. Containers provide control over resource management, paired with advanced monitoring tools, enabling teams to optimize application performance while keeping costs low.

## Onboarding

If you are a small team with not much time to transform the whole infrastructure - you should perhaps think about starting small, like Pinterest started migration in 2017 and kept making updates as the userbase grew.

Here's are some things you should consider before starting the onboarding process:

- **Training**: It’s really important for your team to get proper training on container technologies like Docker and Kubernetes. Try to offer hands-on sessions and some helpful resources so they can easily work through any bumps along the way.

- **Tooling**: Think about what tools really work for you. Docker is the go-to for containerization, and Kubernetes is great for orchestration. But don’t forget about other options.
Tools like OpenShift, Mesos, or Nomad might be a better fit for your specific needs, just like Titus was for Netflix.

- **Cultural Shift**: Moving to containers often means changing how your team approaches development and deployment.
Cultivating a culture that embraces automation, continuous integration, and deployment can make a big difference. Encourage friendly discussions to help everyone get comfortable with these new practices.
  
[Read: 5 Steps to Migrate your Application to Containers](https://opensource.com/article/22/2/migrate-application-containers)

## Understanding the Workflow

Containers have a way of making the entire CI/CD process more efficient and consistent, which ultimately results in quicker and more reliable deployments. Let's explore how a containerized architecture influences the workflow:

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

3. **Test**: Automated tests - if you have any - run inside containers, making sure that the code behaves as expected in an environment identical to production.

4. **Deploy**: The application is deployed using an **orchestration tool** (a tool responsible for management of tasks across multiple systems) like Kubernetes, which manages the lifecycle of the containers—scaling them up or down as needed.

5. **Monitor**: Monitoring tools like **Prometheus** and **Dynatrace** track the health of the containers, alerting the team to any issues that arise.

This workflow reduces the chances of ["it works on my machine"](https://www.daytona.io/definitions/w/works-on-my-machine-syndrome) problems, as containers ensure consistency across development, testing, and production environments.
On top of that, it enables teams to roll out new features or bug fixes faster, with confidence that the environment won’t introduce unexpected issues due to a change in dependency versions and environment.

## Final Thoughts

When thinking about containerizing your applications, it's really important to consider your own situation and plans for growth.
Sure, containerization can be a major efficiency booster and help you scale effectively, but just because it worked wonders for someone else doesn’t mean it’s the right fit for you. Each setup is different.

Before diving in and investing a lot of time and money, take a moment to assess if it really suits your needs. It would be frustrating to find out down the line that containerization wasn’t necessary at all, especially after all that effort and expense.
So, do your homework, weigh the pros and cons, and plan carefully. Making an informed decision now can save you a lot of headaches later on!

Start small, iterate, and don’t be afraid to learn from the successes—and the challenges—of the industry leaders who have gone before you. Good luck with containers, see you next time!

## References

[Book: Getting Started With Containerization](https://www.oreilly.com/library/view/getting-started-with/9781838645700/)

[Containerizing Apache Hadoop Infrastructure at Uber](https://www.uber.com/blog/hadoop-container-blog/)

[Building a Kubernetes platform at Pinterest](https://medium.com/pinterest-engineering/building-a-kubernetes-platform-at-pinterest-fb3d9571c948)

[The Evolution of Container Usage at Netflix](https://netflixtechblog.com/the-evolution-of-container-usage-at-netflix-3abfc096781b)

[Airbnb's cluster scaling journey](https://engineering.01cloud.com/2024/02/14/airbnbs-dynamic-kubernetes-cluster-scaling-journey/)
