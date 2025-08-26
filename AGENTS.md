---

## 🚀 Project Overview

This document serves as the single source of truth for Claude Code when interacting with this codebase. The goal is to develop a robust, enterprise-grade data validation application using the `pandas` library, designed to address common data governance tasks. The application will feature a command-line interface (CLI) driven by explicit `/commands` and maintain session state for comprehensive reporting [4].

### Core Functionality
The app will address real-world data reconciliation challenges [5]. It will validate data types, value ranges, regex patterns, perform cross-column validation, check referential integrity, and handle inconsistent data entries and missing values [6].

### Input & Output Specifications
*   **Input**: Multiple Excel (.xlsx) and CSV (.csv) files containing deliberate "bad data" (e.g., missing values, inconsistent naming, incorrect data types, duplicate rows, trailing spaces, case sensitivity issues) [7].
*   **Output**: A new Excel spreadsheet with multiple tabs (Summary, Data_Lineage, validation tasks) using color-coding (red for errors, yellow for warnings, green for passed) [7]. Output should support alternative formats like CSV and HTML [7]. A `Data_Lineage` tab should track source files for each data point [8].
*   **Session Management**: Results from each command are stored in a `.session/` directory as JSON files for persistence, enabling comprehensive reporting across commands [7, 9].

### Technology Stack
*   **Primary Language**: Python
*   **Core Library**: `pandas`
*   **Dependencies**: `openpyxl`, `tqdm`, `colorama`, `pytest`, `memory-profiler`, `argparse`, `json`, `logging`, `os`, `pathlib` [10, 11].
*   **System Requirements**: Python 3.8+, 4GB RAM (8GB recommended), 500MB+ disk space [11].

---

## 💻 Coding Standards and Best Practices

**You MUST adhere to the following coding standards to ensure high-quality, maintainable code.**

### General Principles
*   **Readability**: Prioritize clear and understandable code.
*   **Performance**: Consider execution time and memory usage for operations, especially with large datasets [12, 13].
*   **Error Handling**: Implement robust error handling mechanisms, providing clear feedback messages for users [12, 13]. Examples: `"[FILE NOT FOUND] Cannot read 'sales.xlsx'. Suggestion: Check the file path and ensure the file exists."` [13].
*   **Documentation**: All functions, classes, and complex logic blocks must include clear docstrings (Google style recommended) and comments [12, 14].
*   **Design Patterns**: Follow best practices like SOLID and DRY principles [15].
*   **Type Hints**: Use Python type hints for improved code clarity and maintainability [15].
*   **Modularity**: Design focused components with single, clear responsibilities to improve performance and predictability [16].

### Specific Guidelines
*   **File Naming**: Use `snake_case` for Python file names.
*   **Variable/Function Naming**: Use descriptive names that clearly indicate their purpose.
*   **Code Formatting**: Use a consistent formatter (e.g., Black) to ensure uniform code style [14].
*   **Imports**: Destructure imports when possible (e.g., `from library import foo`) [17].
*   **Avoid Irreversible Actions**: Do not take irreversible actions that might harm the user or their environment without explicit user approval [18].
*   **Context Preservation**: When creating code, ensure new implementations don't conflict with existing patterns or inadvertently overwrite critical sections [19].

---

## ✅ Testing Strategy

**All new features and bug fixes MUST be accompanied by comprehensive test coverage.**

### General Principles
*   **Test-Driven Development (TDD)**: Whenever possible, write tests based on expected input/output pairs *before* implementing the code. Ensure tests fail initially and then pass once the code is written [20].
*   **Unit Tests**: Use `pytest` for unit testing. New features require corresponding unit tests [11, 14].
*   **Edge Cases**: Include test cases for valid inputs, invalid inputs, and edge cases (e.g., empty files, huge files, malformed data) [13].
*   **Test Execution**: To run tests, use `pytest -v` [14].
*   **Verification**: After implementing a solution, ensure it passes all relevant tests. Do not overfit to tests [21].
*   **Blind Validation**: For critical tasks, a separate agent or mechanism should be used for blind validation to verify that the main agent's work is reliably done and the tests pass [22, 23].

### Performance Testing
*   **Profiling**: Conduct memory profiling for optimization and monitor execution time for individual commands [12, 13].
*   **Large Files**: Implement chunk processing for files larger than 100MB [13].
*   **Progress Bars**: Use `tqdm` for long-running operations to provide user feedback [11, 13].

---

## 🔄 Workflow and Git Practices

**Follow these guidelines for effective collaboration and version control.**

### Git Workflow
*   **Branching**: Use a clear branching strategy (e.g., `feature/branch-name`, `bugfix/branch-name`).
*   **Commit Messages**: Write descriptive commit messages that clearly explain the changes made [24, 25]. Claude should automatically compose messages based on diff and context [25].
*   **Pull Requests**: Claude can assist in creating and reviewing pull requests [26, 27]. Ensure PRs include sufficient context and testing details [27].
*   **Sensitive Files**: Always ensure sensitive files (e.g., `.env`, `package-lock.json`, `.git/`) are correctly excluded from version control using `.gitignore` [28].

### Command-Line Interface (CLI)
*   The application is command-line interface driven by explicit `/commands` [4].
*   **Session Reset**: Use `/clear` frequently between tasks to reset the context window and maintain focus [29].
*   **Debugging**: When debugging, you may be asked to capture error messages and stack traces, identify reproduction steps, isolate failures, implement minimal fixes, and verify solutions [30].
*   **Help**: The `/help` command shows all available commands with examples [31].

### Common Commands to Document and Use:
*   `/compare --files <list of files> --primary-key <column name>`: Finds missing records between files [32].
*   `/merge --files <list of files> --column-map <JSON mapping> --strategy <how to combine data>`: Combines multiple files into one, standardizing column names [32, 33].
*   `/validate --file <file to validate> --rules <JSON string defining rules>`: Checks data quality against specified rules [33].
*   `/report --output-file <name for the report file> --format <output format>`: Generates a comprehensive report of all issues found [34].
*   `/preview --file <file to preview> --rows <number of rows>`: Shows the first few rows of a file [31, 34].
*   `/status`: Displays all issues found so far in the current session [31].
*   `/clear`: Resets all findings and starts a new validation session [31].
*   `/help` or `/help --command validate`: Gets command assistance [31].

---

## 🛠️ Developer Environment

**Ensure your development environment is set up consistently.**

### Tools
*   **Git**: Installed and configured locally [35].
*   **Google Cloud CLI**: Installed and logged in (for Jules integration) [35].
*   **GitHub CLI (`gh`)**: Installed to allow Claude to interact with GitHub [36].
*   **Python Virtual Environments**: Always create and activate a virtual environment within the repository [37, 38].
*   **Package Manager**: Use `pip` for Python package management [38].
*   **Verification Script**: Use `verify_environment.py` (if available) to automatically check for all required installations [11].

### Data Generation
*   Create a `create_test_data.py` file to generate test data with deliberate data quality issues [10, 37].

---

## ⚠️ Specific Project Notes and Warnings

*   **Model Chattyness**: Claude models can be chatty. Specify the desired output format explicitly, perhaps by using an assistant message to ensure consistent responses [39].
*   **Hallucination Prevention**: Allow Claude to state "I don't know" to prevent it from generating inaccurate information [39].
*   **Clarity and Specificity**: Be direct, concise, and specific in your instructions, especially for complex tasks. The more detailed the instructions, the better the results [40, 41].
*   **Iterative Refinement**: Start with simple prompts and gradually refine them based on the output. Adjust prompt length, wording, or structure if initial results are not satisfactory [42].
*   **External Data**: When dealing with external data, prioritize using tools like `perplexity` for deep research to get the latest documentation, as LLM knowledge cutoffs can lead to outdated information .

---

## 🎯 Task-Specific Guidance

### For Designers (if applicable to this project)
*   **Detailed Explanations**: When assisting designers with limited coding experience, provide detailed explanations and suggest smaller, incremental changes [43].
*   **Image Analysis**: Leverage image pasting for prototyping; Claude excels at reading designs and generating functional code [43, 44].

### For Data Scientists (if applicable to this project)
*   **Codebase Comprehension**: Utilize Claude for codebase exploration, understanding data pipeline dependencies, and identifying relevant files [45, 46].
*   **ML Concept Explanation**: Ask Claude to explain model-specific functions and settings to bridge knowledge gaps [47].

---