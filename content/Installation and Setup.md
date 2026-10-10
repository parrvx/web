## Polars

- Polars is a data analysis library built in Rust with bindings for Python.
- We need to install Python to install Polars.

## Installing Python and Polars

- `uv` is a command-line tool for managing Python projects.
- `uv` helps download a specific version of Python and various libraries.
- `uv sync` downloads the requirements specified in the `pyproject.toml` file.
- The command will download Python, Polars, Jupyter Lab, and more.

## Jupyter Lab

- Jupyter Lab will be our coding environment for the course.
- A Jupyter Notebook consists of Python cells and text cells.
- Execute the cell with `Shift + Enter` or `Ctrl + Enter`.
- Jupyter will output the last cell evaluation below the cell.

## Intro to Jupyter Notebook

- Jupyter Notebooks used to be called iPython Notebooks.
- Jupyter Notebooks have a `.ipynb` file extension.
- Copy-paste functionalities are available under **Edit** menu.
- The options in the **View** menu toggle the header and the toolbar.
- If serious errors (i.e., frozen execution) occur, acces the **Kernel** menu and select `Restart & Clear Output`.

## Create, Saving, and Closing a Jupyter Notebook

- Save a Jupyter Notebook with `Command + S` (macOS) and `Control + S` (Windows). Jupyter includes an auto-save feature.
- To shut down a Notebook, save and close its tab. 
- Click the **Running Terminals and Kernels** button on the left-hand menu (the second icon from the top).
- Click **Shut Down All** in the **Kernels** section or individually target a specific Notebook you'd like to close.
- Go to **File -> Shut Down** in the main menu.

## Cell Types and Cell Modes

- Cell types: **Code** and **Markdown**. Select from the dropdown menu in the toolbar.
- Cell modes: **Edit Mode** (green outline) or **Command Mode** (blue outline).
- Double-click into a Markdown cell or single-click into a code cell to enter **Edit Mode**.
- Press the Escape key to go to **Command Mode**.
- **Command Mode** is for notebook operations - navigation, cell deletion, cell movement
- Alternatively, in command mode, press \m\ to make a cell Markdown and \y\ to make it a code cell

## Code Cell Execution


- We need to \execute\ a cell to run the Python code inside of it.
- Press **Shift + Enter** to execute a code cell and move to the next cell.
- Press **Ctrl + Enter** to execute a code cell and stay in the same cell.
- Executing a Markdown cell will render the formatting within it.
- A cell can be executed any number of times.
- You can execute cells in any order.

## Popular Keyboard Shortcuts

- In Command Mode, press `a` to insert a cell above the currently selected one
- In Command Mode, press `b` to insert a cell below the currently selected one
- In Command Mode, press `x` to cut a cell (i.e delete it)
- Both add options are available on the main menu under **Insert**.

## Import Libraries into Jupyter Lab

- Use Python's `import` keyword to bring a library into the Jupyter Notebook.
- We can optionally assign an alias to a library with the `as` keyword.
- The common alias for Polars is `pl`.
- Make sure to execute the `import` cell every time you launch the Notebook.

```{python}

```

- Access the Polars library with `pl`.
- Write a dot and press Tab to see the top-level library constructs.

```{python}

```

### Further Reading

- https://docs.pola.rs/
- https://docs.pola.rs/api/python/stable/reference/index.html
