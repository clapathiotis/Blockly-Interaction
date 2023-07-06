# Blockly Interactions

This project extends the functionality of Blockly, an open-source library for building block-based programming editors, by incorporating additional interaction techniques. These techniques enhance the user experience and provide convenient shortcuts for common actions.

## Getting Started

To incorporate these interaction techniques into your Blockly project, follow these steps:

1. Locate the `index.html` file in your project.
2. Open the `index.html` file in a text editor.
3. Scroll down to find the JavaScript code section (indicated by <script> </script>).

## Keyboard Shortcuts for Buttons

Keyboard shortcuts are added to perform actions that are typically triggered by buttons in the user interface. The following shortcuts are available:

- **Shift + L**: Upload (calls `uploadClick()` function)
- **Shift + R**: Reset (calls `resetClick()` function)
- **Shift + D**: Discard (calls `discard()` function)
- **Shift + S**: Save Code (calls `saveCode()` function)
- **Shift + X**: Save (calls `save()` function)
- **Shift + M**: Load XML (calls `loadXML()` function)

To use these shortcuts, press and hold the **Shift** key, then press the corresponding letter key. The code added is shown below.

```html
document.addEventListener('keydown', function(event) {
  var key = event.key;
  var modifier = event.shiftKey ? 'Shift' : '';
  
  if (modifier === 'Shift' && key === 'L') {
    uploadClick();
  } else if (modifier === 'Shift' && key === 'R') {
    resetClick();
  } else if (modifier === 'Shift' && key === 'D') {
    discard();
  } else if (modifier === 'Shift' && key === 'S') {
    saveCode();
  } else if (modifier === 'Shift' && key === 'X') {
    save();
  } else if (modifier === 'Shift' && key === 'M') {
    loadXML();
  }
});
```

## Loading XML

To load an XML file into the Blockly workspace, the following steps had to take place before the interaction:

1. Add a button element to the HTML code:
   ```html
   <button id="load-xml-button">Load XML</button>
   <input type="file" id="load" style="display: none;" />
   ```
2. The button does not have an explicit action associated with it but allows the user to select a file using the file input field.

After the interaction was developed, a 'loadXML()' function to perform the above action was created:

1. The 'loadXML()' function is called when the Shift + M keyboard shortcut is triggered. The code for the newly added function is right below, again added at the script part of 'index.html':
```html
function loadXML() {
  var fileInput = document.getElementById('load');
  fileInput.click();
}
```

## Keyboard Shortcuts to Move Blocks
Arrow keys and the Tab key are assigned keyboard shortcuts to move blocks within the Blockly workspace. The following shortcuts are available:

- **Tab**: Changes the selection to the next block (if any). If no block is currently selected, the first block in the workspace is selected.
- **Left Arrow**: Moves the selected block to the left.
- **Up Arrow**: Moves the selected block upwards.
- **Right Arrow**: Moves the selected block to the right.
- **Down Arrow**: Moves the selected block downwards.

These keyboard shortcuts work when a block is selected in the workspace. If the selected block is connected to another block, it will be disconnected first before moving. If the selected block has connections, then the block does not move to ensure that the blocks remain in a relative position. Moving 1 block at a time is suggested/

Here is the code added, again at the JavaScript section of 'index.html':
```
document.addEventListener('keydown', function(event) {
  var selectedBlock = Blockly.selected;
  var workspace = Blockly.getMainWorkspace();

  if (event.keyCode === 9) { // Tab key
    event.preventDefault();

    if (!selectedBlock) {
      // If no block is currently selected, select the first block in the workspace
      var allBlocks = workspace.getAllBlocks();

      if (allBlocks.length > 0) {
        allBlocks[0].select();
      }
    } else {
      // If a block is currently selected, find the next block and select it
      var allBlocks = workspace.getAllBlocks();
      var selectedIndex = allBlocks.indexOf(selectedBlock);
      var nextIndex = (selectedIndex + 1) % allBlocks.length;
      var nextBlock = allBlocks[nextIndex];
      selectedBlock.unselect();
      nextBlock.select();
    }
  } else if (selectedBlock) {
    var deltaX = 0;
    var deltaY = 0;

    // Check if the block is connected to another block
    var isConnected = false;
    var blockConnections = selectedBlock.getConnections_();
    for (var i = 0; i < blockConnections.length; i++) {
      if (blockConnections[i].targetConnection) {
        isConnected = true;
        break;
      }
    }    
    if (isConnected) {
      // Disconnect the block from its parent
      selectedBlock.unplug(false);
    } else {
      // Adjust the delta values based on the arrow key pressed
      switch (event.keyCode) {
        case 37: // Left arrow
          event.preventDefault();
          deltaX = -Blockly.SNAP_RADIUS;
          break;
        case 38: // Up arrow
          event.preventDefault();
          deltaY = -Blockly.SNAP_RADIUS;
          break;
        case 39: // Right arrow
          event.preventDefault(); 
          deltaX = Blockly.SNAP_RADIUS;
          break;
        case 40: // Down arrow
          event.preventDefault();
          deltaY = Blockly.SNAP_RADIUS;
          break;
      }

      // Move the selected block by the delta values
      selectedBlock.moveBy(deltaX, deltaY);
      event.preventDefault();
    }
  }
});
```

## Integration
The provided code snippets need to be integrated into the '**index.html**' file of your Blockly project. Modify the existing file by adding the relevant sections of code at the appropriate locations, as described above.

## Notes
- These interaction techniques were implemented by modifying the '**index.html**' file only.
- Additional customization or styling can be applied as per your project requirements.
