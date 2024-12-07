---
title: "Optimizing LLM Inference with GPU-Accelerated Docker Containers"
description: "Learn how to set up and optimize GPU-accelerated Docker containers for efficient LLM inference."
date: 2024-08-20
author: "Jacob Gaffke"
---

# Optimizing LLM Inference with GPU-Accelerated Docker Containers

## Introduction

[Large Language Models (LLMs)](/definitions/20240820_definition_large-language-model.md) such as GPT-2 and GPT-3 have significantly pushed the boundaries of [natural language processing (NLP)](/definitions/20240820_definition_natural-language-processing.md), enabling a wide range of applications from complex text generation to translation and summarization. However, deploying these models efficiently requires substantial computational power, particularly for tasks like real-time text generation. GPUs are indispensable for handling these operations effectively, and [containerization](/definitions/20240819_definition_containerization.md) offers a streamlined solution for managing and scaling such workloads.

This guide will take you through setting up and configuring [Docker](/definitions/20240819_definition_docker.md) containers specifically for GPU-accelerated tasks. We'll cover everything from initial setup to optimizing performance and troubleshooting common issues. By the end of this guide, you'll be equipped to deploy and manage [LLMs](/definitions/20240820_definition_large-language-model.md) in a GPU-enabled [containerized environment](/definitions/20240819_definition_containerization.md).

![architecture diagram](assets/20240820_gpu_utilization_img1.jpg)

### TL;DR

- **Set up a GPU-enabled environment**: Install and configure Docker with NVIDIA Container Toolkit for GPU support.
- **Build a container with essential libraries**: Include PyTorch, Transformers, and other dependencies for LLM inference.
- **Create and optimize a text generation script**: Leverage GPU resources to enhance performance in LLM tasks.
- **Monitor and improve performance**: Use tools like `nvidia-smi` and benchmarking to ensure efficient GPU utilization.
- **Address common issues**: Learn troubleshooting techniques for memory errors, slow performance, and GPU access problems.

## Installing Dependencies

Before setting up your environment for GPU-intensive tasks, ensure that you have the following prerequisites:

- A machine with a CUDA-compatible GPU (e.g., NVIDIA GPUs)
- [Docker](/definitions/20240819_definition_docker.md)
- [Daytona](https://github.com/daytonaio/daytona)
- [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

### Daytona Installation

You can install Daytona by running the following command in your terminal:

```bash
curl -sf -L https://download.daytona.io/daytona/install.sh | sudo bash
```

Daytona creates a controlled [development environment](/definitions/20240819_definition_development-environment.md) where you can work on the project with all dependencies correctly configured, reducing the likelihood of compatibility issues.

### Docker Installation

[Docker](/definitions/20240819_definition_docker.md) is a platform that allows you to automate the deployment of applications inside lightweight, portable containers. These containers include everything needed to run the application, such as the code, runtime, libraries, and dependencies, ensuring consistency across different environments.

If [Docker](/definitions/20240819_definition_docker.md) isn't already installed on your system, follow these steps:

```bash
# Update package lists and install Docker
sudo apt-get update
sudo apt-get install docker.io
sudo systemctl start docker
```

### NVIDIA Container Toolkit Installation

The NVIDIA Container Toolkit is essential for enabling GPU support in [Docker](/definitions/20240819_definition_docker.md) containers. It provides the necessary libraries and tools to seamlessly access NVIDIA GPUs from within [Docker](/definitions/20240819_definition_docker.md) containers, allowing you to leverage GPU acceleration for your applications.

![nvidia diagram](assets/20240820_gpu_utilization_img2.jpg)

To enable GPU support in [Docker](/definitions/20240819_definition_docker.md) containers, you need to install the NVIDIA Container Toolkit:

```bash
# Configure the production repository
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# Install the NVIDIA Container Toolkit
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit

# Configure the container runtime
sudo nvidia-ctk runtime configure --runtime=docker

# Restart Docker to apply changes
sudo systemctl restart docker
```

### Verify GPU Configuration

To verify that your [Docker](/definitions/20240819_definition_docker.md) setup can access the GPU, run the following command:

```bash
docker run --rm --gpus all nvidia/cuda:12.6.0-base-ubuntu24.04 nvidia-smi
```

If your setup is correct, the `nvidia-smi` command will display information about your GPU, confirming that the GPU is accessible inside [Docker](/definitions/20240819_definition_docker.md) containers.

## Running LLM Inference in a Docker Container

With your GPU-enabled [Docker](/definitions/20240819_definition_docker.md) environment ready, the next step is to develop a text generation script using an [LLM](/definitions/20240820_definition_large-language-model.md) and run it inside a [Docker](/definitions/20240819_definition_docker.md) container.

### Create Daytona Workspace

Before starting, make sure to create a Daytona workspace to set up a development environment:

```bash
daytona create https://github.com/giraffekey/gpu-container-example
```

This will create a controlled environment with the required Python dependencies installed.

You can open the workspace in your preferred IDE with the following command:

```bash
daytona code
```

### Download the GPT-2 Model

There should be this script in your opened workspace:

```python
# download.py

from transformers import GPT2LMHeadModel, GPT2Tokenizer

model_name = "gpt2"
model = GPT2LMHeadModel.from_pretrained(model_name)
tokenizer = GPT2Tokenizer.from_pretrained(model_name)
model.save_pretrained("./gpt2_model")
tokenizer.save_pretrained("./gpt2_tokenizer")
```

This script downloads and saves the GPT-2 model and tokenizer.

Run the script with:

```bash
python3 download.py
```

You should see `gpt2_model` and `gpt2_tokenizer` directories.

### Test the Model

This is the script we will be using to generate text with the model:

```python
# inference.py

import torch
from transformers import GPT2LMHeadModel, GPT2Tokenizer

def generate_text(prompt, max_length=50, top_k=50, top_p=0.9, temperature=0.8):
    # Check if GPU is available and set device accordingly
    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
    
    # Load pre-trained GPT-2 model and tokenizer
    model = GPT2LMHeadModel.from_pretrained("./gpt2_model")
    tokenizer = GPT2Tokenizer.from_pretrained("./gpt2_tokenizer", clean_up_tokenization_spaces=True)
    
    # Move model to the GPU
    model.to(device)

    # Encode the input prompt
    inputs = tokenizer.encode(prompt, return_tensors="pt").to(device)

    # Create attention mask
    attention_mask = torch.ones(inputs.shape, device=inputs.device)

    # Generate text
    outputs = model.generate(
        inputs,
        max_length=max_length, 
        attention_mask=attention_mask,
        pad_token_id=tokenizer.eos_token_id,
        do_sample=True,  # Enable sampling
        top_k=top_k,     # Top-k sampling
        top_p=top_p,     # Nucleus (top-p) sampling
        temperature=temperature  # Adjust temperature
    )

    # Decode the generated text
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

if __name__ == "__main__":
    prompt = "Once upon a time in a land far, far away"
    generated_text = generate_text(prompt)
    print(generated_text)
```

This script loads the model and tokenizer, performs text generation with advanced sampling techniques, and prints the output.

You can test the script in your workspace with the following command:

```bash
python3 inference.py
```

### Create a Docker Container

To run this script in a [Docker](/definitions/20240819_definition_docker.md) container, we'll be using the following Dockerfile:

```Dockerfile
FROM nvidia/cuda:12.6.0-base-ubuntu24.04

# Install Pip
RUN apt-get update && apt-get install -y \
    python3-pip \
    python3-dev \
    python3-venv

# Create virtual environment
RUN python3 -m venv workspace

# Install PyTorch and Transformers libraries
RUN /workspace/bin/pip install torch transformers

# Set the working directory
WORKDIR /workspace

# Copy your script into the container
COPY inference.py /workspace

# Copy downloaded model into container
COPY gpt2_model /workspace/gpt2_model

# Copy downloaded tokenizer into container
COPY gpt2_tokenizer /workspace/gpt2_tokenizer

# Specify the command to run
CMD ["bin/python", "inference.py"]
```

This `Dockerfile` sets up a GPU-enabled environment, installs Python and the necessary libraries, and copies the text generation script into the container.

### Build and Run the Docker Container

With your `Dockerfile` ready, build and run the container:

```bash
# Build the container
docker build -t llm-gpu .

# Run the container with GPU support
docker run --gpus all llm-gpu
```

### Output

Running the script should generate text similar to the following:

```
Once upon a time in a land far, far away, they would be able to see through their mind, and understand their own thoughts. We should be ashamed of ourselves, but we must not be ashamed of ourselves. We can only see and feel
```

The output will be different each time the command is run.

## Implementing Advanced Text Generation Techniques

When generating text using [LLMs](/definitions/20240820_definition_large-language-model.md), advanced sampling methods can significantly improve the quality and diversity of the output. This section will introduce top-k sampling, nucleus sampling (top-p sampling), and temperature scaling.

### Top-k Sampling

Top-k sampling restricts the model's predictions to the top `k` most probable next words, reducing the likelihood of generating less coherent outputs.

### Nucleus Sampling (Top-p Sampling)

Nucleus sampling selects from the smallest set of words whose cumulative probability is greater than or equal to `p`. This method allows for more dynamic sampling, adapting the number of considered tokens based on context.

### Temperature Setting

The temperature parameter controls the randomness of predictions by scaling the logits before applying the softmax function. Lower temperatures produce more deterministic results, while higher temperatures introduce greater variability.

### Configuring the Script

In the `inference.py` script, you can experiment with these values in order to tamper with the text output.

```python
# inference.py

...

if __name__ == "__main__":
    prompt = "Once upon a time in a land far, far away"
    generated_text = generate_text(prompt, top_k=50, top_p=0.9, temperature=2.0)
    print(generated_text)
```

By increasing the temperature all the way to 2.0, the generated text becomes more creative and often less coherent.

Here's an example:

```
Once upon a time in a land far, far away

There stood one and no boy, the name came over in one. One that spoke so loudly he was the best that could play; they looked me in the eyes, he sat on
```

It's important to play around with these values in order to achieve the preferred output.

## Monitoring and Optimizing Performance

After running the script, it's crucial to monitor performance and optimize as needed. You can use `nvidia-smi` for real-time GPU monitoring and the Python `time` module for performance benchmarking.

### Monitoring GPU Utilization

To monitor real-time GPU usage, run:

```bash
nvidia-smi
```

### Benchmarking and Performance Tuning

To measure the script's execution time and evaluate GPU utilization, consider using the benchmarking script:

```python
# benchmark.py

import time
import torch
from transformers import GPT2LMHeadModel, GPT2Tokenizer

def generate_text(prompt, max_length=50, model_name='gpt2', top_k=50, top_p=0.9, temperature=0.8):
    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
    model = GPT2LMHeadModel.from_pretrained(model_name)
    tokenizer = GPT2Tokenizer.from_pretrained(model_name, clean_up_tokenization_spaces=True)
    model.to(device)
    inputs = tokenizer.encode(prompt, return_tensors='pt').to(device)
    attention_mask = torch.ones(inputs.shape, device=inputs.device)

    start_time = time.time()
    outputs = model.generate(
        inputs,
        max_length=max_length, 
        attention_mask=attention_mask,
        pad_token_id=tokenizer.eos_token_id,
        do_sample=True,
        top_k=top_k,
        top_p=top_p,
        temperature=temperature
    )
    end_time = time.time()

    print(f"Time taken: {end_time - start_time:.2f} seconds")
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

if __name__ == "__main__":
    prompt = "Once upon a time in a land far, far away"
    print(generate_text(prompt))
```

Run the script with:

```bash
python3 benchmark.py
```

Running this script will help you assess the performance of your model and guide optimization efforts.

## Optimization and Troubleshooting

### Fine-Tuning Performance

To maximize GPU efficiency, consider the following optimizations:

- **Mixed Precision Inference**: Use mixed precision to reduce memory usage and boost performance.
- **Batch Size Optimization**: Experiment with different batch sizes to balance memory usage and processing speed.

### Troubleshooting Common Issues

Even with a well-configured setup, issues can arise. Below are some common problems and their solutions:

1. GPU Access Issues

    - **Problem**: [Docker](/definitions/20240819_definition_docker.md) cannot access the GPU inside the container.
    - **Solution**: Ensure that the NVIDIA Container Toolkit is correctly installed and that you are using the `--gpus all` flag when running the container.

2. Out-of-Memory Errors

    - **Problem**: Out-of-memory (OOM) errors during inference.
    - **Solution**: Lower the `max_length` parameter or reduce batch sizes in your script. Consider using mixed precision to reduce memory usage.

3. Slow GPU Performance

    - **Problem**: Slow inference times despite using a GPU.
    - **Solution**: Verify that the script is utilizing the GPU by monitoring usage with `nvidia-smi`. If usage is low, optimize the script by adjusting sampling parameters, reducing model size, or increasing batch size within memory limits.

## Conclusion

This guide has walked you through setting up a [Docker](/definitions/20240819_definition_docker.md) environment for GPU-accelerated [LLM](/definitions/20240820_definition_large-language-model.md) inference. By following these steps, you can efficiently deploy and manage [LLMs](/definitions/20240820_definition_large-language-model.md), fully leveraging the power of GPUs for [natural language processing](/definitions/20240820_definition_natural-language-processing.md) tasks. Whether you're developing models for research or deploying them in production, [containerization](20240819_definition_containerization.md) with [Docker](/definitions/20240819_definition_docker.md) provides the scalability and efficiency needed to maximize your hardware resources.

By mastering these techniques, you'll ensure that your AI and machine learning projects are both powerful and efficiently deployed in any environment.

## References

- [Docker Documentation](https://docs.docker.com/get-started/)
- [NVIDIA Container Toolkit Documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/overview.html)
- [PyTorch CUDA Integration](https://pytorch.org/get-started/locally/)
- [Transformers Documentation](https://huggingface.co/docs/transformers/)
