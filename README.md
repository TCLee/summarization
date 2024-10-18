# Summarize text using a local LLM

## Overview

In this notebook, we'll go over how to summarize text using a LLM running locally on your own device. LLMs are a great tool for summarizing text, given their proficiency in understanding and generating text.

In this notebook, we'll go over different strategies to summarize text.
If all the documents can fit in the LLM's context window, we can use a simple approach that just _"stuffs"_ all the documents into a single prompt for summarization. However, we'll need different approaches in cases where the amount of text is too large to fit in the LLM's context window.

The code in this notebook is adapted from the [LangChain tutorial: Summarize Text](https://python.langchain.com/docs/tutorials/summarization).


## Project Directory Structure

Directory | Description
:--- | :---
`data` | Contains sample text data that will be used for summarization
`prompts` | Contains prompt templates for use with the LLM
`images` | Contains images used in the notebook
`tokenizer` | Contains the [🤗 Hugging Face tokenizer](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct) to be used with the `Llama 3.2` model.


## Setup

### Git

Clone this repository to your local computer by running:

```zsh
git clone https://github.com/TCLee/summarization.git
```

### Conda

1. You will need conda in order to install the required packages to run the notebook. [Installing conda](https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html).

2. Make sure the current working directory is this cloned project's directory:

   ```zsh
   cd /path/to/summarization
   ```
   
3. Create the environment from the 
   [`environment.yml`](environment.yml) file:

    ```zsh
    conda env create -f environment.yml -p ./env
    ```

    This will create a new environment in a subdirectory of the project directory called `env`, (e.g., `/path/to/summarization/env`)

4. Activate the environment: 

    ```zsh
    conda activate ./env
    ```

### Run LLM locally

This guide will show you how to run [`LLaMA 3.2`](https://ollama.com/library/llama3.2:3b) with `3B` parameters via [`Ollama`](https://ollama.com) locally (e.g., on your laptop).

1. [Download](https://ollama.com/download/mac) and run the `Ollama` desktop app.

2. Open the `Terminal` app and run:

    ```zsh
    ollama pull llama3.2:3b
    ```

    This will fetch the `Llama 3.2` model from a registry onto your computer.

3. You can verify that the `Llama 3.2` model has been downloaded by running:

    ```zsh 
    ollama list
    ```

    Make sure you see `llama3.2:3b` in the list of models.

Check out Ollama's [GitHub repo](https://github.com/ollama/ollama) for more details and [documentation](https://github.com/ollama/ollama/tree/main/docs#documentation).


### Environment variables

This project makes use of 
[python-dotenv](https://github.com/theskumar/python-dotenv)
to load in the environment variables from a `.env` file.

Create a `.env` file in the root directory of this cloned repository
(e.g., `/path/to/summarization/.env`). Fill in the following with your own API keys:

```Dotenv
# Optional. Recommended to see what's going on 
# under the hood of LangGraph and LangChain.
LANGSMITH_API_KEY="your-langsmith-secret-key"
LANGCHAIN_TRACING_V2="true"
LANGCHAIN_PROJECT="Summarization"
```

#### (Optional) LangSmith
Many of the applications you build with LangChain will contain multiple steps with multiple invocations of LLM calls. As these applications get more and more complex, it becomes crucial to be able to inspect what exactly is going on inside your chain or agent. The best way to do this is with [LangSmith](https://smith.langchain.com/).


### Jupyter Notebook

The conda environment includes an installation of [Jupyter Lab](https://jupyter.org/). Start Jupyter Lab from your terminal:

```zsh
jupyter lab
```

In Jupyter Lab, open the notebook 
[`summarization.ipynb`](summarization.ipynb) 
and follow the instructions there.