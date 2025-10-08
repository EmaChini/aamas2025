# Synthetic CPI generation
![Python Version](https://img.shields.io/badge/python-3.12%2B-blue)
![GitHub issues](https://img.shields.io/github/issues/danielamadori/synthetic-cpi-generation)
![GitHub pull requests](https://img.shields.io/github/issues-pr/danielamadori/synthetic-cpi-generation)
![GitHub contributors](https://img.shields.io/github/contributors/danielamadori/synthetic-cpi-generation)


## Description
This repository contains code and resources for generating synthetic data as described in the validation section in the paper.
Here running all the main file it will be possible to recreate all the syntetic dataset used in the validation. The  `CPIs` folder will contain all the BPMN+CPIs used in the validation. However, note that the BPMN+CPIs are generated randomly within the complexity class (i.e., it does not change the values ). 

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
