---
title: 'Guide to Using Sapat: The Video Transcription Tool'
description:
  'A brief description of what the guide covers. The description should be a
  maximum of 160 characters.'
date: 2025-01-26
author: 'Jeffrey Whewhetu'
tags: ['model', 'transcribe', 'video transcription', 'transcription tool']
---

# Guide to Using Sapat: The Video Transcription Tool

## Introduction

Sapat is a versatile and efficient tool designed to simplify transcription workflows by leveraging powerful AI models. Whether you're a content creator, a researcher, or a developer, Sapat enables you to convert video and audio files into accurate transcriptions using services like Azure OpenAI, Groq, and OpenAI.  

This guide will walk you through Sapat's features, setup process, and best practices to help you make the most of this tool.  

## TL;DR
- Prerequisites
- What's Sapat, it's features and how it Works
- The AI model that powers Sapat. Whisper, what is it and it's features
- Installation of Sapat using Daytona
- How to Transcribe with Sapat
- Tips and Best Practices
- Common issues and Troubleshootings
- Conclusion
- References

## Prerequisites

Before using Sapat, ensure you have the following:  

- [Daytona](https://daytona.io) installed on your system.

- **API access key** for any of the supported services:
  - Azure OpenAI  
  - Groq Cloud  
  - OpenAI

## What's Sapat?  

Sapat is a transcriptoon tool designed to transcribe video and audio files using state-of-the-art AI model - OpenAI's Whisper. By supporting multiple APIs, it gives users flexibility and reliability in generating transcriptions quickly and accurately.  

## Features

Sapat offers a range of powerful features to simplify and enhance your transcription workflow. From built-in video-to-audio conversion to flexible multi-API support. Sapat provides everything you need for accurate and efficient transcriptions.

- **Video-to-Audio Conversion**: Converts video files into MP3 format using ffmpeg for transcription.

- **Multi-API Support**: Works with Azure OpenAI, Groq, and OpenAI APIs.

- **Batch Processing**: Handles individual files or entire directories for transcription.

- **Customizable Parameters**: Adjust language, audio quality, temperature, and prompts to guide transcription models.

- **Temporary File Cleanup**: Automatically removes intermediate MP3 files after transcription.

## How It Works  

Sapat's process is designed for ease of use and efficiency.  Simply provide your audio, video or even a directory containing your audio or video files, and Sapat handles the conversion, transcription, and cleanup, delivering a ready-to-use text file.

1. **Input File**: Sapat accepts video or audio files as input.

2. **Audio Conversion**: Videos are converted to MP3 format using ffmpeg.

3. **API Transcription**: The audio file is sent to the selected API for transcription.

4. **Output**: The transcription is saved as a `.txt` file in the same directory as the input file.

5. **Cleanup**: Temporary files (e.g., MP3) are deleted after transcription.

## The AI Model that powers Sapat: Whisper

Whisper is an open-source automatic speech recognition (ASR) model developed by OpenAI. It is trained on a massive dataset of multilingual and multitask supervised data, making it one of the most robust and versatile transcription tools available today. Whisper can handle a wide range of audio inputs, from clear studio recordings to noisy, real-world environments.

Sapat leverages the power of OpenAI's Whisper model to provide accurate and reliable transcriptions.  Sapat's multi-API architecture allows users to select Whisper through various providers, including OpenAI, Azure OpenAI, and Groq Cloud. This flexibility gives users access to this cutting-edge transcription technology through their preferred platform. By supporting multiple APIs, Sapat provides redundancy and choice, allowing users to optimize for cost, performance, or availability.

### Features of Whisper

### 1. **Multilingual Support**

Whisper supports over 100 languages, making it ideal for global applications. Whether you're transcribing English, Spanish, Mandarin, or Swahili, Whisper delivers accurate results.

### 2. **Noise Robustness**

Whisper excels in noisy environments. It can filter out background noise, overlapping speech, and other audio distortions, ensuring high-quality transcriptions even in challenging conditions.

### 3. **Contextual Understanding**

Whisper is designed to understand context, accents, and dialects. This makes it suitable for transcribing domain-specific content, such as medical terminology, legal jargon, or technical discussions.

### 4. **Open-Source and Customizable**

Whisper is open-source, allowing developers to fine-tune the model for specific use cases. This flexibility makes it a popular choice for researchers and AI engineers.

### 5. **Scalability**

Whisper can handle both small-scale and large-scale transcription tasks, making it ideal for individual projects or enterprise-level applications.

## Setup Sapat in Daytona Workspace for Transcription

1. Create a Daytona workspace with the command below. The IDE you set as default in Daytona should open in a few second after running the command.

```
daytona create https://github.com/nkkko/sapat
```

2. Run this command to build a distribution. It would be be in the `dist` directory.
```
python -m build
```

3. Run the command to install the distribution wheel

```
pip install dist/sapat-0.1.1-py3-none-any.whl  # Replace with the actual filename displayed after previous command is ran
```

4. Create a `.env` file in the project root and add your API credentials. I use Groq Cloud API but you can use other supported APIs.

```
# Groq
GROQCLOUD_API_KEY=your_groq_api_key_here
GROQCLOUD_MODEL=whisper-large-v3-turbo
GROQCLOUD_API_ENDPOINT=https://api.groq.com/openai/v1/audio/transcriptions
GROQCLOUD_MODEL_NAME_CHAT=llama3-8b-8192
```

## How to Transcribe a Video File with Sapat  

1. **Run the Transcription Command**:  
   ```bash
   sapat path/to/my_video.mp4 --quality H --language en --api groq
   ```  
   - Replace `path/to/my_video.mp4` with path to your video file.  
   - Use the `--quality` option to set MP3 quality (`L`, `M`, `H`).  

2. **View Results**:  
   - A file named `my_video.txt` will be created in the same directory as the video file, containing the transcription.  


## How to Transcribe an Audio File with Sapat

1. **Run the Transcription Command**:  
   ```bash
   sapat path/to/my_audio.mp3 --language es --api groq
   ```  
   - Replace `path/to/my_audio.mp3` with path to your audio file.  
   - Add a `--prompt` to guide the transcription model if needed.  

2. **Output**:  
   - The transcription will be saved as `my_audio.txt` in the same directory.  

## Tips and Best Practices  

- **Choose the Right API**: Use the API that suits your transcription needs:  
  - Azure OpenAI for enterprise solutions.  
  - Groq for faster processing.  
  - OpenAI for general transcription.

- **Optimize Audio Quality**: For best results, use high-quality audio (`--quality H`).

- **Leverage Prompts**: Provide a `--prompt` to guide the transcription model for specific contexts or terminology.

- **Batch Process**: Save time by processing an entire directory instead of individual files.

## Common Issues and Troubleshooting  

### Issue: Missing `.env` File  

- Ensure the `.env` file is in the project root and contains valid API credentials.  

### Issue: API Errors

- **Rate Limits**: Ensure your API account has sufficient credits or quotas.
- **Invalid Keys**: Double-check your API credentials in the `.env` file.

### Issue: Poor Transcription Accuracy

- Use a clearer audio source.  
- Specify the correct language using the `--language` option.  
- Provide a contextual `--prompt` to improve transcription quality.  

## Conclusion  

Sapat is a powerful tool that simplifies the transcription of video and audio files using leading AI services. By following this guide, you can set up Sapat, transcribe files with ease, and troubleshoot common issues.  

Sapat offers a flexible and robust solution for all your transcription needs, leveraging the capabilities of Whisper model. With multi-API support and customizable parameters, Sapat adapts to your specific requirements, providing accurate and reliable transcriptions.

## References

- _[Daytona Official Website](https://daytona.io)_

- _[Source Cdoe Repository for Sapat Transcription Tool](https://github.com/nkkko/sapat)_
