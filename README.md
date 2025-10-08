# Explaining Strategies for Expected Impacts

Welcome to the repository that manages the tool and the validation results for the submitted paper *Explaining Strategies for Expected Impacts* to AAMAS 2026.

PRISM is already made available because PRISM is free and open source software, distributed under the GNU General Public License (GPL), version 2.


## Prerequisites

- **Python 3.12+**
- **Prism**

    To install **Python**, follow the instructions on [Python's official website](https://www.python.org/downloads/). 

    To install **Prism**, follow the instructions on [PRISM model checker](https://www.prismmodelchecker.org/download.php) (version 4.8.1 or higher)
---



## Running Benchmark

Ensure all dependencies are installed and your environment is correctly configured before running benchmarks.

### Preparing CPI Bundle

Place your CPI bundle into the `CPIs` folder. If you don't have a CPI bundle, you can create one by following the instructions in the repository [synthetic-cpi-generation](https://github.com/danielamadori/synthetic-cpi-generation), or you can download the pre-built bundle used in the paper for validation [here](https://univr-my.sharepoint.com/:f:/g/personal/emanuele_chini_univr_it/EuMjJi6L03lCp0e348YPAYwBMJ5jTGO1lojwuIlOAhpaaA?e=u9oXl1).

### Running the Script

Execute the benchmark script according to your operating system:

**Run the script**
    ```bash
    chmod +x run_benchmark.sh
    ./run_benchmark.sh
    ```

After execution, benchmark results and logs will be generated in the main directory:


#
---

## Repository Structure

Below is an overview of the main folders and files in this repository:

```
aamas2025/
├── README.md                # Project overview and instructions
├── tool/                    # (Tool scripts and utilities, if present)
├── validation/              # Validation experiments and results
│   ├── CPI_generation/      # CPI generation scripts and generated processes
│   │   ├── main.ipynb       # CPI generation notebook
│   │   ├── README.md        # CPI generation instructions
│   │   ├── requirements.txt # Python dependencies for CPI generation
│   │   └── generated_processes/ # Generated CPI process files
│   ├── cpi-to-prism/        # Benchmarking and PRISM integration
│   │   ├── benchmarks.sqlite    # Benchmark results database
│   │   ├── run_benchmark.sh     # Benchmark execution script
│   │   ├── main.ipynb           # Benchmark analysis notebook
│   │   ├── requirements.txt     # Python dependencies for benchmarking
│   │   ├── CPIs/                # CPI bundles for experiments
│   │   ├── models/              # Model files for PRISM
│   │   ├── prism-4.8.1-linux64-x86/ # PRISM binaries (Linux)
│   │   ├── prism-4.8.1-mac64-arm/   # PRISM binaries (Mac)
│   │   └── sources/             # Source files and scripts
│   └── results/              # Results and analysis
│       ├── benchmarks_our.sqlite      # Our framework results database
│       ├── benchmarks_prism.sqlite    # PRISM results database
│       └── Validation_Expalining_Strategies_for_Expected_Impacts.ipynb # Analysis notebook
└── .gitignore               # Git ignore file
```

**Key folders:**
- `validation/CPI_generation/`: Scripts and notebooks for generating synthetic CPI processes.
- `validation/cpi-to-prism/`: Scripts, models, and data for benchmarking with PRISM.
- `validation/results/`: Databases and notebook for storing and analyzing experiment results.

Refer to the README files in each subfolder for more detailed instructions and context.
