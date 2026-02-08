
# Parallel Prime Number Computation Benchmark

![Language](https://img.shields.io/badge/language-C-blue.svg) ![Language](https://img.shields.io/badge/language-Python-yellow.svg)

This project benchmarks the performance of **parallel prime number computation** using multiple processes in C and visualizes the results using Python and Matplotlib. It demonstrates how execution time varies with the number of child processes for different numeric ranges.

---

## Overview

The project consists of two main components:

### 1. C Program (fastprime.c)
- Computes prime numbers within a specified range using multiple child processes (fork).
- Divides the workload evenly among processes.
- Writes all discovered prime numbers to a shared file (prime.txt).
- Measures and prints the total execution time.
- Handles graceful termination using SIGINT.

### 2. Python Script (benchmark.py)
- Automatically compiles the C program.
- Detects the number of logical CPU cores on the host machine.
- Runs benchmarks across multiple ranges and process counts.
- Plots execution time vs. number of processes.
- Saves the visualization as execution_time_plot.png.

---

## Project Structure

```text
.
├── fastprime.c              # Parallel prime computation (C)
├── benchmark.py             # Benchmarking & plotting (Python)
├── prime.txt                # Output file containing prime numbers
├── execution_time_plot.png  # Generated performance plot
└── README.md
System Requirements
OS: Linux / POSIX-compliant system

Compiler: GCC

Python: Python 3.x

Libraries: Matplotlib

Setup & Dependencies
Modern Linux distributions often restrict system-wide pip installs (PEP 668). Choose one of the following methods to set up the Python environment:

Method 1: Virtual Environment (Recommended)
Isolates dependencies from the system.

Bash

sudo apt install python3-venv python3-full
python3 -m venv venv
source venv/bin/activate
pip install matplotlib
Method 2: System Package
Installs Matplotlib globally.

Bash

sudo apt install python3-matplotlib
Usage
1. Running the Benchmark (Automated)
The Python script handles compilation, testing, and plotting automatically.

Bash

python3 benchmark.py
This will generate:

prime.txt: The text file containing primes found during the last run.

execution_time_plot.png: A graph showing performance scaling.

2. Running the C Program (Manual)
If you wish to run the C program individually:

Compile:

Bash

gcc fastprime.c -o fastprime -lm
Run:

Bash

./fastprime <range_low> <range_high> <num_processes>
Example:

Bash

./fastprime 1000 100000 4
Output:

Plaintext

0.023456
(The output represents execution time in seconds.)

Benchmark Ranges
The benchmark.py script tests the following numeric ranges to demonstrate how parallel execution scales with workload size:

Low Load: 1,000 – 10,000

Medium Load: 50,000 – 100,000

High Load: 100,000 – 500,000

Key Concepts Demonstrated
Process Creation: Using fork() to create child processes.

Workload Partitioning: Splitting a numeric range across available workers.

Synchronization: Using wait() to ensure parent processes wait for children.

Signal Handling: catching SIGINT for graceful exits.

File I/O: Using buffered output to reduce system call overhead.

Benchmarking: Visualizing algorithmic efficiency using Python.

Notes
Scheduling Overhead: Increasing the number of processes beyond the available physical/logical CPU cores may reduce performance due to context switching and scheduling overhead.

I/O Buffering: Each process buffers output before writing to prime.txt to minimize the performance cost of disk access.

Timing: The reported time includes computation and file writing, but excludes the Python plotting overhead.