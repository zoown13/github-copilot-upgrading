## Upgrading a Legacy Project with GitHub Copilot

Let's go through the process of taking a legacy (outdated) Python application and bring it up to the latest version of Python with the assitance of GitHub Copilot.

> [!NOTE]
> This repo is intended to give an introduction to various **GitHub Copilot** features, such as **Copilot Chat** and **inline chat**. Hence the step-by-step guides below contain the general description of what needs to be done, and Copilot Chat or inline chat can support you in generating the necessary commands.
>
> Each step (where applicable) also contains a `Cheatsheet` which can be used to validate the Copilot suggestion(s) against the correct command.
>
> 💡 Play around with different prompts and see how it affects the accuracy of the GitHub Copilot suggestions. For example, when using inline chat, you can use an additional prompt to refine the response without having to rewrite the whole prompt.

## Workshop features

In this workshop, you will be working with a legacy Python application that used Python version 2.5. Here are some features:

1. All dependencies are pre-installed for you, but not using the legacy application which uses a dated version of Python.
1. The application uses Sqlite3 and dated Python syntax that you can update
1. The legacy application has documentation that can be used for functional testing
1. Both unit and functional tests are provided as part of the legacy code. 


### 1. Explore the project using agents

Use the `@workspace` agent to explain what is going on with this project.

- Open GitHub Copilot Chat and prefix your prompt with `@workspace`
- Ask questions like how is this project installing dependencies

### 2. Determine the legacy and porting problem

Try to run the tests in the Python application. Use `pytest` which is pre-installed to get an output. What happens? 

- Ask `@workspace what are some problems that this code may have as I port it to modern Python?`
- Try installing the dependencies with a virtual environment

> [!NOTE]
> Why this might not work? Dependencies will probably fail to install as this is legacy Python using `distribute` which is no longer supported. 
> Use Copilot to suggest other ways to install the dependencies


### 3. Copy all of the code over to the ugpraded dir

In order to port the code, you will need to copy all of the code over to the
`upgraded` directory. This is where you will be working on the code.

- Use the functional tests to determine a _slice_ of functionality that you will focus on
- 
> [!NOTE]
> Why this might not provide correct explanations? Because the business logic
> may want to have some of this components which aren't obvious to the LLM


### 4. Install the project 

Create a virtual environment and install the project. Do `python setup.py develop` and try to understand what the error is. 

- Use GitHub Copilot chat to paste the error and get guidance on what is
  going on
- Ensure to add the file as context `#file:setup.py` 
- Fix the errors with the suggestions and complete the installation 


### 5. Run the tests

The project has the `pytest` framework and command-line tool installed and available. Try running the unit tests available and explore the errors.

- Use the output of the errors to ask Copilot for help. Include it in the chat with `#terminalSelection`. Make sure you have selected the output.
- Review the response from Copilot and ask for clarifications if needed
- Do *not* edit the code yet.


> [!NOTE]
> The errors might not immediately make sense or indicate that the Python version is dated. Ensure you ask further questions to get a better understanding of the errors and pick a strategy. You can also hint that an old Python version was used for the project.

### 6.Fix the try/except errors

Use the functional tests to determine a _slice_ of functionality that you will focus on. In this case you will fix the try/except errors.

- Use GitHub Copilot to help you with the actual problem to fix. Mention the old Python version.
- Fix all try/except errors and run the tests continously until these are fixed.

> [!NOTE]
> There are other errors aside from the exception ones. Make sure all try/except are clean and fixed before moving on.


### 7. Fix the ConfigParser problem

The next slice of the problem is dealing with `ConfigParser` not being available. Use GitHub Copilot to provide a strategy to choose for implementing a fix.

- Ask _"This project was built using Python 2.5 and with Python 3.9 I get the following:"_ . Include a paste of the test output
- The fix might be simple. Choose an option to implement and verify immediately.
- Run the tests to ensure that the changes are correct and that the tests pass

[!NOTE]
> All tests should now pass. If they don't, you can use the test output to ask Copilot for help and revise all the previous steps in this workshop


### 8. Port the tests to Pytest

Pytest is the most common and powerful testing framework and testing command-line tool in Python. The legacy code uses `unittest` which is not as powerful and flexible as `pytest`. Port all the tests to `pytest` and run them.

- On any test file, use the `@workspace` agent to ask how to port the tests to `pytest`
- Write a single test, and try using test functions instead of classes when 
  possible
- Once you write a test, use GitHub Copilot to suggest the next test to generate

> [!NOTE]
> Although tests can run with `pytest` because it is flexible enough to run `unittest` tests, it is better to port the tests to `pytest` as it is more powerful and flexible. This will also help you in the future when you need to add new tests or modify existing ones.

### 9. Use modern packaging

The legacy code uses `distribute` which you had to fix earlier. But it is still using `setuptools` which is now deprecated with `setup.py`. Use `pyproject.toml` to
package the project.

- Ask Copilot to help you with the `pyproject.toml` file. Use the `@workspace` agent to ask how to create a `pyproject.toml` file. Ensure you have the `setup.py` file open so that it can be used as context.
- Create a new `pyproject.toml` file and use Copilot suggestions to fill it in.
- Use the `pyproject.toml` file to install the project. You can use `pip install .` to install the project in editable mode.


> [!NOTE]
> Python packaging continues to be a challenging topic. The `pyproject.toml` file is the new standard for packaging Python projects, but it is still not widely adopted. You can use GitHub Copilot to help you with the `pyproject.toml` file, but it may not always be accurate. Make sure to verify the contents of the file and test the installation.

### 10. Automate with GitHub Actions

The legacy project didn't have any automation. Use GitHub Actions to automate testing and validation of the project. The goal is to have a workdlow that will run on every pull request and will run the tests and try to install the project.

- Ask GitHub Copilot with the `@workspace` agent how to create a GitHub Actions workflow.
- Create the necessary files and directory to create a GitHub Actions workflow.
- Push your changes when done to verify GitHub Actions is working.

> [!NOTE]
> Building automation is a key part of modern software development, but it can take a long time to get everything just right.
> Be patient while creating the automation and use GitHub Copilot to help you with errors and issues as you make progress.
