# Lecture demos

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

4. Confirm that `data/kc_house_data.csv` is present. Run the commands from this
   `varada` directory so the notebook can find the dataset.
5. Start JupyterLab:

   ```sh
   uv run --locked jupyter lab lecture-3-demo.ipynb
   ```

   Use the Python 3 kernel. The notebook includes TODO exercises to complete
   during class; running all cells before filling these in will produce errors.

### VS Code

After `uv sync --locked`, open this `varada` directory in VS Code with the Python
and Jupyter extensions installed. Open the notebook, select **Select Kernel →
Python Environments**, and choose this directory's `.venv` interpreter.

## Instructor maintenance

`pyproject.toml` declares the dependencies, `.python-version` selects Python 3.12,
and `uv.lock` records the resolved package versions. Commit all three files along
with this README, the notebook, and `data/kc_house_data.csv`. `.venv` is already
ignored by the repository.

Before class, verify that the notebook's first cell loads the dataset successfully.

To add a dependency, run `uv add PACKAGE` from this directory. To intentionally
refresh all locked versions, run `uv lock --upgrade` followed by `uv sync --locked`.
Check the demo after changing dependencies and commit both `pyproject.toml` and
`uv.lock`. Students should use `uv sync --locked` after pulling updates.
