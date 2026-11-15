# Basic shit

## 1. Files and folders

Your computer stores information in **files**, which are organised into **folders** (also called *directories*).

- A file contains information, such as a Python programme, an image, or a text document.
- A directory contains files and possibly other directories.
- A file name identifies a file. For example, `hello.py` is a Python file, where `.py` is the file extension.
- A file path describes where a file is located on your computer.

For example, suppose your computer contains the following:

```text
Home
└── Desktop
    └── Programming
        ├── hello.py
        └── calculator.py
```

Here, `hello.py` is inside the `Programming` folder, which is inside `Desktop`.

The location of a file matters: **your computer needs to know where a file is before it can find or run it.**

## 2. VS Code

VS Code is a **code editor**. It lets you write and modify code, but writing something in the editor does not necessarily mean you've saved it as a file.

For example, you might type:

```python
print("Hello, world!")
```

At this point, you have written some code, but you might not have saved it anywhere.

To save your work:

1. Press `Ctrl + S` (Windows) or `Cmd + S` (Mac).
2. If this is a new file, choose a folder in which to save it.
3. Give it a name, such as `hello.py`.
4. Check that the file appears in the folder you selected.

N.b. Editing changes what you see in VS Code; saving writes those changes to the file on your computer. Unless Auto Save is enabled, you must save your changes yourself.

For your convenience, go to vscode and press `cmd` + `shift` + `p` at the same time, you should see a little textbox at the top where you can type. Keep the `>` and enter `settings.json`, hit enter, and it should show you a cryptic file that you don't really understand. It doesn't matter, add a new line before the closing curly brace of the file and add:
```
"files.autoSave": "onFocusChange",
```
then hit save. This helps you to save your file whenever you click away from the editor.

Usually you would use **File → Open Folder** in VS Code to open an entire programming folder. This makes it easier to keep track of where your files are. E.g. you can create some folder on your desktop that contains your work for something (e.g. cs50) and then when you want to work just within that workspace, simply find it in finder or on your desktop, and gently **drag the folder onto your vscode app's icon** to open the folder in vscode. That way, the terminal that opens would also open in that folder.

## 3. The command line (terminal)

The command line is a textual interface for interacting with your computer. Instead of clicking buttons, you type commands.

For example, to run a Python script:

```bash
python hello.py
```

On a Mac, you will commonly use `python3 hello.py` instead.

The terminal and the VS Code editor are **two different things**:

- The editor is where you write code.
- The terminal is where you can enter commands to run that code, navigate folders, and perform other operations.

You can open VS Code's integrated terminal using **Terminal → New Terminal**.

### The current working directory

Here's something important: **the terminal always has a current location**, called its *current working directory*.

Imagine you're standing inside a particular folder. When you type a command, the terminal interprets it relative to where you're standing, unless you explicitly specify another location.

For example, suppose you're currently inside your home folder, but `hello.py` is stored in `Desktop/Programming`.

Running:

```bash
python hello.py
```

will not find the script, because the terminal is looking for `hello.py` in your current folder.

You first need to navigate to the correct folder, or provide the script's full path.

## 4. Essential terminal commands

You only need a handful of commands to get started.

| Command | What it does |
|---|---|
| `pwd` | Shows the current working directory |
| `ls` | Lists files and folders in the current directory |
| `cd foldername` | Enters a folder |
| `cd ..` | Moves up one folder |
| `cd ~` | Goes to your home directory |
| `clear` | Clears the terminal display |
| `mkdir -p` | Creates a folder if it doesn't already exist |

For example:

```bash
pwd # if you just open a terminal by default it is at ~/ which is the same as /Users/[yourusername]
cd Desktop # this folder stores all of the things you see on your desktop
mkdir -p cs50 # create a folder for cs50
cd cs50 # go into that location
ls # see files
```

If `hello.py` appears in the list, you can run it:

```bash
python3 hello.py
```

3 is important because macos has some cunty built-in python that already occupies the 'python' command, so python3 is like using the correct python

**Important:** Running a command does not automatically change the terminal's directory. You need `cd` to navigate.

## 5. Paths: telling the computer where something is

There are two main ways to describe a file's location.

**Relative path:** Describes a location starting from the current working directory.

```bash
python3 cs50/hello.py
```

This works if you're currently in the `Desktop` folder.

**Absolute path:** Describes the complete location, independently of the current working directory.

For example, on macOS:

```bash
python3 /Users/jayz/Desktop/cs50/hello.py
```

both approaches can run the same file. The difference is where the terminal starts looking.

You can also use `.` for the current directory and `..` for its parent directory.

## 6. Putting everything together

Let's run your first Python programme from scratch.

1. Create a folder called `cs50` on your Desktop.
2. Open VS Code and select **File → Open Folder → cs50**.
3. Create a file called `hello.py`.
4. Type the following code:

   ```python
   print("Hello, world!")
   ```

5. Save the file using `Cmd + S`.
6. Open **Terminal → New Terminal** in VS Code.
7. Check the terminal's location using `pwd`. It will normally start in the folder you opened in VS Code.
8. Run the programme using `python3 hello.py`

If everything works, you should see:

```text
Hello, world!
```

if it fucks up then let me know

## 7. Common mistakes

| Problem | Likely reason | Solution |
|---|---|---|
| `File not found` | Terminal is in the wrong folder, or the filename is incorrect | Check `pwd` and `ls`, then use `cd` |
| Changes aren't reflected when running | You forgot to save | Save the file before running |
| `python: command not found` | Python isn't installed or that command isn't available | Check the Python installation and try `python3` or `py` |
| `No such file or directory` when using `cd` | The folder doesn't exist at that location | Check the spelling and current directory |
| A command with spaces in a path fails | The terminal treats spaces as separators | Put the path in quotation marks, e.g. `"My Folder/hello.py"` |
| Code produces no visible output | The programme doesn't print anything | Try `print("Hello!")` |


# some python shit

## 1. Libraries and packages
python comes with a **standard library** (e.g. `math`, `random`, `os`), but you can install additional third-party packages (e.g. `numpy`, `requests`).

Use `import` to fuck with them

```python
import math
print(math.sqrt(16))
```

A **module** is typically a single Python file; 
a **package** organises modules together; 
a **library** is a general term for reusable code.

### 2. pip: Installing packages
`pip` is Python's package installer. It downloads and installs third-party packages, usually from PyPI (Python Package Index).

```bash
python -m pip install requests
python -m pip uninstall requests
python -m pip list
```

installing a package makes it available to the relevant Python environment; `import` makes it accessible within your programme

### 3. Virtual environments (`venv`)
Different projects may require different packages or versions. A **virtual environment** gives each project its own isolated set of installed packages, avoiding conflicts.

```bash
python -m venv .venv           # Create environment
```

Activate it:

```bash
source .venv/bin/activate     # macOS / Linux
.venv\Scripts\Activate.ps1    # Windows PowerShell
```

Then install packages as usual:

```bash
python -m pip install requests
deactivate                   # Exit environment
```

Once activated, `python` and `pip` use the environment's Python and packages.

### 4. Dependencies and `requirements.txt`
**Dependencies** are external packages your project needs to run.

Record installed package versions:

```bash
python -m pip freeze > requirements.txt
```

Install the recorded dependencies on another computer or in a new environment:

```bash
python -m pip install -r requirements.txt
```

Typically, share `requirements.txt` with your project, but **do not share the `.venv` folder**.

### 5. Typical project workflow

```bash
cd my-project
python -m venv .venv
source .venv/bin/activate
python -m pip install requests
python -m pip freeze > requirements.txt
python main.py
```

`pip` installs packages, `import` uses them, `venv` isolates them, and `requirements.txt` records them.


Nah for your cs50 stuff don't even bother but when you move onto some pd np stuff yeah 
