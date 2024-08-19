---
title: "Transcribe Video and Audio with Python"
description: "This guide provides a comprehensive step-by-step process for setting up and using Sapat to automatically transcribe video and audio files using Azure OpenAI's Whisper API."
date: 2024-08-19
author: "Jacob Gaffke"
---

# Transcribe Video and Audio with Python

## Introduction

Transcribing video and audio files is essential in various fields, from content creation to legal documentation and academic research. Manual [transcription](/definitions/transcription.md) is labor-intensive and error-prone, making automation an invaluable tool. This guide introduces [a Python-based tool](https://github.com/nkkko/sapat) that automates the [transcription](/definitions/transcription.md) of video files by converting them into MP3 format, transcribing the audio using one of a variety of supported advanced AI models, and saving the [transcription](/definitions/transcription.md) as a text file. Whether you're a content creator, a researcher, or someone needing to convert speech into text, this guide will help you accomplish your tasks efficiently.

By following this guide, you will learn how to set up the necessary environment, install the required software, and use the [transcription](/definitions/transcription.md) tool. The tool supports processing individual video files or entire directories, ensuring temporary MP3 files are cleaned up after [transcription](/definitions/transcription.md). You can choose between using Azure OpenAI's Whisper API or Rev AI API based on your preference and access. A basic understanding of Python and command-line operations, as well as access to the relevant API, is required.

### Prerequisites

Before diving into the [transcription](/definitions/transcription.md) process, ensure that the following prerequisites are met:

1. **Python 3.6+**: The tool requires Python version 3.6 or later. Python is a versatile programming language widely used for automation tasks, including data processing and machine learning.
   
2. **ffmpeg**: A free and open-source software suite for handling multimedia data, ffmpeg allows the tool to convert video files into MP3 format. Ensure ffmpeg is installed and available in your system PATH.

3. **API Access**: You can choose between the Azure OpenAI API or Rev AI API for [transcription](/definitions/transcription.md). Make sure you have an API key or token to access the chosen service.

4. **Basic Command-Line Knowledge**: Familiarity with command-line operations is necessary to install dependencies, run scripts, and troubleshoot any issues that might arise.

With these prerequisites met, you’ll be able to follow the steps outlined in this guide to achieve accurate and efficient [transcription](/definitions/transcription.md)s using your preferred API.

### TL;DR

- **Automated Transcription**: Convert videos to MP3 and transcribe them using Azure OpenAI's Whisper API or Rev AI API.
- **Batch Processing**: Support for processing individual video files or entire directories of videos.
- **Cleanup**: Automatic deletion of temporary MP3 files after [transcription](/definitions/transcription.md).
- **Customizable**: Options to specify language, prompt, and audio quality.
- **API Flexibility**: Choose between Azure OpenAI's Whisper API or Rev AI API for [transcription](/definitions/transcription.md).

## Prerequisites

### Install Python and ffmpeg

To begin with, you need to have Python and ffmpeg installed on your system.

#### Python

Ensure that Python 3.6 or later is installed. You can download it from the [official Python website](https://www.python.org/downloads/). After installation, verify it by running the following command in your terminal or command prompt:

```bash
python --version
```

You should see a version number that starts with 3.6 or higher.

#### ffmpeg

ffmpeg is crucial for converting video files to MP3 format. Download and install ffmpeg from the [ffmpeg website](https://ffmpeg.org/download.html). After installation, ensure that ffmpeg is accessible from your system's PATH. To check if ffmpeg is correctly installed, run:

```bash
ffmpeg -version
```

This command should output the version details of ffmpeg, indicating that it is installed and ready to use.

### Clone the Repository

Next, you need to clone the [transcription](/definitions/transcription.md) tool's [repository](/definitions/repository.md) from GitHub. This [repository](/definitions/repository.md) contains all the code and dependencies required for the tool to function.

Open your terminal or command prompt and run the following commands:

```bash
git clone https://github.com/nkkko/sapat.git
cd sapat
```

These commands will download the [repository](/definitions/repository.md) to your local machine and navigate into the project directory.

### Install Required Packages

The tool relies on several Python packages that need to be installed before you can use it.

In the project directory, install the necessary Python packages by running:

```bash
pip install .
```

This command reads the `pyproject.toml` file and installs all listed packages. These packages include libraries for interacting with the Azure OpenAI API, Rev AI API, handling environment variables, and managing multimedia files.

### Configure API Credentials

The tool supports both Azure OpenAI's Whisper API and Rev AI API for [transcription](/definitions/transcription.md). You need to configure your API credentials depending on the service you choose to use.

#### Azure OpenAI

If you are using the Azure OpenAI Whisper API, create a `.env` file in the project root directory and add your Azure OpenAI credentials. The `.env` file should include the following lines:

```env
AZURE_OPENAI_API_KEY=your_api_key_here
AZURE_OPENAI_ENDPOINT=https://DEPLOYMENTENDPOINTNAME.openai.azure.com
AZURE_OPENAI_DEPLOYMENT_NAME_WHISPER=whisper
AZURE_OPENAI_API_VERSION_WHISPER=2024-06-01
AZURE_OPENAI_DEPLOYMENT_NAME_CHAT=gpt-4o
AZURE_OPENAI_API_VERSION_CHAT=2023-03-15-preview
```

Replace `your_api_key_here` with your actual Azure OpenAI API key, and adjust the endpoint and deployment names as per your Azure setup. This configuration allows the tool to authenticate and interact with the Whisper API for [transcription](/definitions/transcription.md).

#### Rev AI

If you prefer to use Rev AI for [transcription](/definitions/transcription.md), you can configure your access token by adding the following line to the `.env` file:

```env
REVAI_ACCESS_TOKEN=your_token_here
```

Replace `your_token_here` with your actual Rev AI access token. This configuration enables the tool to authenticate and interact with Rev AI for [transcription](/definitions/transcription.md).

With these preparatory steps completed, you are now ready to proceed with the main process of [transcription](/definitions/transcription.md) using either Azure OpenAI or Rev AI.

## Workflow

### Building and Installing the Package

The tool can be built and installed as a Python package, making it easy to run from any directory on your system.

#### Build the Distribution Package

Use Python’s build tool to create a distribution package. Run the following command in the project directory:

```bash
python -m build
```

This command packages the tool into a wheel file (`.whl`) located in the `dist` directory. A wheel file is a distribution format for Python packages that allows for easy installation.

#### Install the Package

Once the package is built, you can install it using pip. Replace `sapat-0.1.1-py3-none-any.whl` with the actual filename generated during the build process:

```bash
pip install dist/sapat-0.1.1-py3-none-any.whl
```

Installing the package in this way makes the tool globally available on your system, meaning you can run it from any directory.

### Adding the Tool to PATH

In some cases, the tool may not automatically be added to your system's PATH. If this happens, you'll need to manually add it.

#### Linux/macOS

On Linux or macOS, the installed script is typically located in the `~/.local/bin` directory. Add this directory to your PATH by editing your shell configuration file (`~/.zshrc` or `~/.bashrc`):

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

This command appends the directory to your PATH and reloads the shell configuration.

#### Windows

On Windows, the installed script is usually found in a directory like `%USERPROFILE%\AppData\Local\Programs\Python\Python39\Scripts`, depending on your Python version. To add this directory to your PATH:

1. Right-click on `This PC` or `My Computer` and select `Properties`.
2. Click on `Advanced system settings` and then on the `Environment Variables` button.
3. In the `System variables` section, find the `Path` variable and click `Edit`.
4. Add the directory path to the list and click `OK`.

This manual PATH setup ensures that you can run the tool from any command prompt or terminal session.

### Using the Transcription Tool

Now that everything is set up, you can start using the [transcription](/definitions/transcription.md) tool to convert video files into text using either Azure OpenAI's Whisper API or Rev AI API.

You can transcribe a single video file or an entire directory of video files by specifying the file or directory as an argument. For example, to use Azure OpenAI's Whisper API:

```bash
sapat my_video.mp4 --quality H --language

es --prompt "This is a test prompt" --temperature 0.5
```

To use Rev AI API, ensure the `REVAI_ACCESS_TOKEN` is set in your `.env` file, and then run:

```bash
sapat my_video.mp4 --provider rev --language es --quality H
```

The tool will detect the API credentials and use the specified service for [transcription](/definitions/transcription.md). In both cases, the [transcription](/definitions/transcription.md) process will generate a `.txt` file with the same name as the input video file.

### Command Parameters

The tool provides several options that allow you to customize the [transcription](/definitions/transcription.md) process:

- **`--provider`**: Specify the API provider to use for [transcription](/definitions/transcription.md). Options are `azure` for Azure OpenAI Whisper API and `rev` for Rev AI API. If not specified, the tool will default to Azure OpenAI if its credentials are detected.

- **`--language`**: Specify the language of the audio. The default is English (`"en"`), but you can set it to other languages supported by the selected API.

- **`--prompt`**: If you want to guide the [transcription](/definitions/transcription.md) with a specific context or topic, you can provide a prompt. This can help improve the accuracy of the [transcription](/definitions/transcription.md) in certain scenarios. This option is particularly relevant for Azure OpenAI's Whisper API.

- **`--temperature`**: The temperature setting controls the creativity of the AI model's output, available when using Azure OpenAI's Whisper API. It ranges from 0 to 1, with 0 being more deterministic and 1 being more creative or varied. The default value is 0.

- **`--quality`**: You can specify the quality of the MP3 audio used for [transcription](/definitions/transcription.md). The options are `'L'` for low, `'M'` for medium, and `'H'` for high. The default setting is medium quality.

**Note**: When processing a directory, the tool will automatically transcribe all `.mp4` files in that directory.

### Example Commands

Here are some example commands that illustrate how to use the tool with both Azure OpenAI's Whisper API and Rev AI API.

#### Azure OpenAI

```bash
sapat videos/ --quality H --language fr --prompt "Transcribe the following lecture accurately" --temperature 0.2
```

This command processes every `.mp4` file in the `videos` directory, producing a separate `.txt` file for each video with [transcription](/definitions/transcription.md)s in French.

#### Rev AI

```bash
sapat my_video.mp4 --provider rev --quality M --language en
```

This command transcribes the `my_video.mp4` file using Rev AI API, with medium-quality audio settings and English as the language.

## Verification and Cleanup

After the [transcription](/definitions/transcription.md) process is complete, it’s important to confirm that everything has been executed correctly. Here’s how you can verify the results:

### Verify the Output

#### Check the Text Files

After running the tool, locate the `.txt` files generated by the [transcription](/definitions/transcription.md). These files should be in the same directory as the input video files, with names matching the original video files.

#### Review the Transcription

Open the `.txt` files and review the [transcription](/definitions/transcription.md)s. Check for accuracy, paying attention to whether the language, context, and content have been correctly captured.

### Confirm Cleanup of Temporary Files

The tool is designed to automatically delete temporary MP3 files after [transcription](/definitions/transcription.md). Verify that there are no leftover `.mp3` files in the directories you processed.

If everything appears correct and the [transcription](/definitions/transcription.md) quality meets your expectations, the process has been successfully completed.

## Common Issues and Troubleshooting

Even with the best tools and setup, issues can arise. Below are some common problems you might encounter and their solutions:

### Incorrect or Garbled Transcription

**Problem:** The [transcription](/definitions/transcription.md) output is incorrect, garbled, or incomplete.

**Solution:** There could be several reasons for this issue:
- Ensure that the audio quality of the video file is clear and free of background noise. Poor audio quality can lead to inaccurate [transcription](/definitions/transcription.md)s.
- Check the language setting (`--language` option). Make sure it matches the language spoken in the video.
- If using Azure OpenAI's Whisper API, try adjusting the temperature setting (`--temperature`). A lower temperature (closer to 0) might produce more consistent results.

### ffmpeg Not Recognized

**Problem:** The terminal or command prompt returns an error stating that `ffmpeg` is not recognized as a command.

**Solution:** This issue typically occurs when ffmpeg is not correctly installed or not added to the system PATH.
- Verify that ffmpeg is installed by running `ffmpeg -version`.
- If it is installed, ensure that the directory containing `ffmpeg` is included in your system PATH. Refer to the earlier section on adding ffmpeg to your PATH for detailed instructions.

### API Errors or Quota Exceeded

**Problem:** You receive errors related to the API you are using, such as quota exceeded or authentication failure.

**Solution:** 
- Double-check your API key or access token in the `.env` file to ensure they are correct.
- Log in to your Azure or Rev AI account and verify that you have sufficient credits or that your subscription plan allows for the API usage. You might need to request an increase in your API usage limits if you are hitting the quota frequently.

### Python Package Conflicts

**Problem:** Installation of the package fails due to conflicts with other installed Python packages.

**Solution:** 
- Try creating a [virtual environment](/definitions/virtual environment.md) to isolate the tool’s dependencies from the rest of your system. You can create a [virtual environment](/definitions/virtual environment.md) with the following commands:

```bash
python -m venv myenv
source myenv/bin/activate  # On Windows use: myenv\Scripts\activate
```

Then install the tool within this [virtual environment](/definitions/virtual environment.md).

## Conclusion

In this guide, you've learned how to set up and use the `nkkko/sapat` [repository](/definitions/repository.md) to transcribe video and audio files using either Azure OpenAI's Whisper API or the Rev AI API. The process involves converting video files into MP3 format, using advanced AI to transcribe the audio, and saving the [transcription](/definitions/transcription.md) in a text file. With options to process individual files or entire directories, this tool is versatile and powerful, suitable for a wide range of [transcription](/definitions/transcription.md) needs.

By following the steps outlined in this guide, you’ve installed the necessary software, configured API access, and successfully transcribed video files. Additionally, you’ve learned how to troubleshoot common issues, ensuring that you can rely on this tool for accurate and efficient [transcription](/definitions/transcription.md)s in the future.

### Next Steps

Now that you have mastered the basics of this tool, consider exploring further possibilities:
- **Integration**: Integrate this tool into a larger workflow for automating content creation, such as automatically adding captions to videos.
- **Customization**: Modify the tool’s source code to support additional file formats or languages.
- **Advanced Usage**: Experiment with different temperature settings, prompts, and languages to optimize [transcription](/definitions/transcription.md)s for specific content types.

## References

For more information and additional resources, consider the following links:
- [Python Installation Guide](https://www.python.org/downloads/)
- [ffmpeg Documentation](https://ffmpeg.org/documentation.html)
- [Azure OpenAI Whisper API](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/whisper)
- [Rev AI API Documentation](https://www.rev.ai/docs)

These references provide additional details and context for the tools and APIs used in this guide. Exploring them will deepen your understanding and help you make the most of the [transcription](/definitions/transcription.md) tool.
