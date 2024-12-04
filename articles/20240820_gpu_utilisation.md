---
title: "GPU Utilization in Containerized Environments: A Comprehensive Guide"
description: "A step-by-step guide on setting up and configuring containers for GPU-intensive tasks such as LLM inference or fine-tuning, using nanoGPT as a demo project."
author: "Your Name"
date: "2024-08-20"
tags: ["GPU", "Containerization", "LLM Inference", "nanoGPT", "Docker", "Daytona"]
---


## TL;DR

This guide explains how to configure containers for GPU-intensive tasks such as large language model (LLM) inference and fine-tuning. Using [nanoGPT](https://github.com/karpathy/nanoGPT) as an example, it covers setting up a GPU-capable environment with Docker and NVIDIA Container Toolkit, running GPU-accelerated containers in Daytona, and addressing common challenges like driver mismatches. Optional performance benchmarks and optimization tips are provided for maximizing efficiency.

---

## Introduction

Running GPU-intensive applications in containerized environments has become a necessity for tasks like LLM inference, fine-tuning, and large-scale data processing. Containers ensure consistency, portability, and scalability, but configuring them to leverage GPU resources effectively can be challenging.

In this guide, we’ll:

1. Set up a GPU-enabled container environment using Docker and NVIDIA tools.
2. Configure and run [nanoGPT](https://github.com/karpathy/nanoGPT) in a containerized setup, using Daytona for orchestration.
3. Explore common challenges, troubleshooting steps, and optional performance optimizations.

---

## Prerequisites

Before diving into the setup, ensure you have:

### Hardware
- An NVIDIA GPU compatible with CUDA (e.g., Tesla, Quadro, or GeForce series).

### Software
- **CUDA Drivers**: Installed and matched to your GPU’s requirements.
- **Docker**: Installed and configured on your machine.
- **NVIDIA Container Toolkit**: Installed to enable GPU access in Docker.

### Verifying GPU Compatibility

Use the following command to confirm your system recognizes the GPU:

```bash
lspci | grep -i nvidia
```

If your NVIDIA GPU appears in the output, your system is ready. Otherwise, ensure proper GPU installation and driver setup.

---

## Step 1: Installing Required Tools

### Installing Docker

1. **Update your package list**:

   ```bash
   sudo apt-get update
   ```

2. **Install Docker**:

   ```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

3. **Start Docker and enable it on boot**:

   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Verify Docker installation**:

   ```bash
   docker --version
   ```

---

### Installing NVIDIA Container Toolkit

The NVIDIA Container Toolkit allows Docker containers to utilize GPU resources.

1. **Set up the repository**:

   ```bash
   distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
   curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
   curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
   ```

2. **Install the NVIDIA Container Toolkit**:

   ```bash
   sudo apt-get update
   sudo apt-get install -y nvidia-container-toolkit
   sudo systemctl restart docker
   ```

3. **Test GPU access in Docker**:

   ```bash
   docker run --gpus all nvidia/cuda:11.0-base nvidia-smi
   ```

   You should see a summary of your GPU’s usage and specs.

---

## Step 2: Building a GPU-Enabled Docker Image

To create a GPU-ready environment, we'll build a Dockerfile tailored for LLM workloads, specifically for [nanoGPT](https://github.com/karpathy/nanoGPT).

### Writing the Dockerfile

Here’s a Dockerfile optimized for nanoGPT:

```Dockerfile
# Use an official NVIDIA CUDA image
FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu20.04

# Install Python and required dependencies
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    git && \
    rm -rf /var/lib/apt/lists/*

# Install PyTorch with CUDA support
RUN pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Clone the nanoGPT repository
RUN git clone https://github.com/karpathy/nanoGPT.git /nanoGPT

# Set working directory
WORKDIR /nanoGPT

# Install nanoGPT dependencies
RUN pip3 install -r requirements.txt

# Default command to run nanoGPT training or inference
CMD ["python3", "train.py", "--dataset", "path/to/your/dataset"]
```

### Building the Docker Image

1. Save the Dockerfile in the root directory of your nanoGPT project.
2. Build the image:

   ```bash
   docker build -t nanogpt-gpu .
   ```

---

## Step 3: Running nanoGPT in Daytona

[Daytona](https://daytona.docs.io) is an orchestration tool designed for containerized workflows, simplifying deployment and GPU management.

### Running nanoGPT in Daytona

1. **Deploy the container**:
   Use Daytona to allocate GPU resources and deploy the `nanogpt-gpu` container. For example:

   ```bash
   daytona run --gpus all nanogpt-gpu
   ```

2. **Verify GPU usage**:
   Inside the running container, check GPU utilization:

   ```bash
   docker exec -it <container_id> nvidia-smi
   ```

   This command should display active processes utilizing the GPU.

---

## Troubleshooting Common Issues

### Driver Incompatibilities

Ensure the CUDA version in your container matches the host’s NVIDIA driver. Check the driver version with:

```bash
nvidia-smi
```

Cross-reference it with the CUDA version in your base image.

### Container Crashes or Resource Shortages

If containers fail to start or crash, inspect logs:

```bash
docker logs <container_id>
```

Allocate sufficient memory and compute resources when running GPU-intensive tasks.

---

## Optional: Performance Benchmarks and Optimization

### Benchmarking GPU Usage

Use tools like `nvprof` or `NVIDIA Nsight Systems` to profile GPU utilization. For example:

```bash
nvprof python3 train.py --dataset path/to/your/dataset
```

This helps identify bottlenecks and optimize kernel execution.

### Optimization Tips

- **Streamline Docker Images**: Use multi-stage builds to reduce image size and deployment time.
- **Environment Variables**: Adjust `CUDA_VISIBLE_DEVICES` to control which GPUs the container can access.
- **Mixed Precision Training**: Leverage mixed-precision training (`torch.cuda.amp`) to reduce memory consumption and improve performance.

---

## Conclusion

This guide has covered everything you need to know to set up GPU-enabled containers for tasks like LLM inference. Using tools like Docker, NVIDIA Container Toolkit, and Daytona, you can create portable, scalable environments for GPU workloads. The nanoGPT example illustrates how to integrate these practices into real-world applications.

With proper setup, troubleshooting, and optimizations, you can maximize the potential of GPUs in your containerized workflows. Explore nanoGPT in Daytona and elevate your machine-learning projects today!

---

### References

- **[Docker Documentation](https://docs.docker.com/)**: For general containerization practices.
- **[NVIDIA Toolkit](https://docs.nvidia.com/)**: Detailed guides on GPU usage in containers.
- **[nanoGPT GitHub Repository](https://github.com/karpathy/nanoGPT)**: The demo project used in this guide.
- **[Daytona Documentation](https://daytona.readthedocs.io/)**: For deploying GPU-intensive workloads.

---