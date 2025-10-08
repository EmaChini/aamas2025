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

Run the benchmarks for our tool in the tool folder while for prism please enter in the validation folder
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
├── tool/                    # Main tool scripts, GUI, and documentation
│   ├── .gitignore
│   ├── Dockerfile
│   ├── example_fig8.ipynb
│   ├── example_from_bundle.ipynb
│   ├── example_refinements.ipynb
│   ├── example_strategy_decision_based.ipynb
│   ├── image.png
│   ├── LICENSE.txt
│   ├── README.md
│   ├── requirements.txt
│   ├── run_benchmark.bat
│   ├── run_benchmark.sh
│   ├── tutorial.ipynb
│   ├── CPIs/
│   │   └── cpi_bundle_x1_y1.cpis.gz
│   ├── docs/
│   │   ├── index.md
│   │   ├── installation_and_usage.md
│   │   ├── style.css
│   │   ├── _includes/
│   │   │   └── navbar.html
│   │   └── _layouts/
│   │       └── default.html
│   ├── gui/
│   │   ├── Dockerfile
│   │   ├── requirements.txt
│   │   └── src/
│   │       ├── env.py
│   │       ├── main.py
│   │       ├── assets/
│   │       ├── controller/
│   │       ├── model/
│   │       └── view/
│   ├── src/
│   │   ├── __init__.py
│   │   ├── __main__.py
│   │   ├── run_benchmark.py
│   │   ├── server.py
│   │   ├── ai/
│   │   │   ├── llm_utils.py
│   │   │   ├── model.py
│   │   │   └── prompt.py
│   │   ├── api/
│   │   │   ├── llm.py
│   │   │   └── paco.py
│   │   ├── experiments/
│   │   │   ├── benchmark.py
│   │   │   ├── experiment.py
│   │   │   ├── watchdog.py
│   │   │   ├── etl/
│   │   │   └── telegram/
│   │   ├── paco/
│   │   │   ├── solver.py
│   │   │   ├── test_from_file.py
│   │   │   ├── test_solver.py
│   │   │   ├── test.json
│   │   │   ├── test.py
│   │   │   ├── evaluations/
│   │   │   ├── execution_tree/
│   │   │   ├── explainer/
│   │   │   ├── optimizer/
│   │   │   ├── parser/
│   │   │   ├── saturate_execution/
│   │   │   └── searcher/
│   │   ├── utils/
│   │   │   ├── check_syntax.py
│   │   │   ├── env.py
│   │   │   └── logger.py
│   │   └── tests/
│   │       ├── saturate_execution/
│   │       │   └── test_saturate_execution.py
│   │       └── searcher/
│   │           └── test_found_strategy.py
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
- `tool/gui/`: Source code and assets for the graphical user interface (GUI).
- `tool/src/`: Main source code for the tool, including core modules, APIs, experiments, and utilities.
- `tool/tests/`: Test scripts for validating tool functionality.
- `validation/CPI_generation/`: Scripts and notebooks for generating synthetic CPI processes.
- `validation/cpi-to-prism/`: Scripts, models, and data for benchmarking with PRISM.
- `validation/results/`: Databases and notebook for storing and analyzing experiment results.

Refer to the README files in each subfolder for more detailed instructions and context.
