# Explaining Strategies for Expected Impacts — Code Repository

This repository contains the implementation, experimental benchmarks, and validation scripts for the paper  
**“Explaining Strategies for Expected Impacts”**, submitted at **AAMAS 2026**.  

It is organized into a **tool** component (core method / user interface) and a **validation** component (for experiments, CPI generation, and integration with PRISM).  

> ⚠️ **Important:** All components — except possibly the result notebook in `validation/results/` and `validation/CPI_generation` — are **strongly recommended to be run in Docker**.  
> The **`tool/`** and **`cpi-to-prism/`** folders, in particular, should **always** be executed within Docker to ensure dependency consistency and reproducibility.


>⚠️ **NB!** Each folder has a **README** file that helps moving within the single folders. 

---

## Table of Contents

1. [Overview](#overview)  
2. [Repository Structure](#repository-structure)  
3. [Docker Setup (Strongly Recommended)](#docker-setup-strongly-recommended)  
4. [Usage](#usage)  
   - [Running the Tool / Benchmark](#running-the-tool--benchmark)  
   - [Validation / CPI generation / cpi-to-prism](#validation--cpi-generation--cpi-to-prism)  
5. [Configuration & Dependencies](#configuration--dependencies)  
6. [Results & Output](#results--output)  
7. [Development & Testing](#development--testing)  
8. [Caveats & Notes](#caveats--notes)  

---

## Overview

This repository implements the methods, algorithms, and experiments described in the AAMAS 2026 paper:

> **Explaining Strategies for Expected Impacts**  
> *A framework for strategy synthesis and explainability for business processes with probabilistic uncertainty and multiple impact constraints.*

The project builds on the BPMN+CPI formalism and integrates:
- A **strategy synthesis algorithm** with on-the-fly exploration and impact-based pruning;
- An **explainer module** producing minimal decision trees at each decision point;
- A **validation suite** comparing our method with PRISM.

---

## Repository Structure
```
/
├── tool/ # Core implementation and interface
│ ├── Dockerfile # Docker environment for the tool
│ ├── requirements.txt
│ ├── run_benchmark.sh
│ ├── gui/ # GUI components
│ ├── src/ # Core algorithm and explainability modules
│ ├── tests/ # Unit/integration tests
│ └── examples/ # Example notebooks or usage scripts
│
├── validation/ # Validation and experiments
│ ├── CPI_generation/ # CPI process generators
│ ├── cpi-to-prism/ # CPI→PRISM conversion and benchmarking
│ ├── results/ # Databases and result notebooks
│ └── run_benchmark.sh
│
└── README.md # This file
```

### Key Folders
- **`tool/`** — main algorithmic tool, explainer, and benchmark interface.  
- **`validation/CPI_generation/`** — generation of synthetic CPI processes.  
- **`validation/cpi-to-prism/`** — conversion utilities and benchmarking using PRISM.  
- **`validation/results/`** — result databases and notebooks (may be run outside Docker).

---

## Docker Setup (Strongly Recommended)

To ensure consistent environments across machines, Docker is strongly recommended (if not essential). The only part you might optionally run outside Docker is the final analysis notebook in validation/results/, though even then using containerization is safer.

### Why Docker?

The tool and cpi-to-prism pipelines have multiple dependencies (Python versions, libraries, PRISM binaries).

Docker isolates environment conflicts and ensures reproducibility.

It simplifies deployment and sharing of results.

### How to use Docker in this repo

tool Docker container

The tool/ folder contains a Dockerfile. You can build and run it to execute benchmarks, experiments, or launch the GUI.

Example usage (from the repo root):
```
cd tool
docker build -t aamas-tool .
docker run --rm -v "$(pwd):/workspace" aamas-tool bash -c "./run_benchmark.sh"
```

You can mount host directories (e.g. for output) as volumes.

For GUI mode, you may need to expose ports or use X11 forwarding or web UI configuration.

cpi-to-prism / validation Docker (optional / suggested)

Consider encapsulating the validation/cpi-to-prism/ pipeline in a Docker container too, so that PRISM binaries, Python scripts, and models run in a controlled environment.

If no Dockerfile is provided, you could write one mirroring the tool setup: install dependencies from requirements.txt, include PRISM binaries, set working directory, and enable the run_benchmark.sh script.

Mount volumes / share data

Use Docker -v flags to mount your local working copy into the container so that generated files, CPI bundles, logs, databased etc. persist.

For example:
```
docker run --rm -v "$(pwd)/validation:/workspace/validation" aamas-tool bash -c "cd validation/cpi-to-prism && ./run_benchmark.sh"
```

Optional non‐Docker execution

In principle, you can run most scripts natively (e.g. on your system), provided you replicate the Python environment, install PRISM, and satisfy all dependencies.

However, you risk version mismatches, missing dependencies, or system-specific issues.

The only part that is less necessary to dockerize is the final notebook in validation/results (i.e. the post-hoc analysis) and the BPMN+CPIs generation. 


## Usage

Below are instructions to reproduce tool runs, benchmarks, and validation steps. Adjust paths / arguments as needed.

### Running the Tool / Benchmark

Build and run the Docker image for the tool.

To start the application using Docker, follow these steps:

1. Start the Docker:
    ```bash
    docker build -t paco .
    docker run -d -p 8000:8000 -p 8050:8050 -p 8888:8888 -it --name PACO paco
    docker logs PACO
    ```

2. Open a browser and navigate to `http://127.0.0.1:8050` to view the app.
3. Open a browser and navigate to `http://127.0.0.1:8000` to access the application via REST API.
   The docs are available at `http://127.0.0.1:8000/docs`
4. Open another browser tab and go to `http://127.0.0.1:8888` to access the Jupyter environment.  
   You will find multiple `.ipynb` notebooks available — **we recommend [starting with `tutorial.ipynb`](../tutorial.ipynb)**, which provides a guided walkthrough of the main functionalities.

> ⚠️ **LLM Integration:**  
> The tool is designed to support integration with a **Large Language Model (LLM)** for strategy explanation and reasoning.  
> In our experiments, we ran the model **locally using [LM Studio](https://lmstudio.ai/)**, so **no external API endpoint** is provided by default.  
>
> If you wish to connect your own LLM instance (e.g., OpenAI, Ollama, or a custom local API), you can easily modify the endpoint in the function  
> `run_llm_on_bpmn()` located in  
> `tool/src/ai/ll_utils.py`.
>
> ### Steps to enable your own LLM
>
> 1. **Comment out** the following lines (used to check LM Studio’s availability):
>    ```python
>    try:
>        response = requests.get("http://localhost:1234/v1/models", timeout=max_attempts)
>        response.raise_for_status()
>    except requests.exceptions.RequestException as e:
>        return {
>            "bpmn": bpmn_dict,
>            "message": "I'm offline"
>        }
>    ```
>
> 2. **Modify the LLM endpoint configuration** as needed in the code below:
>    ```python
>    llm = ChatOpenAI(
>        openai_api_base="http://localhost:1234/v1",
>        openai_api_key="lm-studio",
>        model="deepseek-r1-distill-llama-8b",
>        temperature=0.7,
>        verbose=False
>    )
>    ```
>
> You can replace the `openai_api_base`, `openai_api_key`, or `model` fields with your preferred configuration — for example, connecting to **OpenAI**, **Ollama**, or any other OpenAI-compatible API.  
>
> 💡 *Tip:* If you are running locally with LM Studio, make sure the local API is active on `localhost:1234` before executing the tool.

### Running the experiments

From inside container (or locally, if not using Docker):

```
# make sure tool/ is current working directory
chmod +x run_benchmark.sh
./run_benchmark.sh
```

This will execute a suite of benchmark experiments based on the algorithm in Section 3, generate logs, results files, and possibly intermediate artifacts.

Optionally, run the Jupyter notebooks in `tool/` (e.g. example_fig8.ipynb, tutorial.ipynb) to explore usage examples and visualizations.

### Validation / CPI Generation / PRISM Benchmarking

#### Generate CPI processes
Go to `validation/CPI_generation/` (inside Docker or native environment), install dependencies, and run the notebook / scripts to generate synthetic CPI bundles.
This outputs CPI bundles into `validation/CPI_generation/generated_processes/`.

#### Translate CPI to PRISM / run benchmarks
Navigate to `validation/cpi-to-prism/`. Make sure PRISM is available (e.g. binaries included or installed).
Run:
```
chmod +x run_benchmark.sh
./run_benchmark.sh
```

This will convert CPI bundles into PRISM models, run PRISM on them, and store results (e.g. into SQLite database, logs).

> ⚠️ **CPIs:**  
> The folders `validation/cpi-to-prism/CPIs` and `tool/CPIs` are intended to contain the **same set of CPI files**.  
> Currently, **only** the folder `validation/cpi-to-prism/CPIs` includes all the CPI instances used in the experiments, due to storage constraints.  
>
> To use these CPIs within the tool, simply **copy** the contents of  
> `validation/cpi-to-prism/CPIs` → `tool/CPIs`.
>
>
> This ensures both components (the tool and the validation pipeline) operate on the same CPI set.


### Analyze results
The generated results are stored in `validation/results/` (e.g. benchmarks_our.sqlite, benchmarks_prism.sqlite) along with the analysis notebook (e.g. Validation_Expalining_Strategies_for_Expected_Impacts.ipynb).
You can open that notebook (locally or via Jupyter) to reproduce plots, tables, and comparisons.

## Configuration & Dependencies

Python version: 3.12+ (as indicated in the original README) 


Dependencies: each submodule (tool, cpi-to-prism, CPI_generation) has a requirements.txt with needed Python packages.

PRISM: version 4.8.1 or higher (binaries should be placed into `cpi-to-prism/prism-*` folders). 


Other external tools / libraries (e.g. for GUI, matplotlib, etc.) as per the requirements files.

Ensure file system permissions allow execution of shell scripts (chmod +x).

Ensure Docker is installed and functioning (if using Docker).

## Results & Output

Benchmark output from the tool component: logs, result files, possibly intermediate strategy / model artifacts.

### Validation / Results:

- `validation/results/benchmarks_our.sqlite`

- `validation/results/benchmarks_prism.sqlite`

- Final analysis notebook: `Validation_Expalining_Strategies_for_Expected_Impacts.ipynb`

CPI generation outputs: in `validation/CPI_generation/CPIs/`

Intermediate model / log data in validation/cpi-to-prism/ (e.g. PRISM models, CPIs, database files)

## Development & Testing

Use the tests in tool/tests/ to validate core correctness.

When changing or adding experimental logic, run the benchmark suite and verify that the new outputs are plausible.

For GUI changes, test interface responsiveness and integration with backend modules.

Ensure any new dependencies are added to the appropriate requirements.txt and Dockerfile.

When modifying the cpi-to-prism pipeline, validate that PRISM conversions and benchmarks still run successfully.

## Caveats & Notes

Docker is strongly recommended: Without it, environment mismatch or missing dependencies are likely.

Ensure that PRISM binaries are compatible with your architecture (e.g. Linux, macOS, CPU architecture) when including them or mounting them in Docker.

Execution time for benchmarks or PRISM runs may vary depending on your hardware—ensure you allocate adequate compute and memory resources to the container (e.g. via --cpus, --memory) if needed.

If GPUs or specialized hardware are used (unlikely here, but if for LLM modules inside the tool), adapt Docker settings accordingly (e.g. --gpus).

Always back up generated result databases before re-running experiments, to avoid accidental overwriting.

> ⚠️ Each folder has a README file that helps moving within the single folders. 