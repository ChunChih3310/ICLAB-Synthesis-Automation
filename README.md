# USAGI: Ultra Synthesis Automation and Gate-Level Integration

![image](https://github.com/user-attachments/assets/06291db2-a284-45c9-a282-fc229804d337)


USAGI is a Python script designed to automate the process of synthesizing and performing gate-level simulations for digital designs across a range of cycle times. It helps designers find the optimal balance between area, performance, and latency by automating the synthesis process for multiple configurations and selecting the best result based on a customizable performance function.

## Features

- Automates synthesis for a range of cycle times.
- Customizable performance function to suit specific design goals.
- Parallel processing to speed up the synthesis process.
- Automatic selection and retention of the best-performing design.
- Perform gate-level simulation on the best result.
- Generates a CSV file with synthesis results for easy analysis.

## Prerequisites

- **Operating System**: Linux-based system
- **Python**: Python 3.x
- **External Tools**:
  - `dcnxt_shell` for synthesis (Design Compiler)
  - `vcs` for gate-level simulation (Synopsys VCS)
  - `08_check` script to check synthesis results
- **Python Libraries**: Standard libraries (`os`, `re`, `csv`, `subprocess`, `time`, `shutil`, `threading`, `concurrent.futures`)

## Usage

1. **Clone the Repository**:

    ```bash
    git clone https://github.com/ChunChih3310/Ultra-Synthesis-Automation-and-Gate-Level-Integration.git
    cd Ultra-Synthesis-Automation-and-Gate-Level-Integration
    ```

2. **Configuration**:

    Open the script `USAGI.py` in a text editor and modify the following variables in the Configuration section:

    ```python
    # ==================================================
    # Configuration
    # ==================================================
    latency = 1  # Latency of the design

    upper_bound = 5.0  # Upper bound of the cycle time range
    lower_bound = 3.0  # Lower bound of the cycle time range
    step = 0.1         # Step size for cycle time increments
    reverse = True     # If True, cycle times will be in descending order

    dummy_dir = os.path.expanduser('~/dummy_dir')  # Temporary directory to store files
    lab_source_dir = os.path.expanduser('~/Midterm_Project_bk/Exercise')  # Path to your lab files
    max_workers = 100  # Number of parallel synthesis processes
    ```

    - `latency`: Latency of the design.
    - `upper_bound`: Upper bound of the cycle time range.
    - `lower_bound`: Lower bound of the cycle time range.
    - `step`: Step size for cycle time increments.
    - `reverse`: If True, cycle times will be in descending order.
    - `dummy_dir`: Temporary directory to store files.
    - `lab_source_dir`: Path to your lab files.
    - `max_workers`: Maximum number of parallel synthesis processes.

3. **Performance Function**:

    The script uses a performance function to evaluate and compare different synthesis results. You can customize this function according to your optimization goals.

    Modify the performance_func function to suit your performance criteria. 
    ```python
    # ==================================================
    # Performance Calculation
    # ==================================================
    def performance_func(area, cycle_time, latency):
        return (area) * (cycle_time ** 2) * (latency ** 2)
    ```

4. **Run the Script**:

    Run the script using the following command:

    ```bash
    python3 USAGI.py
    ```

    The script will perform the following steps:
    1. Copy your lab files to a temporary directory for each cycle time.
    2. Modify the syn.tcl file to set the cycle time for synthesis.
    3. Run synthesis for each cycle time in parallel.
    4. Collect synthesis results, including area and performance metrics. (Only the directory with the best performance will be retained.)
    5. Identify the best-performing design based on the performance function.
    6. Perform gate-level simulation on the best result.
    7. Generate a CSV file with synthesis results.

## License
This project is licensed under the MIT License 

## Contact

- **Author**: Chun-Chih Yu
- **Email**: [chunchih.ee13@nycu.edu.tw](mailto:chunchih.ee13@nycu.edu.tw)
