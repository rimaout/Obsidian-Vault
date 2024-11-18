---
created: 2024-02-25
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: false
updated: 2024-05-27T13:29
---
---
## Index
1. [[]]

---
**Directory Structure:**
```
├── bin
│   └── cli_script
├── setup.py
└── some_module
    ├── __init__.py
    └── some_module.py
```

**Procedure:**
To make a Python script usable as a CLI (Command Line Interface) tool, follow these steps:

1. You need to create a setup script to package and install your Python script as a CLI tool. Create a new file named `setup.py` in the same directory as your Python script.
    
2. In `setup.py`, use the `setuptools` module to define the scripts and packages that should be installed:
    
```python
from setuptools import find_packages, setup

setup(
    name='some_module',
    version='1.0'
    packages=find_packages(),
    scripts=['bin/cli_script']
)
```


3. Replace `your_script` with the name of your Python script (without the `.py` extension), and `bin/your_script` with the path to the script in the `bin` directory of your project.
    
4. To install your CLI tool, run the following command in the terminal:
    

```python
pip install -e .
```

Replace `.` with the path to your project directory if you’re not currently in the directory containing `setup.py`.

5. Once installed, you can run your CLI tool from the terminal by typing its name followed by the required arguments:

```python
your-cli-tool-name input_file.txt -v
```

Replace `input_file.txt` with the path to your input file and add any other required arguments or flags.

By following these steps, you can create a Python script that can be used as a CLI tool. The `argparse` module provides a simple way to define and parse command-line arguments, and the `setuptools` module allows you to package and install your script as a CLI tool. 
