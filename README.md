# Blockly Interactions

This project extends the functionality of Blockly, an open-source library for building block-based programming editors, by incorporating additional interaction techniques. These techniques enhance the user experience and provide convenient shortcuts for common actions.

## Getting Started

To incorporate these interaction techniques into your Blockly project, follow these steps:

1. Locate the `index.html` file in your project.
2. Open the `index.html` file in a text editor.
3. Scroll down to find the JavaScript code section.

## Keyboard Shortcuts for Buttons

Keyboard shortcuts are added to perform actions that are typically triggered by buttons in the user interface. The following shortcuts are available:

- **Shift + L**: Upload (calls `uploadClick()` function)
- **Shift + R**: Reset (calls `resetClick()` function)
- **Shift + D**: Discard (calls `discard()` function)
- **Shift + S**: Save Code (calls `saveCode()` function)
- **Shift + X**: Save (calls `save()` function)
- **Shift + M**: Load XML (calls `loadXML()` function)

To use these shortcuts, press and hold the **Shift** key, then press the corresponding letter key.

## Loading XML

To load an XML file into the Blockly workspace, perform the following steps:

1. Add a button element to the HTML code:
   ```html
   <button id="load-xml-button">Load XML</button>
   <input type="file" id="load" style="display: none;" />
   ```
2. The button does not have an explicit action associated with it but allows the user to select a file using the file input field.

3. The 'loadXML()' function is called when the Shift + M keyboard shortcut is triggered or when the button is clicked.

## Keyboard Shortcuts to Move Blocks
Arrow keys and the Tab key are assigned keyboard shortcuts to move blocks within the Blockly workspace. The following shortcuts are available:

- **Tab**: Changes the selection to the next block (if any). If no block is currently selected, the first block in the workspace is selected.
- **Left Arrow**: Moves the selected block to the left.
- **Up Arrow**: Moves the selected block upwards.
- **Right Arrow**: Moves the selected block to the right.
- **Down Arrow****: Moves the selected block downwards.

These keyboard shortcuts work when a block is selected in the workspace. If the selected block is connected to another block, it will be disconnected first before moving.

## Integration
The provided code snippets need to be integrated into the '**index.html**' file of your Blockly project. Modify the existing file by adding the relevant sections of code at the appropriate locations, as described above.

## Notes
- These interaction techniques were implemented by modifying the '**index.html**' file only.
- Additional customization or styling can be applied as per your project requirements.
