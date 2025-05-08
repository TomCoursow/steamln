# steamls - Steam Game Name to Compatdata Folder Mapper

## Description

`steamls` is a simple bash script for Linux that helps you identify which numbered `compatdata` folder in your Steam library corresponds to which installed game. This is particularly useful for managing save files, mods, or configuration located within the Wine prefixes created by Steam Play (Proton).

The script reads the `appmanifest` files located in your Steam library folders to extract the game AppIDs (which is the `compatdata` folder number) and names.

## Features

* Lists all installed games and their corresponding `compatdata` folder numbers when run without arguments. 
* Allows filtering the list by providing a game name or a regular expression pattern as an argument (case-insensitive matching).
* Supports searching across multiple Steam library locations (configured within the script).

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/TomCoursow/steamln.git
    cd steamls
    ```

2.  **Ensure the script is executable:**
    Navigate into the cloned repository directory and make sure the `steamls` file has execute permissions.
    ```bash
    chmod +x steamls
    ```

3.  **Add the script to your PATH:**
    For easy access from any terminal location, you should place the `steamls` script in a directory that is included in your system's PATH environment variable. A common location for user-specific executables is `~/bin`.

    Create the `~/bin` directory if it doesn't exist:
    ```bash
    mkdir -p ~/bin
    ```

    Copy or link the `steamls` script to `~/bin`:
    ```bash
    cp steamls ~/bin/
    # Or create a symbolic link if you prefer:
    # ln -s /path/to/your/cloned/repo/steamls ~/bin/steamls
    ```

4.  **Add `~/bin` to your PATH (if necessary):**
    Edit your `~/.bash_profile` file (or `~/.bashrc` depending on your shell configuration) to add `~/bin` to your PATH.

    Open the file in a text editor:
    ```bash
    nano ~/.bash_profile
    # or
    # nano ~/.bashrc
    ```

    Add the following line to the end of the file (if no Home bin folder is part of the PATH yet):
    ```bash
    export PATH="$HOME/bin:$PATH"
    ```

    Save the file and exit the editor.

5.  **Apply the changes:**
    Either close and reopen your terminal, or source your bash profile:
    ```bash
    source ~/.bash_profile
    # or
    # source ~/.bashrc
    ```

Now you should be able to run the `steamls` command from any directory in your terminal.

## Usage

* **List all installed games and their compatdata folders:**
    ```bash
    steamls
    ```
    Example Output:
    ```
    Compatdata Folder: 238960 -> Game: Path of Exile
    Compatdata Folder: 359870 -> Game: FINAL FANTASY X/X-2 HD Remaster
    Compatdata Folder: 362890 -> Game: Black Mesa
    Compatdata Folder: 397540 -> Game: Borderlands 3
    Compatdata Folder: 427520 -> Game: Factorio
    Compatdata Folder: 453090 -> Game: Parkitect
    Compatdata Folder: 454650 -> Game: DRAGON BALL XENOVERSE 2
    Compatdata Folder: 526870 -> Game: Satisfactory
    Compatdata Folder: 582010 -> Game: Monster Hunter: World
    Compatdata Folder: 729040 -> Game: Borderlands GOTY Enhanced
    Compatdata Folder: 983870 -> Game: FOUNDRY
    ```

* **Find the compatdata folder for a specific game (using a pattern):**

    Provide a pattern as an argument. The matching is case-insensitive.
    ```bash
    steamls "Borderlands"
    ```
    This would match games like "Borderlands GOTY Enhanced" and "Borderlands 3".

    Example Output:
    ```
    Compatdata Folder: 397540 -> Game: Borderlands 3
    Compatdata Folder: 729040 -> Game: Borderlands GOTY Enhanced
    ```

    The pattern may use grep search pattern
    ```bash
    steamls "FINAL.*HD"
    ```
    This regular expression would match "FINAL FANTASY X/X-2 HD Remaster".

    Example Output:
    ```
    Compatdata Folder: 359870 -> Game: FINAL FANTASY X/X-2 HD Remaster
    ```

## Customization

If you have Steam libraries in locations other than the default `~/.local/share/Steam/`, you can add their `steamapps` paths to the `STEAMAPPS_PATHS` array at the beginning of the `steamls` script:

```bash
# Define an array of Steam library steamapps paths to search
# Add your additional library paths to this array
STEAMAPPS_PATHS=(
    "${DEFAULT_STEAMAPPS_PATH}"
    "/path/to/your/other/steam/library/steamapps" # <-- Add your custom path here
)
