---
title: Setup
---

This lesson uses Python and a large-language model (LLM) chat to provide
guidance and recommended practices on using generative artificial
intelligence to help write code.

This lesson uses Jupyter notebooks, an interactive development
environment widely used for doing data science with Python. **The rest
of this page provides instructions for setting up the software and data
needed to complete this lesson. Please complete setup prior to your
scheduled lesson.**

## Setup

This lesson uses two pieces of software: Visual Studio Code and
Miniforge.

### Installing Visual Studio Code

Visual Studio Code, also known as VS Code, is a customizable code editor
developed by Microsoft for Windows, macOS, and Linux.

1.  Download the appropriate [VS Code
    installer](https://code.visualstudio.com/download) for your system.
    Most people should click the big blue button for their operating
    system.
2.  Run the installer

### Installing Miniforge

Miniforge is a package manager used to manage software related to
Python. To install:

1.  Download the appropriate [Miniforge
    installer](https://conda-forge.org/download/) for your system
2.  Run the installer

::: callout ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

#### Anaconda

You may already be familiar with Anaconda, which includes similar
package management software as Miniforge and a whole lot more. We
**strongly recommend** sticking to the installation instructions and
software presented here for this lesson. The Anaconda distribution
includes additional programs that may affect the output of some of the
code presented in this lesson, which can be confusing for people new to
Python.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

### Setting up the Python environment

Once Miniforge is installed, you're ready to set up the Python
environment. You'll need to use a command-line interface, or CLI, to do
so. A CLI is an application that runs commands that are provided as
text. Examples of command-line interfaces include the Windows command
prompt and Unix shells, including bash. We'll be using the CLI to
install and run JupyterLab.

Each operating system has one or more command-line interfaces available.
We recommend using the following applications for this lesson:

- **Windows:** Use the Miniforge Prompt, which was installed as part of
  Miniforge. You can find it by searching for Miniforge Prompt in the
  search box on the Windows toolbar.
- **macOS:** Use the Terminal. You can find it in the
  Applications/Utilities folder or by searching for Terminal using
  Spotlight.

Type or copy the following command into the CLI to set up the
environment:

    mamba create --name python-ai-lesson ipykernel geopandas jupyterlab pyogrio

### Creating the lesson folder

Create a folder called **python-ai-lesson** on your desktop to store
lesson materials.

### Using VS Code

Find and open VS Code using the search interface in your operating
system. Once VS Code is open:

1.  Click File \> Open Folder
2.  Select the **python-ai-lesson** folder created above

The contents of the folder should now appear in the left sidebar of the
VS Code window.

Your instructor will explain how to work with Python in VS Code as part
of the lesson.
