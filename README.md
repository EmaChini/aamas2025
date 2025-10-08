# Explaining Strategies for Expected Impacts

Welcome to the repository that manages the tool and the validation results for the submitted paper *Explaining Strategies for Expected Impacts* to AAMAS 2026.




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
- Linux
    ```bash
    chmod +x run_benchmark.sh
    ./run_benchmark.sh
    ```

After execution, benchmark results and logs will be generated in the main directory:

- `benchmarks.sqlite` – Benchmark results database
- `benchmarks_output.log` – Detailed benchmark execution log
