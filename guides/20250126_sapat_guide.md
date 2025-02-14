---
title: 'Building AI-Powered Tools: A Guide to Whisper and Sapat'
description:
  'A brief description of what the guide covers. The description should be a
  maximum of 160 characters.'
date: 2025-01-26
author: 'Jeffrey Whewhetu'
tags: ['model', 'open source', 'transcription']
---

# Building AI-Powered Tools: A Guide to Whisper and Sapat

## Introduction

Artificial Intelligence (AI) is transforming how we build and interact with software tools. From automation to intelligent decision-making, AI-powered solutions can enhance efficiency, accuracy, and user experience. However, developing an AI-powered tool requires careful planning, iterative prototyping, and robust implementation.

This guide walks you through the essential steps of prototyping and building an AI-powered tool called Sapat using Whisper model — from defining the problem and selecting the right AI model for better performance and efficiency. This guide will help you navigate the process and creation of impactful AI-driven solution for transcription.

## TL;DR

- Prerequisites: Basic Python knowledge, Daytona installed, and an API key for Whisper model.
- What is Whisper? It is an open-source automatic speech recognition (ASR) model by OpenAI. It supports over 100 languages, works well in noisy environments, understands context and accents, and scales for both small and large transcription tasks.
- What is Sapat? It is the prototype and built AI-enabled tool that uses Whisper for transcription. It simplifies integration with multiple AI providers such as Groq Cloud, Azure OpenAI and OpenAI, Sapat ensures flexibility, scalability, and performance.
- Why It Matters: This guide shows how to quickly prototype and build AI-powered tools using Whisper, making transcription accessible and scalable.

## Prerequisites

Before continue your reading, ensure you have:
1. Some level of Python programming experience.
1. **Daytona**: Install Daytona from [here](https://github.com/daytonaio/daytona).
2. **API Access**: Obtain an API key from any Whisper providers (e.g., OpenAI, Groq, or Azure OpenAI).

## What is Whisper?

Whisper is an open-source automatic speech recognition (ASR) model developed by OpenAI. It is trained on a massive dataset of multilingual and multitask supervised data, making it one of the most robust and versatile transcription tools available today. Whisper can handle a wide range of audio inputs, from clear studio recordings to noisy, real-world environments.

### Key Features of Whisper

1. **Multilingual Support**: Whisper supports over 100 languages, making it ideal for global applications. Whether you're transcribing English, Spanish, Mandarin, or Swahili, Whisper delivers accurate results.

2. **Noise Robustness**: Whisper excels in noisy environments. It can filter out background noise, overlapping speech, and other audio distortions, ensuring high-quality transcriptions even in challenging conditions.

3. **Contextual Understanding**: Whisper is designed to understand context, accents, and dialects. This makes it suitable for transcribing domain-specific content, such as medical terminology, legal jargon, or technical discussions.

4. **Open-Source and Customizable**: Whisper is open-source, allowing developers to fine-tune the model for specific use cases. This flexibility makes it a popular choice for researchers and AI engineers.

5. **Scalability**: Whisper can handle both small-scale and large-scale transcription tasks, making it ideal for individual projects or enterprise-level applications.

## Introducing Sapat: A Whisper-Powered Transcription CLI Tool

Sapat goes beyond simply wrapping Whisper; it enhances the transcription workflow with a suite of valuable features.  From automatic video-to-audio conversion and flexible multi-API support (including OpenAI, Groq Cloud, and Azure OpenAI) to batch processing and customizable parameters, Sapat is designed for efficiency and control.  Whether you're transcribing a single file or managing a large batch, Sapat simplifies every step of the process, delivering accurate and reliable results.

Sapat is used as a case study to demonstrate the process of prototyping and building an AI-powered tool—from concept to implementation.

### Key Features of Sapat
- **Video-to-Audio Conversion**: Automatically converts video files to MP3 format for transcription.
- **Multi-API Support**: Works with Whisper-powered APIs like OpenAI, Groq, and Azure OpenAI.
- **Batch Processing**: Transcribes multiple files or entire directories at once.
- **Customizable Parameters**: Adjust language, audio quality, and prompts for better results.
- **Temporary File Cleanup**: Automatically removes intermediate files after transcription.

## Prototyping and Building Sapat

### Step 1: Define the Problem and Scope

Before diving into code, clearly define the problem you're solving. For Sapat, the goal is to create a transcription tool that:

- Integrates with multiple Whisper-powered APIs.
- Supports batch processing for efficiency.
- Offers customizable parameters for better transcription results.

### Step 2: Set Up the Development Environment

- Install Daytona: Follow the installation instructions [here](https://github.com/daytonaio/daytona).
- Development Environment Setup: To set up the development environment, we use a `.devcontainer/devcontainer.json` file to configure a Dev Container. It sets up a development environment with pre-installed tools and dependencies, ensuring a smooth development experience.

```
{
    "name": "Video Transcription Tool",
    "image": "mcr.microsoft.com/devcontainers/python:3.12",
    "customizations": {
      "vscode": {
        "settings": {
          "python.defaultInterpreterPath": "/usr/local/bin/python",
          "python.linting.enabled": true,
          "python.linting.pylintEnabled": true
        },
        "extensions": [
          "ms-python.python",
          "ms-python.vscode-pylance",
          "njpwerner.autodocstring"
        ]
      }
    },
    "mounts": [
      {
        "source": "${localEnv:HOME}",
        "target": "${containerWorkspaceFolder}/con-home",
        "type": "bind"
      }
    ],
    "onCreateCommand": {
      "update": "sudo apt update && sudo apt upgrade -y",
      "ownership": "sudo chown -R $USER:$USER ${containerWorkspaceFolder}"
    },
    "postCreateCommand": {
      "ffmpeg": "sudo apt install ffmpeg -y",
      "requirements": "pip install -r requirements.txt"
    }
}
```
- Dependencies. The project relies on several Python packages, which are listed in `requirements.txt`:

```
python-dotenv
requests
click
openai
groq
build
```

### Step 3: Project Structure and Configuration

- Project structure. The project is organized as follows:
```
├── pyproject.toml
├── README.md
├── requirements.txt
└── src
    ├── sapat
        ├── __init__.py
        ├── script.py
        └── transcription
            ├── azure.py
            ├── base.py
            ├── groq.py
            ├── __init__.py
            └── openai.py
```

- Project Configuration. The `pyproject.toml` file defines the project metadata and dependencies:
```
[project]
name = "sapat"
version = "0.1.2"
description = "Video Transcription Tool using different APIs"
requires-python = ">=3.6"
dependencies = [
    "click>=8.1.8",
    "requests>=2.32.3",
    "python-dotenv>=1.0.1",
    "openai>=1.58.1",
    "groq>=0.13.1"
]

[project.scripts]
sapat = "sapat.script:main"

[build-system]
requires = ["wheel", "setuptools>=61.0"] # Ensure setuptools is recent enough
build-backend = "setuptools.build_meta"
```

- `src/sapat/` directory: Contains the main application code, including the CLI script and API implementations of each Whisper model providers can be found in `src/sapat/transcription` directory.

### Step 4: Implementation of Core Features

- **Base Class Implementation**. The `src/sapat/transcription/base.py` file defines a base class (`TranscriptionBase`) that provides common functionality for all transcription APIs, such as audio file conversion and processing. This ensures consistency and reduces code duplication across different API implementations.
```
from abc import ABC, abstractmethod
from pathlib import Path
import subprocess
import click


class TranscriptionBase(ABC):
    """
    Base class for transcription APIs.
    """

    @staticmethod
    def convert_to_mp3(input_file: str, output_file: str, quality: str):
        """
        Converts an audio file to MP3 format using FFmpeg.

        Parameters:
        - input_file (str): Path to the input file.
        - output_file (str): Path to the output MP3 file.
        - quality (str): Desired audio quality ('L', 'M', 'H').
        """
        if quality == 'L':
            ffmpeg_options = ['-ar', '22050', '-ac', '1', '-b:a', '96k']
        elif quality == 'M':
            ffmpeg_options = ['-ar', '44100', '-ac', '1', '-b:a', '96k']
        elif quality == 'H':
            ffmpeg_options = ['-ar', '44100', '-ac', '2', '-b:a', '192k']
        else:
            raise ValueError("Invalid quality option. Choose from 'L', 'M', 'H'.")

        command = ['ffmpeg', '-i', input_file, '-vn'] + ffmpeg_options + [output_file]
        subprocess.run(command, check=True)


    def process_file(self, input_file, language, prompt, temperature, quality, correct):
        input_path = Path(input_file)
        mp3_file = input_path.with_suffix('.mp3')
        txt_file = input_path.with_suffix('.txt')

        click.echo(f"Processing {input_file}")

        if not mp3_file.exists():
            self.convert_to_mp3(str(input_path), str(mp3_file), quality)
            click.echo("Conversion to MP3 completed")
        else:
            click.echo("MP3 file already exists, skipping conversion")

        transcription_result = self.transcribe_audio(str(mp3_file), language=language, prompt=prompt, temperature=temperature)
        click.echo("Transcription completed")

        if correct:
            system_prompt = "You are a helpful assistant. Your task is to correct any spelling discrepancies in the transcribed text. Make sure that the names of the following products are spelled correctly: {user provided prompt} Only add necessary punctuation such as periods, commas, and capitalization, and use only the context provided."
            corrected_text = self.generate_corrected_transcript(str(mp3_file), 0.7, system_prompt)
            click.echo("Correction completed")
        else:
            corrected_text = transcription_result

        with open(txt_file, 'w', encoding='utf-8') as f:
            if isinstance(corrected_text, dict):
                f.write(corrected_text.get('text', ''))
            else:
                f.write(corrected_text)
        click.echo(f"Transcription saved to {txt_file}")

        mp3_file.unlink()

    @abstractmethod
    def transcribe_audio(self, audio_file: str, **kwargs):
        """
        Abstract method for transcribing audio files. Must be implemented by subclasses.

        Parameters:
        - audio_file (str): Path to the audio file to be transcribed.
        - kwargs: Additional arguments for transcription.

        Returns:
        - The transcription result (implementation-specific).
        """
        pass

    @staticmethod
    def generate_corrected_transcript(audio_file, temperature, prompt):
        """
        Default implementation for generating corrected transcripts. Can be overridden by subclasses.
        """
        raise NotImplementedError("Correction not implemented for this API.")
```

- **Implementation of Groq Cloud Whisper API**. The `src/sapat/transcription/groq.py` file implements the `GroqCloudTranscription` class, which extends the `TranscriptionBase` class to provide transcription functionality using the Groq Cloud API.
```
import os
import requests
from dotenv import load_dotenv
from groq import Groq
from .base import TranscriptionBase

# Load environment variables
load_dotenv(".env")

class GroqCloudTranscription(TranscriptionBase):
    """
    GroqCloud API implementation for transcription.
    """

    def __init__(self, temperature: float, response_format: str = "json"):
        """
        Initializes the GroqCloudTranscription class.

        Parameters:
        - temperature (float): Default temperature value for transcription.
        - response_format (str): Default response format for transcription.
        """
        self.api_key = os.getenv('GROQCLOUD_API_KEY')
        self.model = os.getenv('GROQCLOUD_MODEL')
        self.endpoint = os.getenv('GROQCLOUD_API_ENDPOINT')
        self.model_name_chat = os.getenv('GROQCLOUD_MODEL_NAME_CHAT')
        self.temperature = temperature
        self.response_format = response_format
        self.max_file_size_mb = 25

    def transcribe_audio(self, audio_file: str, **kwargs):
        """
        Transcribes an audio file using GroqCloud API.

        Parameters:
        - audio_file (str): Path to the audio file.
        - kwargs: Additional parameters for transcription.

        Returns:
        - dict or str: The transcription result.
        """
        self._validate_audio_file(audio_file)

        headers = {
            "Authorization": f"Bearer {self.api_key}",
        }
        data = {
            "model": kwargs.get("model", self.model),
            "response_format": kwargs.get("response_format", self.response_format),
            "temperature": kwargs.get("temperature", self.temperature),
        }

        if "language" in kwargs:
            data["language"] = kwargs["language"]
        if "prompt" in kwargs:
            data["prompt"] = kwargs["prompt"]

        with open(audio_file, 'rb') as f:
            files = {'file': f}
            response = requests.post(self.endpoint, headers=headers, data=data, files=files)

        if response.status_code == 200:
            if data["response_format"] in ["json", "verbose_json"]:
                return response.json()
            return response.text
        else:
            raise Exception(f"Transcription failed: {response.text}")

    def generate_corrected_transcript(self, audio_file: str, temperature: float, system_prompt: str):
            """
            Uses a chat API to correct the transcription text.

            Parameters:
            - audio_file (str): Path to the audio file for transcription.
            - temperature (float): The sampling temperature for the chat API.
            - system_prompt (str): The system prompt to guide the assistant.

            Returns:
            - str: The corrected transcription.
            """
            client = Groq(
                api_key=self.api_key
            )

            # First, get the transcription text
            transcription = self.transcribe_audio(audio_file)
            transcription_text = transcription.get('text', '') if isinstance(transcription, dict) else transcription

            # Use the chat API to correct the text
            response = client.chat.completions.create(
                model=self.model_name_chat,
                temperature=temperature,
                messages=[
                    {
                        "role": "system",
                        "content": system_prompt
                    },
                    {
                        "role": "user",
                        "content": transcription_text
                    }
                ]
            )
            return response.choices[0].message.content


    def _validate_audio_file(self, audio_file: str):
        """
        Validates the audio file for size and format.

        Parameters:
        - audio_file (str): Path to the audio file.

        Raises:
        - Exception: If the file is invalid.
        """
    
        # Ensure the converted value is a valid file path
        if not os.path.exists(audio_file):
            raise ValueError(f"File {audio_file} does not exist.")

        file_size_mb = os.path.getsize(audio_file) / (1024 * 1024)
        if file_size_mb > self.max_file_size_mb:
            raise Exception(f"File size exceeds the maximum limit of {self.max_file_size_mb} MB.")

        valid_extensions = ['.mp3', '.wav', '.flac']
        if not any(str(audio_file).endswith(ext) for ext in valid_extensions):
            raise ValueError(f"Unsupported audio file format: {audio_file}. Supported formats are {valid_extensions}.")
```

- **Main Script**. The main script `src/sapat/script.py`, handles the transcription logic:
```
import click
from pathlib import Path
from .transcription.groq import GroqCloudTranscription
from .transcription.azure import AzureTranscription
from .transcription.openai import OpenAITranscription

@click.command()
@click.argument("input_path", type=click.Path(exists=True))
@click.option("--language", "-l", default="en", help="Language of the audio (default: en)")
@click.option("--prompt", "-p", help="Optional prompt to guide the model")
@click.option("--temperature", "-t", type=float, default=0.3, help="Sampling temperature (default: 0.3)")
@click.option("--quality", "-q", type=click.Choice(['L', 'M', 'H'], case_sensitive=False), default='M', help="Quality of the MP3 audio: 'L' for low, 'M' for medium, and 'H' for high (default: 'M')")
@click.option("--correct", is_flag=True, help="Use LLM to correct the transcript")
@click.option("--api", "-a", type=click.Choice(['openai', 'groq', 'azure'], case_sensitive=True), required=True, help="API to use for the transcription ('openai', 'groq' or 'azure')")
def main(input_path, language, prompt, temperature, quality, correct, api):
    """
    Transcribe video files using different APIs.

    INPUT_PATH is the path to the video file or directory containing video files.
    """
    # Initialize the correct transcription object
    input_path = Path(input_path)

    # Handle file processing based on API choice
    if api.lower() == "groq":
        transcriber = GroqCloudTranscription(temperature=temperature)
    elif api.lower() == "azure":
        transcriber = AzureTranscription(temperature=temperature)
    elif api.lower() == "openai":
        transcriber = OpenAITranscription(temperature=temperature)
    else:
        click.echo(f"Unsupported API: {api}")
        return

    if input_path.is_file():
        transcriber.process_file(input_path, language, prompt, temperature, quality, correct)
    elif input_path.is_dir():
        for file in input_path.glob('*.mp4'):
            transcriber.process_file(file, language, prompt, temperature, quality, correct)
    else:
        click.echo(f"{input_path} is not a valid file or directory.")

if __name__ == "__main__":
    main()
```

- **Environment Variables**. The `.env.example` file contains the necessary API keys and endpoints:
```
AZURE_OPENAI_API_KEY=
AZURE_OPENAI_ENDPOINT=https://DEPLOYMENTENDPOINTNAME.openai.azure.com
AZURE_OPENAI_DEPLOYMENT_NAME_WHISPER=whisper
AZURE_OPENAI_API_VERSION_WHISPER=2024-06-01
AZURE_OPENAI_DEPLOYMENT_NAME_CHAT=gpt-4o
AZURE_OPENAI_API_VERSION_CHAT=2023-03-15-preview

GROQCLOUD_API_KEY=
GROQCLOUD_MODEL=whisper-large-v3-turbo
GROQCLOUD_API_ENDPOINT=https://api.groq.com/openai/v1/audio/transcriptions
GROQCLOUD_MODEL_NAME_CHAT=llama3-8b-8192

OPENAI_API_KEY=
OPENAI_MODEL=whisper-1
OPENAI_API_ENDPOINT=https://api.openai.com/v1/audio/transcriptions
OPENAI_MODEL_NAME_CHAT=gpt-4o
```

## Usage of Sapat

### Installation

### CLI Usage Example

Transcribe an entire directory using OpenAI:
```
sapat path/to/video_files/ --quality H --api openai
```

Transcribe a single file using Groq Cloud:
```
sapat path/to/video.mp4 --quality --language en --api groq
```

## Tips for Maximizing Whisper's Potential with Sapat

1. **Optimize Audio Quality**:
   - Use high-quality audio files (`--quality H`) for better results.
   - Remove background noise before transcription if possible.

2. **Leverage Prompts**:
   - Provide a `--prompt` to guide Whisper for specific contexts or terminology.
   - Example: Use a prompt like "Medical terms: diagnosis, prognosis, treatment" for healthcare-related content.

3. **Batch Processing**:
   - Save time by transcribing multiple files at once:
     ```bash
     sapat path/to/audio_files/ --api groq
     ```

## Conclusion

In conclusion, Sapat serves as a demo example of how simple it can be to prototype and build AI-enabled tools. By leveraging Whisper through AI providers like OpenAI, Groq Cloud, and Azure OpenAI, Sapat demonstrates how developers can quickly integrate advanced AI capabilities such as transcription into their applications. The process of building Sapat highlights the ease of working with modern AI platforms, where the heavy lifting of integration and scalability is handled seamlessly. This allows developers to focus on designing and refining their tools, rather than getting bogged down by technical complexities.

## References

- _[Whisper by OpenAI](https://openai.com/research/whisper)_

- _[Sapat GitHub Repository](https://github.com/nkkko/sapat)_

- _[Daytona Official Website](https://daytona.io)_

