# VS Code Guide for Google Cloud Platform Python Samples

This guide helps you work with the Google Cloud Platform Python Samples repository in Visual Studio Code.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Recommended VS Code Extensions](#recommended-vs-code-extensions)
- [Workspace Setup](#workspace-setup)
- [Common Tasks](#common-tasks)
- [Debugging](#debugging)
- [Useful Keyboard Shortcuts](#useful-keyboard-shortcuts)
- [Tips and Tricks](#tips-and-tricks)

## Prerequisites

Before you start, ensure you have:

- **Python 3.6+** installed on your system
- **Visual Studio Code** installed
- **Git** installed
- **Google Cloud SDK** installed (`gcloud` command)

## Recommended VS Code Extensions

Install these extensions for the best development experience:

1. **Python** (ms-python.python) - Essential for Python development
2. **Pylance** (ms-python.vscode-pylance) - Fast, feature-rich language support
3. **Python Debugger** (ms-python.debugpy) - Debugging support
4. **autoDocstring** (njpwerner.autodocstring) - Generate Python docstrings
5. **GitLens** (eamodio.gitlens) - Enhanced Git capabilities
6. **Google Cloud Code** (googlecloudtools.cloudcode) - GCP integration
7. **Markdown All in One** (yzhang.markdown-all-in-one) - Markdown support
8. **YAML** (redhat.vscode-yaml) - YAML file support

### Install Extensions via Command Line

```bash
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-python.debugpy
code --install-extension njpwerner.autodocstring
code --install-extension eamodio.gitlens
code --install-extension googlecloudtools.cloudcode
code --install-extension yzhang.markdown-all-in-one
code --install-extension redhat.vscode-yaml
```

## Workspace Setup

### 1. Clone the Repository

```bash
git clone https://github.com/GoogleCloudPlatform/python-docs-samples.git
cd python-docs-samples
code .
```

### 2. Configure Python Interpreter

1. Open Command Palette: `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac)
2. Type: `Python: Select Interpreter`
3. Choose your Python 3.6+ interpreter

### 3. Create a Virtual Environment

Open the integrated terminal (`Ctrl+` ` or `Cmd+` `) and run:

```bash
# Navigate to your sample directory
cd <sample-directory>

# Create virtual environment
python3 -m venv env

# Activate it
# On Windows:
env\Scripts\activate
# On macOS/Linux:
source env/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 4. Recommended VS Code Settings

Create or update `.vscode/settings.json` in your workspace:

```json
{
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.flake8Enabled": true,
    "python.formatting.provider": "black",
    "python.testing.pytestEnabled": true,
    "python.testing.unittestEnabled": false,
    "python.testing.nosetestsEnabled": false,
    "editor.formatOnSave": true,
    "files.exclude": {
        "**/__pycache__": true,
        "**/*.pyc": true,
        "**/env": true,
        "**/.pytest_cache": true
    },
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true
}
```

## Common Tasks

### Running Samples

1. Navigate to a sample directory (e.g., `logging/cloud-client`)
2. Open the Python file you want to run
3. Press `F5` to debug or `Ctrl+F5` to run without debugging

Or use the terminal:

```bash
python snippets.py
```

### Running Tests

```bash
# Run all tests in current directory
pytest

# Run specific test file
pytest test_file.py

# Run with coverage
pytest --cov

# Run with verbose output
pytest -v
```

### Linting and Formatting

```bash
# Run flake8 linter
flake8 .

# Format code with black
black .

# Check imports with isort
isort .
```

## Debugging

### Basic Debug Configuration

Create `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "debugpy",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "env": {
                "GOOGLE_APPLICATION_CREDENTIALS": "${workspaceFolder}/path/to/credentials.json"
            }
        },
        {
            "name": "Python: pytest",
            "type": "debugpy",
            "request": "launch",
            "module": "pytest",
            "args": [
                "${file}",
                "-v"
            ],
            "console": "integratedTerminal"
        }
    ]
}
```

### Setting Breakpoints

1. Click in the gutter (left of line numbers) to set a breakpoint
2. Press `F5` to start debugging
3. Use debug toolbar to:
   - Continue (`F5`)
   - Step Over (`F10`)
   - Step Into (`F11`)
   - Step Out (`Shift+F11`)

## Useful Keyboard Shortcuts

### Navigation

- `Ctrl+P` / `Cmd+P` - Quick file open
- `Ctrl+Shift+P` / `Cmd+Shift+P` - Command palette
- `Ctrl+Shift+F` / `Cmd+Shift+F` - Search across files
- `Ctrl+G` / `Cmd+G` - Go to line
- `F12` - Go to definition
- `Alt+F12` / `Option+F12` - Peek definition

### Editing

- `Alt+Up/Down` / `Option+Up/Down` - Move line up/down
- `Shift+Alt+Up/Down` / `Shift+Option+Up/Down` - Copy line up/down
- `Ctrl+/` / `Cmd+/` - Toggle line comment
- `Shift+Alt+F` / `Shift+Option+F` - Format document
- `Ctrl+Space` / `Cmd+Space` - Trigger IntelliSense

### Terminal

- `Ctrl+`` / `Cmd+`` - Toggle integrated terminal
- `Ctrl+Shift+`` / `Cmd+Shift+`` - Create new terminal

## Tips and Tricks

### 1. Workspace Recommendations

When working with specific samples, use VS Code workspaces to keep your settings organized. Save your workspace with `File > Save Workspace As...`

### 2. Google Cloud Authentication

Set up default application credentials:

```bash
gcloud auth application-default login
```

Or set the environment variable in your terminal settings:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/credentials.json"
```

### 3. Multi-root Workspaces

If you work with multiple sample directories, use multi-root workspaces:

```json
{
    "folders": [
        {
            "path": "logging/cloud-client"
        },
        {
            "path": "storage/cloud-client"
        }
    ]
}
```

### 4. Code Snippets

Create custom snippets for common patterns. Go to `File > Preferences > User Snippets` and select Python.

### 5. Git Integration

- View changes: `Ctrl+Shift+G` / `Cmd+Shift+G`
- Stage changes: Click `+` icon next to files
- Commit: Type message and press `Ctrl+Enter` / `Cmd+Enter`

### 6. Search and Replace

- Use regular expressions in search: Click the `.*` icon
- Search in specific directories: Click the `...` icon in search panel
- Replace in all files: Use the replace icon in search results

### 7. IntelliSense for Google Cloud Libraries

Install type stubs for better autocomplete:

```bash
pip install types-google-cloud-storage
pip install types-google-cloud-bigquery
# Install other type stubs as needed
```

### 8. Environment Variables

Use a `.env` file for environment variables:

```env
GOOGLE_APPLICATION_CREDENTIALS=/path/to/credentials.json
GOOGLE_CLOUD_PROJECT=your-project-id
```

Install the DotENV extension to support this.

## Additional Resources

- [VS Code Python Documentation](https://code.visualstudio.com/docs/python/python-tutorial)
- [Google Cloud Python Client Libraries](https://cloud.google.com/python/docs/reference)
- [Repository README](README.md)
- [Contributing Guide](CONTRIBUTING.md)

## Troubleshooting

### Python Interpreter Not Found

If VS Code can't find your Python interpreter:
1. Open Command Palette
2. Type `Python: Select Interpreter`
3. If your interpreter isn't listed, click "Enter interpreter path..."

### Import Errors

If you see import errors:
1. Ensure you've activated your virtual environment
2. Verify dependencies are installed: `pip list`
3. Reinstall requirements: `pip install -r requirements.txt`

### Authentication Errors

If you encounter authentication errors:
```bash
gcloud auth application-default login
gcloud config set project YOUR_PROJECT_ID
```

---

Happy coding! 🚀

For more information, visit the [Google Cloud Platform Python Samples Repository](https://github.com/GoogleCloudPlatform/python-docs-samples).
