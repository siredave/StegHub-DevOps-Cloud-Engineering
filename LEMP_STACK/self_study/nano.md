# Basic Nano Commands

Nano is a simple, easy-to-use text editor for Unix and Linux systems.It is the standard de facto text editor of Linux for system maintainers, comes pre-installed on Ubuntu and its derivative including Linux Mint. It’s fairly advanced for newbies but not too hard to get accustomed to. Here are some basic commands to help you get started.

## Opening a File

To open a file with Nano, use the following command:

```sh
nano filename
```

If the file does not exist, Nano will create it.

## Basic Navigation

- **Move Cursor:** Use the arrow keys to move the cursor up, down, left, and right.
- **Move to Beginning of Line:** `Ctrl + A`
- **Move to End of Line:** `Ctrl + E`
- **Move Forward One Word:** `Ctrl + Space`
- **Move Backward One Word:** `Alt + Space`
- **Scroll Up One Page:** `Ctrl + Y`
- **Scroll Down One Page:** `Ctrl + V`

## Editing

- **Cut Text (Cut the current line):** `Ctrl + K`
- **Uncut Text (Paste the cut line):** `Ctrl + U`
- **Copy Text:** `Alt + ^` (Set a mark) and move the cursor to select text, then `Alt + 6`
- **Paste Text:** `Ctrl + U`
- **Delete Character:** `Ctrl + D`
- **Backspace:** `Backspace` key

## Searching

- **Search for Text:** `Ctrl + W` and then type the search query and press `Enter`
- **Find Next Occurrence:** `Ctrl + W` and then `Ctrl + W` again
- **Search and Replace:** `Ctrl + \` and then follow the prompts

## Saving and Exiting

- **Save the File:** `Ctrl + O`, then press `Enter` to confirm
- **Exit Nano:** `Ctrl + X`
- **Save and Exit:** If you have unsaved changes, Nano will prompt you to save the changes. Press `Y` to save, `N` to discard, and `Ctrl + C` to cancel the exit.

## Other Useful Commands

- **Display Help:** `Ctrl + G`
- **Show Current Cursor Position:** `Ctrl + C`
- **Cut from Cursor to End of Line:** `Ctrl + K`
- **Insert Another File:** `Ctrl + R`

## Example Usage

1. Open a file:
    ```sh
    nano example.txt
    ```

2. Edit the file using the commands above.

3. Save the changes:
    ```sh
    Ctrl + O
    ```

4. Exit Nano:
    ```sh
    Ctrl + X
    ```

By mastering these basic commands, you'll be able to efficiently navigate and edit files using Nano.
