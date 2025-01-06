---
title: 'GPU Utilization in Daytona for LLM Fine-Tuning and Inference'
description:
  'Learn how to setup gpu utilization in daytona and use it for llm 
  fine tuning and inference'
date: 2025-01-05
author: 'Tata Shalom'
tags: ['daytona', 'llm', 'gpu']
---

# GPU Utilization in Daytona for LLM Fine Tuning and Inference

## Introduction

GPUs (Graphics Processing Units) are specialized hardware designed to
accelerate the rendering of images, video, and animations. Originally
developed to handle the intense mathematical calculations required for rendering
graphics in real-time (like for video games), GPUs have evolved to become
versatile tools for a number of computational tasks. Over the last decade,
GPUs have transitioned from being purely graphics-focused components to becoming
essential for many non-graphics tasks.Their ability to handle massive
parallel computations has driven this shift.

## Overview of LLMs (Large Language Models)

Large Language Models (LLMs) are advanced AI systems designed to understand, generate,
and manipulate human language.Built using deep learning architectures, particularly transformer
models like GPT (Generative Pre-trained Transformer), LLMs are trained on vast datasets
comprising text from books,websites, and other sources.Their primary strength lies in generating
contextually relevant and coherent text based on user prompts.

  **Uses of LLMs**

- **Programming Assistance:** LLMs like GPT 4, Claude Sonnet 3.5 have been integrated into
programming by creating tools that generate code snippets and useful debugging tools.
- **Data Analysis:** LLMs can be used to summarize, extract insights, or analyze textual datasets
for numerous purposes.
- **Content Creation:** You can generate images, texts and to a certain extent videos with LLMs which
can be used by content creators to speed up their workflows
_ **Education:** Large Language Models can be used to explain complex concepts in a concise and structured
format, It can also be used for tutoring and creating a personalized learning experience.

## Overview of LLM Fine-Tuning

Fine-tuning is the process of adapting a pre-trained Large Language Model (LLM) to perform specific
tasks or excel in particular domains. While LLMs are initially trained on vast datasets to develop
a general understanding of language, fine-tuning leverages domain-specific data to refine the model’s
performance for specific applications. Fine-tuning is necessary because pre-trained Large Language Models (LLMs),
while good at general language understanding, often lack the precision required for numerous fields.
It enables models to become better by aligning them with the vocabulary, structure, and nuances of a particular
task or domain, thereby improving the quality and accuracy of outputs. Fine-tuning also allows for cost efficiency,
as it leverages pre-trained models instead of training from scratch, saving significant computational resources.
Additionally, it allows organizations to customize models to their specific application requirements, making them
more effective and contextually relevant.

  **Types Of Fine-Tuning**

- **Supervised Fine-Tuning:** This involves using labeled datasets where input-output pairs are defined
(e.g., translating text, answering questions, or summarizing content).
- **Reinforcement Learning from Human Feedback (RLHF):** A feedback-driven fine-tuning method where human evaluators
rate outputs, and the model learns to optimize for quality responses.
- **Few-shot or Zero-shot Fine-Tuning:** Few-Shot involves minimal additional training by conditioning the model
on a few examples or a task prompt, leveraging pre-existing knowledge.

  **Steps in Fine-Tuning**

- **Dataset Preparation:** This is the collection and preprocessing of task specific datasets, You should ensure
data is clean and representative of the task.
- **Model Configuration:** This is the process of choosing a pretrained model like GPT, BERT or LLaMA and configuring
parameters like learning rate, batch size and epochs, and epochs for training.
- **Training:**  Perform task-specific fine-tuning using the dataset while monitoring loss and accuracy metrics.
- **Validation:** Evaluate the fine-tuned model on unseen validation data to ensure its performance generalizes well.

## Overview of LLM Inference

Inference refers to the phase where a trained LLM is used to generate predictions or responses based on queries.
During inference, the model processes the input, retrieves relevant learned patterns, and outputs the most contextually
appropriate text.. The process begins with tokenizing the input into smaller units, such as words or subwords, which are
numerically encoded for model processing. The encoded tokens are passed through the LLM, where neural networks identify
contextual relationships between tokens. Based on these computations, the model predicts the most likely next token(s)
iteratively, generating the output text one token at a time. This continues until a stopping criterion, such as a specific
token or maximum length, is met. Finally, the generated tokens are decoded back into text and formattedas the final response.

  **Types of LLM Inference Tasks**

- **Text Generation:** This involves producing relevant texts for prompts e.g story writing, code generation e.t.c
- **Text Classification:**  This is the process of of categorizing input texts into different predefined labels using techniques
such as sentiment analysis.
- **Question Answering:** Extracting or generating answers based on a given question and context.
- **Summarization:** Condensing long text into concise summaries.
- **Translation:** Converting text from one language to another.

## Overview of Daytona

Daytona is a platform that simplifies the development environment setup by
offering dev environments for software developers. It enables users to create
and share fully configured development environments, allowing for faster
onboarding, collaboration, and consistent setups across teams.Daytona enables
you to manage and deploy Workspaces, which are reproducible development
environments built on standard OCI containers, and it includes native support
for the Dev Container standard. The architecture of Daytona is designed to
potentially support other configuration standards in the future, such as
Dockerfiles, Docker Compose, Nix, and Devfile.

**Features of Daytona**

- **Pre-configured Environments**: You can create environments with all
  dependencies, tools, and configurations pre-installed, so developers can start
  coding immediately without having to spend time configuring their setups.
- **Collaborative Workspaces**:The platform enables team collaboration by
  allowing multiple developers to work on the same environment. This can be
  particularly useful for pair programming, code reviews, or troubleshooting.
- **Containerized Environments**:Each development environment can be
  containerized, ensuring that the setup is consistent, reproducible, and
  isolated from other environments. This helps avoid the common "works on my
  machine" problem.
- **Reverse Proxy Support**:Daytona integrates a reverse proxy allowing you to
  access a workspace on a public or restricted network.

For more information about Daytona check out its [docs](https://daytona.io/docs)

In this guide you will learn how to build an environment using Daytona in which you can utilize your powerful Nvidia
GPU for the purpose of LLM Fine-Tuning and LLM Inference. Before you get started make sure you have
[Docker](https://docs.docker.com/get-started/get-docker/) installed, an IDE like [VS Code](https://code.visualstudio.com/download) or
[JetBrains](https://www.jetbrains.com/idea/download/),
[Daytona](https://www.daytona.io/docs/installation/installation/), [CUDA-enabled GPU](https://developer.nvidia.com/cuda-gpus), [Nvidia GPU Driver](https://www.nvidia.com/en-us/drivers/) and WSL(Window Sub-System for Linux) and a Linux Distribution like Ubuntu. Both Window and Linux users can follow
this guide, the only difference is potential driver installations which will be clarified later on in this guide.

## TL;DR

- A GPU (Graphics Processing Unit) is a specialized processor designed to accelerate graphics rendering
  and parallel computing tasks, commonly used in gaming, AI, and data-intensive applications.
- A Large Language Model (LLM) is an AI system trained on vast text data to understand, generate,
  and manipulate human language for various tasks like text generation, translation, and question answering.
- LLM fine-tuning is the process of adapting a pre-trained language model to a specific task or domain by
  training it further on specialized data.
- LLM inference is the process of using a trained language model to generate responses or predictions based
  on input text.
- Daytona simplifies setting up developer playgrounds by providing reproducible,
  isolated environments with easy management and flexible configuration options.
- Prerequisites to follow this guide: Docker, IDE(VS Code or JetBrains), Daytona,
  WSL and CUDA Compatible GPU and its drivers.

You can find the Github repository where my devcontainer configuration files
which i used for this guide
[here](https://github.com/stdthoth/daytona-gpu-utilization).

## Setup a Daytona configuration for GPU Utilization

Here, you're going to create a dev container using a `devcontainer.json` file, a
`Dockerfile` and a `docker-compose.yml` file. One of Daytona's remarkable
qualities is the ability to a build a project image according to the dev
container standard. You can find out more about Daytona Builders
[here](https://www.daytona.io/docs/usage/builders/).
Before setting up the dev container configuration you should verify if your GPU
is CUDA compatible,if the drivers are installed on the host machine and the Nvidia
Container Toolkit installation status.

- **Step 1:** Verify GPU driver status and install Nvidia Container Toolkit

  To verify your drver status open your terminal and run this command

  ```bash
  nvidia-smi
  ```
  You should get an output resembling the below image

  ![image of github provider](assets/20250105_daytona_gpu_utilization_img_1.png)

  If you do not have drivers installed get them from [here](https://www.nvidia.com/en-us/drivers/)
  depending on your OS and GPU,If drivers are installled open your WSL distribution and check if
  the Nvidia Container Toolkit is installed with

  ```bash
    dpkg -l | grep nvidia-container-toolkit
  ```
  If installed it will show the package version, if it isn't installed run this command

  ```bash
    sudo apt-get install -y nvidia-container-toolkit
  ```
  Configure the runtime with this command
  
  ```bash
    sudo nvidia-ctk runtime configure
    sudo systemctl restart docker
  ```
  Once everything is setup you can run a CUDA enabled container with GPU access with
  this command

  ```bash
    docker run --gpus all nvidia/cuda:12.0-base nvidia-smi
  ```
  Ensure that the Windows/Linux drivers are compatible with the CUDA version in your Docker image,
  i.e a driver version of 12.5 should be used with a CUDA docker image of version 12.5 or less
  since there is backward compatibilty between them.

  > **Important Note:** For windows users If you have Nvidia GPU drivers already installed on their
  >system, CUDA becomes available within WSL2. The CUDA driver installed on windows will be stubbed
  >inside the WSL2, therefore users must not install any Nvidia GPU Linux driver within WSL2 to
  >avoid conflicts.