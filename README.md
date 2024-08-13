
# Mini Fuzzer

**Mini Fuzzer** is a mutation-based fuzzing tool aimed at testing command-line applications. It focuses on generating effective test cases by measuring the line coverage of the target program, specifically supporting software written in C/C++.

## Features

- **Automatic Input Generation:** Generates inputs for the target program automatically.
- **Multiple Mutation Strategies:** Applies various mutation techniques to inputs.
- **Coverage-Based Test Case Generation:** Uses line coverage metrics to guide test case creation.
- **Real-Time Progress Display:** Shows the fuzzing progress in real-time.
- **Crash Reporting:** Produces a summary report for any detected crashes.
<img width="1036" alt="スクリーンショット 2024-01-05 23 50 24" src="https://github.com/yk0112/mini_fuzzer/assets/130746469/f9e1b403-0379-43c6-b441-140a0580bdfe">


## Installation

To install Mini Fuzzer, clone the repository:

```bash
$ git clone https://github.com/yk0112/mini_fuzzer.git

## Usage

### Compile Your Program

First, compile your C or C++ program with GCC. Make sure to include the `-fprofile-arcs` and `-ftest-coverage` flags during compilation:

```bash
$ gcc -fprofile-arcs -ftest-coverage example.c -o example
```

## Config file settings
Before start fuzzing, you need to edit config.py for settings.
First, specify the path where the gcov file will be generated in GCOV_DIRECTORY. Basically, the path to the directory where the executable file is located is preferable.

```python
GCOV_DIRECTORY = 'your path'
```
Next, you can configure some behaviors of the fuzzer.

```python
# setting the target program timeout
TIMEOUT = 5

# list of arguments that will not be mutated
SKIP_ARGS = []

# for arithmetic inc or dec in mutation
INCREMENT_VALUE = 30
DECREMENT_VALUE = 30
```
## Preparing the seed file
Sets the seeds in text file. mini fuzzer generates diverse test cases by mutating seeds.
Describe the seeds as a list of string types corresponding to each command line argument of the target program.
```
["-O", "arg1", "arg2", "arg3"]
["-l", "arg4", "arg5"]
...
```
## Start fuzzing
Start fuzzing by running the command below. Info about detected crashes is stored in dump.csv.
```
$ python fuzz.py <Path to the executable file to be tested>　 <path to seed file>
```

# Dependencies
- Python 3.9 or greater
- Linux OS
- gcov (gcov is a code coverage analysis tool provided as part of GCC)
- Colorama (Python library)
