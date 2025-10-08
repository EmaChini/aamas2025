# Synthetic CPI generation
![Python Version](https://img.shields.io/badge/python-3.12%2B-blue)
![GitHub issues](https://img.shields.io/github/issues/danielamadori/synthetic-cpi-generation)
![GitHub pull requests](https://img.shields.io/github/issues-pr/danielamadori/synthetic-cpi-generation)
![GitHub contributors](https://img.shields.io/github/contributors/danielamadori/synthetic-cpi-generation)


## Description
This repository contains code and resources for generating synthetic data.

More details at [main.ipynb](https://nbviewer.org/github/danielamadori/synthetic-cpi-generation/blob/main/main.ipynb)

### Note
The repository is self contained as source processes from the `generated_processes` folder are included, however these can be generated with custom preferences as explained in the GitHub repository: [PietroSala/process-impact-benchmarks](https://nbviewer.org/github/PietroSala/process-impact-benchmarks/blob/main/main.ipynb)

## Prerequisites

- **Python 3.12+**

To install **Python**, follow the instructions on [Python's official website](https://www.python.org/downloads/).

---

## Quick Start

### Using Python
To start the application using Python, follow these steps:
1. **Environment Setup**
- **Using Conda**
    ```bash
    conda create --name cpi python=3.12
    conda activate cpi
    ```
- **Using venv**
    ```bash
    python3.12 -m venv cpi_env
    source cpi_env/bin/activate  # On macOS/Linux
    cpi_env\Scripts\activate     # On Windows
    ```

2. **Install required dependencies**
    ```bash
    pip install -r requirements.txt
    ```
   
3. **Running the `main.ipynb` Notebook**
   To start the `main.ipynb` notebook directly, use the following command:
    ```bash
    jupyter notebook main.ipynb --port=8888
    ```
    Open a browser and go to `http://127.0.0.1:8888` to access the Jupyter environment and run the `main.ipynb` notebook.

---

## Output
The generated bundle will be saved in the `CPIs` folder.
