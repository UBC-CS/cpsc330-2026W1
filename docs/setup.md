# Setting up your coding environment

## Working in PrairieLearn

You can complete assignments in the **PrairieLearn workspace**, which provides the coding environment in your browser. Follow the workspace instructions in each assignment. **No local installation is needed for this workflow.** You can also read the [course book](https://ubc-cs.github.io/cpsc330-book/) in your browser.

The rest of this guide is optional: use it if you want to run lecture notebooks and demos or work on assignments on your own computer. It assumes you are comfortable opening a terminal and navigating between folders.

## Local setup: install the tools once

We use **uv** to manage Python and packages, and **JupyterLab** or **VS Code** to run notebooks. The lecture environment files live in the [cpsc330-book repository](https://github.com/UBC-CS/cpsc330-book). The `cpsc330-2026W1` repository contains course logistics and these instructions.

Use **PowerShell on Windows** and your usual **Terminal on macOS or Linux**. After installing uv, the commands below are the same on all three platforms. You do not need WSL, Conda, or a separate Python installation for these instructions.

### Install uv

Use the command for your operating system from the [official uv installation guide](https://docs.astral.sh/uv/getting-started/installation/).

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**macOS or Linux:**

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Close and reopen your terminal after installation, then check:

```text
uv --version
```

You should see something like this:

```text
uv 0.12.5 (210d1f678 2026-08-14 aarch64-apple-darwin)
```

Your version number, build date, and platform details may differ. Seeing a uv version confirms that the command is available in your terminal.

### Install Git and choose an editor

Install [Git](git_installation.md) if you want to clone and update the book repository or use Git for assignment work. Git is optional if you only work from assignment ZIP files.

- **JupyterLab:** installed with the course environment; no separate installation step is needed.
- **VS Code:** install [VS Code](https://code.visualstudio.com/) and Microsoft's **Python** and **Jupyter** extensions.

## Run lecture notebooks and demos locally

In a terminal, navigate to the folder where you want to keep the book, then run these commands one line at a time:

```text
git clone https://github.com/UBC-CS/cpsc330-book.git
cd cpsc330-book
uv sync --locked
```

uv uses the supplied `.python-version` file to select Python 3.12, downloading it if needed, and installs the packages into a `.venv` folder. The first installation may take a while because the course includes large machine-learning libraries.

The `pyproject.toml` file specifies the dependencies, and `uv.lock` records their resolved versions. `--locked` checks that these files agree without changing the lockfile. Keep both files as supplied by the course.

Choose one of the following ways to open your notebooks. These steps also apply to an assignment folder after you have created its environment.

### Option A: JupyterLab

From the folder containing `pyproject.toml` and `uv.lock`, run:

```text
uv run --locked jupyter lab
```

Open a notebook in the browser window that appears. Choose **Python 3 (ipykernel)** if prompted for a kernel. Keep the terminal running while you work; when finished, save your notebooks and press **Ctrl+C** in the terminal to stop the server, confirming shutdown if prompted.

Use this launch command each time so JupyterLab runs in that folder's environment. No manual environment activation is required.

### Option B: VS Code

1. In VS Code, choose **File → Open Folder** and open `cpsc330-book` (or the extracted assignment folder).
2. Open a notebook and click **Select Kernel** at the top right. Choose **Select Another Kernel**, if shown, then **Python Environments** and the `.venv` belonging to this folder.
3. Run cells with **Shift+Enter**.

If you also work with Python scripts, use **Python: Select Interpreter** in the Command Palette to select the same environment. Notebook kernel selection is a separate step.

The interpreter paths are:

| Platform | Interpreter inside the project folder |
| --- | --- |
| Windows | `.venv\Scripts\python.exe` |
| macOS / Linux | `.venv/bin/python` |

If the environment does not appear, make sure `uv sync --locked` completed successfully, then reload the VS Code window. See [uv's Jupyter and VS Code guide](https://docs.astral.sh/uv/guides/integration/jupyter/) for more details.

### Update the lecture materials

From the `cpsc330-book` folder, run:

```text
git pull
uv sync --locked
```

Restart any running notebook kernels after updating the environment. Save personal copies of notebooks before editing them; edits to tracked course files can conflict with later updates. If Git reports a conflict, preserve your work and ask for help before discarding changes.

## Work on assignments locally

PrairieLearn remains available if you prefer to work in the browser. For local work, use the assignment's downloadable ZIP and its accompanying instructions.

1. **Extract the entire ZIP** into a folder of your choice, outside the cloned book and logistics repositories. Keep the notebook and data in their supplied relative locations.
2. Check that the extracted folder contains `pyproject.toml`, `uv.lock`, and `.python-version`, alongside the notebook and data. These files specify the environment for that assignment. If they are missing, check the assignment instructions or ask the teaching team for the local setup files.
3. Open a terminal in that folder and run:

   ```text
   uv sync --locked
   ```

4. Launch JupyterLab with `uv run --locked jupyter lab`, or open the assignment folder in VS Code and select **that folder's `.venv`**, as described above.
5. Save your work and follow the assignment's instructions to upload the required files to PrairieLearn and submit. Files saved on your computer do not automatically appear in PrairieLearn.

Each assignment has its own environment. Use its supplied environment files even if you have already set up the book environment. You do not need to clone either course repository to use an assignment ZIP that includes these files.

### Optional: use a private Git repository

You can turn the extracted assignment folder into a **private** Git repository. Where collaboration is permitted by the assignment, share it only with your authorized partners. Keep your notebook and the supplied environment files in version control. Add `.venv/` and `.ipynb_checkpoints/` to `.gitignore`; follow the assignment's guidance about tracking data files.

Each collaborator clones the private repository, runs `uv sync --locked`, and selects their own local `.venv`. Do not commit or share the `.venv` folder itself.

## Check your environment

Run this cell in a notebook opened through JupyterLab or VS Code:

```python
import sys
import numpy as np
import pandas as pd
import sklearn
import matplotlib.pyplot as plt

print("Python:", sys.version)
print("Interpreter:", sys.executable)
print("scikit-learn:", sklearn.__version__)
plt.plot([0, 1, 2], [0, 1, 4])
plt.show()
```

You should see version information and a small plot. The interpreter path should point inside the `.venv` of the book or assignment folder you are working in.

## Troubleshooting

- **`uv` is not recognized:** restart your terminal (and VS Code if using its terminal). If the problem persists, consult the [uv installation guide](https://docs.astral.sh/uv/getting-started/installation/).
- **No `pyproject.toml` found:** navigate to the book root or the extracted assignment folder containing the environment files, then rerun the command.
- **A notebook cannot import a package:** check `sys.executable` using the cell above. Select the correct kernel, run `uv sync --locked` in the corresponding folder, and restart the kernel.
- **A data file cannot be found:** extract the complete assignment ZIP and preserve its folder structure. For lecture notebooks, follow any data-download instructions in the notebook.
- **The lockfile is out of date or installation fails:** for the book, first obtain the latest course files with `git pull`. For assignments, use the files supplied with that assignment. Share the error message, operating system, and `uv --version` with the teaching team. Avoid removing dependencies or upgrading packages to work around the error, since that changes the course environment.

Some demos may require additional software or downloaded models; follow the instructions provided with those demos. If local setup prevents you from working on an assignment, use its PrairieLearn workspace and bring the error to office hours or tutorials.
