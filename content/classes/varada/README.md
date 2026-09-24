# Lecture demos

This directory contains CPSC 330 lecture demo notebooks and a shared Python
environment. Follow the setup below once, then open the notebook for your lecture.

## Student setup

1. Install Git and [uv](https://docs.astral.sh/uv/getting-started/installation/).
2. Clone the repository and enter this directory:

   ```sh
   git clone https://github.com/UBC-CS/cpsc330-2026W1.git
   cd cpsc330-2026W1/content/classes/varada
   ```

   If you already cloned the repository, use your existing checkout.

3. Create the environment with the committed package versions:

   ```sh
   uv sync --locked
   ```

   uv downloads Python 3.12 if needed and creates a local `.venv`. No manual
   activation or separate Python installation is required.

4. Check the notebook's setup instructions for any required datasets or downloads.
   Local datasets are stored in `data/`. Run commands from this `varada` directory
   so the notebooks can resolve their relative paths.
5. Start JupyterLab:

   ```sh
   uv run --locked jupyter lab
   ```

   Open the notebook for your lecture and use the Python 3 kernel. Run cells in
   order, following the notebook's discussion prompts and exercises. Some demos
   include intentional failure examples or interactive controls; follow the
   instructions beside those cells.

### VS Code

After `uv sync --locked`, open this `varada` directory in VS Code with the Python
and Jupyter extensions installed. Open the notebook, select **Select Kernel →
Python Environments**, and choose this directory's `.venv` interpreter.

## Instructor maintenance

`pyproject.toml` declares the dependencies, `.python-version` selects Python 3.12,
and `uv.lock` records the resolved package versions. Commit all three files along
with this README and any updated notebooks. Include required local datasets and
supporting files when suitable for distribution, or document how to obtain them.
`.venv` is already ignored by the repository.

Before class, verify the relevant notebook from a fresh kernel: check setup,
data loading, runnable cells, and any interactive controls. Clearly label
intentional errors and document any additional downloads in the notebook.

To add a dependency, run `uv add PACKAGE` from this directory. To intentionally
refresh all locked versions, run `uv lock --upgrade` followed by `uv sync --locked`.
Check the demo after changing dependencies and commit both `pyproject.toml` and
`uv.lock`. Students should use `uv sync --locked` after pulling updates.
