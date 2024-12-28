---
title: "How to Use and Run Jupyter Notebook in Daytona."
description: "A brief description of what the guide covers. The description should be a maximum of 160 characters."
date: 2024-12-26
author: "Jeffrey Whewhetu"
tags: ["jupyter notebook", "data analysis", "python"]
---

# How to Use and Run Jupyter Notebook in Daytona

## Introduction

Jupyter Notebook is a very powerful and useful tool every data scientists, AI engineers, AI researchers and other professionals use in their work and personal projects. Knowledge about and how to use it's very necessary.

With the power of Daytona Dev Environment and Jupyter Notebook, our work can be as smooth and streamlined as possible.
In this comprehensive guide, we're going to deep dive into everything you need to get started with using Jupyter Notebook in a Daytona playground, hands-on experience with a real world practical project and much more.

### TL;DR

- What you need to follow along with the guide.
- What's Jupyter Notebook and Everything to Know to get Started
- Setting Up Daytona Playground for Jupyter Notebook
- Demo: Exploring the Jupyter Notebook UI
- Building a Jupyter Notebook Project in the Daytona Playground
- Common Issues and Troubleshooting
- Conclusion

## Prerequisites

## What's Jupyter Notebook and Everything to Know to Get Started

### Introduction

Jupyter Notebook is a powerful opensource interactive web-based application for interactive computing. It offers a simple, streamlined, document centric experience. It supports a wide range of programming languages such as Python, R and Julia.

### Features

### Usage

## Why use Daytona

## Setting Up Jupyter Notebook in Daytona

Alright, that's enough reading, now let us start writing codes. To do so you will need to set up a DuckDB [environment](20240819_definition_development%20environment.md) in a [Daytona workspace](20240819_definition_daytona%20workspace.md). Let’s begin.

### Step 1: Create a GitHub Repository

First head to the GitHub website and create a [repository](20240819_definition_repository.md) with the name of your choice. For my repository name, I’ll use `playground-jupyter-notebook`. The full URL path to the repository is `https://github.com/c0d33ngr/playground-jupyter-notebook`

### Step 2: Clone the repository using Git

After creating the repository, the next step is to clone the repository into your local PC or Mac. To clone the repository, open your terminal and run this command `git clone https://github.com/USERNAME/REPOSITORY-NAME` but replace the placeholders with your GitHub username and repository name you chose in step 1.

In my case, it’s `git clone https://github.com/c0d33ngr/playground-jupyter-notebook`

### Step 3: Prepare your `devcontainer.json` file and dataset in CSV format

Run the command to move into your cloned repository but don’t forget to replace `playground-jupyter-notebook` with the repository name you created if yours isn’t the same as mine.

```bash
cd playground-jupyter-notebook
```

Download the airplane crash dataset you are going to perform some data visualization tasks on which is in CSV format, from the GitHub repo [here](https://github.com/c0d33ngr/playground-jupyter-notebook/blob/main/Airplane_Crashes_and_Fatalities_Since_1908.csv).

Note: It has to be in the directory of your clone repository. In my case, it's inside `playground-jupyter-notebook`.

Now, let us proceed to the next step.

Create a hidden directory named `.devcontainer` where our `devcontainer.json` file will be. Let’s do so and move into it.

Run the command to do so

```bash
mkdir .devcontainer && cd .devcontainer
```

Let’s create our devcontainer.json file in the `.devcontainer` directory.

I use `nano` to create my `.devcontainer.json` file using this command.

```bash
nano devcontainer.json
```

Paste this code into your `devcontainer.json` file.

```yaml
{
    "name": "Jupyter Notebook Playground",
    "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
    "features": {
        "ghcr.io/devcontainers/features/python:1": {}
    },
    "postCreateCommand": "pip install -r requirements.txt && jupyter notebook"
}
```

The `devcontainer.json` content contains configurations to start your Jupyter Notebook environment in a [Daytona workspace](20240819_definition_daytona%20workspace.md).

- `name`: This sets the name of the development container environment to `Jupyter Notebook Playground`.
- `image`: This uses a base Ubuntu image from the Microsoft image repository.
- `features`: This configuration adds Python setups in the Daytona workspace
- `postCreateComand`: This installs the Python packages needed for this guide into the workspace and spin up the notebook server.

After creating and saving the `devcontainer.json` file, move up back to the root directory of your clone [repository](20240819_definition_repository.md). For me, I run the command below.

```bash
cd ..
```

### Step 4: Create `requirements.txt` file

In the root directory, create a `requirements.txt` file to specify the Python libraries you want pre-installed in the Jupyter Notebook environment. Add the following content to the file:

```bash
pandas
numpy
matplotlib
seaborn
plotly
scikit-learn
tensorflow
keras
torch
scipy
statsmodels
dask
pyspark
nltk
spacy
ipython
requests
opencv-python
beautifulsoup4
```

### Step 5: Commit and Push Changes to GitHub

Run these commands to push your changes to GitHub.

```bash
git add .
git commit -m “add devcontainer.json file”
git push
```

Now, you have successfully pushed our updated repository, which contains our configuration file (`devcontainer.json`) for our Jupyter Notebook environment.

### Step 6: Verify Daytona Installation

Run this command to check `daytona` is properly installed on your PC or Mac.

```bash
daytona –-version
```

You should see your version of `daytona` installed.

### Step 7: Create a Daytona Workspace with Jupyter Notebook Environment in it

Let’s start the daytona server by running the command.

```bash
daytona serve
```

You should see logs like my screenshot.

Open a new tab in your terminal, for Linux its `Shift + Ctrl + T`

Run the command below in a new tab of your terminal and follow the prompt instructions. It would ask you for a [workspace](20240819_definition_daytona%20workspace.md) name to use, choose the default.

Replace `USERNAME` and `REPOSITORY-NAME` with your username for GitHub and the repository name you created earlier.

```bash
daytona create https://github.com/USERNAME/REPOSITORY-NAME
```

In my case, it's this.

```bash
daytona create https://github.com/c0d33ngr/playground-jupyter-notebook
```

After you successfully run the above command you should see a screenshot like mine showing your Daytona workspace that contains the Jupyter Notebook environment is running.

You can now run this command to open the Jupyter Notebook [environment](20240819_definition_development%20environment.md) in your default [IDE](20240819_definition_integrated%20development%20environment%20_ide_.md) you choose when installing Daytona (Replace `WORKSPACE-NAME` with the name you used when creating the workspace above, in my case it's `playground-duckdb`).

```bash
daytona code WORKSPACE-NAME
```

That’s it. Daytona will create a Jupyter Notebook environment for you and open it in the default IDE you set.

## Demo: Exploring the Jupyter Notebook UI

## Building a Jupyter Notebook Project in the Daytona Playground

### Step 1: Import Libraries and Load the Dataset

```bash
#importing the libraries and data
import numpy as np 
import pandas as pd 
import seaborn as sns
import matplotlib.pyplot as plt
from datetime import date, timedelta, datetime

Data = pd.read_csv('/workspaces/playground-jupyter-notebook/Airplane_Crashes_and_Fatalities_Since_1908.csv')
```

### Step 2: Explore the Dataset

```bash
np.random.seed(42) 
obs, feat = Data.shape
Data.sample(5)
```

### Step 3: Summarize Dataset Dimensions and Features

```bash
print(str("Dataset consist of " + str(obs) + " observations (crashes) and " + str(feat) + " features. Features are following:"))
print(",\n".join(Data.columns))
```

### Step 4: Calculate Missing Values in the Dataset

```bash
Data.isnull().sum() #calculating missing values in rows
```

### Step 5: Clean and Format Time and Operator Data

```bash
#cleaning up
Data['Time'] = Data['Time'].replace(np.nan, '00:00') 
Data['Time'] = Data['Time'].str.replace('c: ', '')
Data['Time'] = Data['Time'].str.replace('c:', '')
Data['Time'] = Data['Time'].str.replace('c', '')
Data['Time'] = Data['Time'].str.replace('12\'20', '12:20')
Data['Time'] = Data['Time'].str.replace('18.40', '18:40')
Data['Time'] = Data['Time'].str.replace('0943', '09:43')
Data['Time'] = Data['Time'].str.replace('22\'08', '22:08')
Data['Time'] = Data['Time'].str.replace('114:20', '00:00') #is it 11:20 or 14:20 or smth else? 

Data['Time'] = Data['Date'] + ' ' + Data['Time'] #joining two rows
def todate(x):
    return datetime.strptime(x, '%m/%d/%Y %H:%M')
Data['Time'] = Data['Time'].apply(todate) #convert to date type
print('Date ranges from ' + str(Data.Time.min()) + ' to ' + str(Data.Time.max()))

Data.Operator = Data.Operator.str.upper() #just to avoid duplicates like 'British Airlines' and 'BRITISH Airlines'
```

### Step 6: Analyze and Visualize Accident Trends Over the Years

```bash
Temp = Data.groupby(Data.Time.dt.year)[['Date']].count() #Temp is going to be temporary data frame 
Temp = Temp.rename(columns={"Date": "Count"})

plt.figure(figsize=(12,6))
plt.style.use('bmh')
plt.plot(Temp.index, 'Count', data=Temp, color='red', marker = ".", linewidth=1)
plt.xlabel('Year', fontsize=10)
plt.ylabel('Count', fontsize=10)
plt.title('Count of accidents by Year', loc='Center', fontsize=14)
plt.show()
```

### Step 7: Standardize Operator Names and Visualize Top Operators by Accident Count

```bash
Data.Operator = Data.Operator.str.upper()
Data.Operator = Data.Operator.replace('A B AEROTRANSPORT', 'AB AEROTRANSPORT')

Total_by_Op = Data.groupby('Operator')[['Operator']].count()
Total_by_Op = Total_by_Op.rename(columns={"Operator": "Count"})
Total_by_Op = Total_by_Op.sort_values(by='Count', ascending=False).head(15)

plt.figure(figsize=(12,6))
sns.barplot(y=Total_by_Op.index, x="Count", data=Total_by_Op, palette="gist_heat", orient='h', hue=Total_by_Op.index)
plt.xlabel('Count', fontsize=11)
plt.ylabel('Operator', fontsize=11)
plt.title('Total Count by Opeartor', loc='Center', fontsize=14)
plt.show()
```

### Step 8: Analyze and Visualize Fatalities by Operator

```bash
Prop_by_Op = Data.groupby('Operator')[['Fatalities']].sum()
Prop_by_Op = Prop_by_Op.rename(columns={"Operator": "Fatalities"})
Prop_by_Op = Prop_by_Op.sort_values(by='Fatalities', ascending=False)
Prop_by_OpTOP = Prop_by_Op.head(15)

plt.figure(figsize=(12,6))
sns.barplot(y=Prop_by_OpTOP.index, x="Fatalities", data=Prop_by_OpTOP, palette="gist_heat", orient='h', hue=Total_by_Op.index)
plt.xlabel('Fatalities', fontsize=11)
plt.ylabel('Operator', fontsize=11)
plt.title('Total Fatalities by Opeartor', loc='Center', fontsize=14)
plt.show()
```

## Common Issues and Troubleshooting

*[List common problems and their solutions.]*

**Problem:** *[Description of the problem]*

**Solution:** *[Description of the solution]*

## Conclusion

In this guide, we covered how to effectively use Jupyter Notebook, a powerful open-source tool for interactive computing. Jupyter provides a simple, document-centric interface that supports various programming languages, including Python, R, and Julia, making it a versatile tool for data analysis, machine learning, and more. We also walked through setting up Jupyter Notebook in Daytona, demonstrating its ease of setup and practical benefits.

Throughout the example project, we applied Jupyter's features to clean, analyze, and visualize airplane crash data, using Python libraries like Pandas and Matplotlib. The combination of Jupyter's interactive environment and Python’s powerful data processing capabilities allowed us to efficiently uncover key trends and insights.

## References

*[Cite any sources or references used in the guide.]*

*[Add links to related guides or further reading that might interest the reader.]*
