### GPU Utilization in Containerized Environments: A Practical Guide

As the demand for machine learning, particularly large language models (LLMs), continues to grow, the need for powerful GPU resources has become increasingly critical. GPUs enable faster inference and fine-tuning, making them essential for developers working with LLMs. However, managing GPU resources efficiently, especially in containerized environments, can be challenging. This article provides a step-by-step guide on setting up and configuring containers for GPU-intensive tasks, with a demo project using [nanoGPT](https://github.com/karpathy/nanoGPT) running in Daytona. 

---

### Setting Up the Environment

#### Prerequisites

Before diving into containerization, ensure you have the following prerequisites:
- **Hardware**: A compatible NVIDIA GPU.
- **Software**:
  - CUDA drivers installed on the host machine.
  - Docker installed.
  - NVIDIA Container Toolkit for Docker.

#### Installing Necessary Tools

1. **Install Docker**:
   Ensure you have Docker installed. You can install Docker on Ubuntu using:

   ```bash
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

2. **Install NVIDIA Container Toolkit**:
   To enable GPU support in Docker, you need to install the NVIDIA Container Toolkit:

   ```bash
   sudo apt-get install -y nvidia-container-toolkit
   sudo systemctl restart docker
   ```

3. **Verify GPU Support in Docker**:
   After installing the toolkit, verify that Docker can access your GPU:

   ```bash
   docker run --gpus all nvidia/cuda:11.0-base nvidia-smi
   ```

   This command should display your GPU information, confirming that Docker can use the GPU.

#### Configuring Docker for GPU Access

To build containers with GPU support, you'll need to create a Dockerfile that includes the necessary CUDA libraries and Python dependencies.

Example Dockerfile for a Python-based GPU application:

```Dockerfile
FROM nvidia/cuda:11.3.1-cudnn8-devel-ubuntu20.04

# Install Python and dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip3 install torch torchvision torchaudio

# Set working directory
WORKDIR /app

# Copy your application code
COPY . /app

# Run your application
CMD ["python3", "your_script.py"]
```

### Demo Project: Running nanoGPT in Daytona

For this guide, we'll use [nanoGPT](https://github.com/karpathy/nanoGPT) by Andrej Karpathy as a demo project. nanoGPT is a lightweight implementation of GPT, making it ideal for experimentation in containerized environments.

#### Project Overview

nanoGPT is a minimalistic implementation of GPT, designed to be simple and easy to run. It's perfect for developers who want to experiment with LLM inference in a containerized environment.

#### Building the Project

1. **Clone the Repository**:
   Start by cloning the nanoGPT repository:

   ```bash
   git clone https://github.com/karpathy/nanoGPT.git
   cd nanoGPT
   ```

2. **Create a Dockerfile**:
   Create a Dockerfile within the nanoGPT directory to containerize the project:

   ```Dockerfile
   FROM nvidia/cuda:11.3.1-cudnn8-devel-ubuntu20.04

   # Install Python and dependencies
   RUN apt-get update && apt-get install -y python3 python3-pip git
   RUN pip3 install torch torchvision torchaudio

   # Clone nanoGPT repository
   RUN git clone https://github.com/karpathy/nanoGPT.git /nanoGPT
   WORKDIR /nanoGPT

   # Run nanoGPT training or inference
   CMD ["python3", "train.py", "--dataset", "path/to/your/dataset"]
   ```

3. **Build the Docker Image**:
   Build the Docker image for nanoGPT:

   ```bash
   docker build -t nanogpt-gpu .
   ```

#### Running the Project in Daytona

Daytona is a container orchestration platform that simplifies running containerized applications, especially those requiring GPU support.

1. **Special Instructions for Daytona**:
   - Ensure that the Dockerfile is compatible with Daytona's environment.
   - Set environment variables specific to Daytona, such as `CUDA_VISIBLE_DEVICES` to allocate GPUs.

2. **Run the Container in Daytona**:
   Use Daytona's interface or CLI to deploy the nanoGPT container. Ensure that the GPU resources are correctly allocated.

   Example command:

   ```bash
   daytona run --gpus all nanogpt-gpu
   ```

3. **Verify GPU Utilization**:
   After deploying the container, use `nvidia-smi` within the container to verify GPU utilization.

   ```bash
   docker exec -it <container_id> nvidia-smi
   ```

#### Accessing Logs and Metrics

Monitoring GPU usage is crucial for optimizing performance. Use Daytona's built-in monitoring tools or integrate with third-party tools like Prometheus and Grafana to track GPU metrics.

### Challenges and Solutions

#### Common Issues

1. **Driver Incompatibilities**:
   - Ensure that the CUDA version in the container matches the driver version on the host machine.

2. **Container Crashes**:
   - Check for memory allocation issues or misconfigured environment variables.

3. **Performance Degradation**:
   - Monitor GPU utilization and optimize code or CUDA settings if needed.

#### Troubleshooting Guide

- **Driver Issues**: If you encounter driver issues, verify that the correct version of the NVIDIA driver is installed and compatible with the CUDA version in your Docker image.
- **Memory Management**: Optimize memory usage within your code to prevent out-of-memory errors, especially when working with large models.

#### Security Considerations

When running GPU-intensive tasks in a multi-tenant environment, it's essential to secure GPU resources. Ensure that containers are isolated and that only authorized containers can access the GPU.

### (Optional) Performance Benchmarks and Optimization Tips

If you wish to go further, you can benchmark nanoGPT's performance in different environments:

1. **Benchmarking GPU Performance**:
   - Use tools like `nvprof` or `nsys` to profile GPU usage and identify bottlenecks.

2. **Optimization Tips**:
   - Reduce Docker image size by using lightweight base images.
   - Adjust CUDA settings to maximize GPU utilization.

### Conclusion

In this guide, we’ve walked through the process of setting up and configuring containers for GPU-intensive tasks, using nanoGPT as a demo project. By following these steps, developers can efficiently run LLM inference in a containerized environment, specifically within Daytona. While there may be challenges along the way, such as driver issues or performance bottlenecks, the solutions provided here should help you navigate them effectively.

We encourage you to experiment with nanoGPT in Daytona, explore advanced configurations, and share your findings with the community.

---

### References/Resources

- **[NVIDIA Documentation](https://docs.nvidia.com/)**: Official guides on setting up NVIDIA GPUs with Docker.
- **[CUDA Toolkit Documentation](https://developer.nvidia.com/cuda-toolkit)**: For understanding CUDA setup and GPU programming.
- **[Docker Documentation](https://docs.docker.com/)**: General containerization practices and GPU support.
- **[Docker High Memory Usage Debug](https://www.benjaminrancourt.ca/how-to-debug-high-memory-usage-in-docker/)**: Troubleshooting High Memory Usage in Docker.
- **[nanoGPT GitHub Repository](https://github.com/karpathy/nanoGPT)**: The nanoGPT project by Andrej Karpathy.
- **[Daytona Documentation](https://daytona.readthedocs.io/)**: For running and optimizing containerized applications in Daytona.

This article provides a comprehensive guide for developers looking to harness GPU resources in containerized environments, particularly for LLM inference using the nanoGPT project.