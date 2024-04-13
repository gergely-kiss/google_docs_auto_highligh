# Google Docs Text Color Automation Script

This Google Apps Script automatically updates the colors of specific words in a Google Document. The script is designed to highlight the words "Il" in a lighter shade of blue and "Rt" in green, ensuring they are treated as standalone words.

## Setup Instructions

### Prerequisites
- You need a Google Account to access Google Docs and Google Apps Script.
- Basic familiarity with Google Docs and Apps Script Editor.

### Step 1: Open Google Docs
Create or open an existing Google Document where you want to use this script.

### Step 2: Access Apps Script
1. Click on **Extensions** in the Google Docs menu.
2. Select **Apps Script** from the dropdown menu.
3. This will open the Google Apps Script editor.

### Step 3: Paste the Script
1. In the Apps Script editor, remove any existing code.
2. Copy and paste the following script into the editor:

```javascript
function onOpen() {
  var ui = DocumentApp.getUi();
  ui.createMenu('Text Color')
    .addItem('Update Colors', 'updateColors')
    .addToUi();
}

function updateColors() {
  var doc = DocumentApp.getActiveDocument();
  var body = doc.getBody();
  var text = body.editAsText();
  var triggers = [
    {word: '\\bWORD_ONE_TO_UPDATE\\b', color: '#3333FF'}, // Light Blue colour
    {word: '\\bWORD_N_TO_UPDATEt\\b', color: '#00FF00'}  // Green colou
  ];

  triggers.forEach(function(trigger) {
    var regex = trigger.word;
    var foundElement = text.findText(regex);
    while (foundElement) {
      var foundText = foundElement.getElement().asText();
      var start = foundElement.getStartOffset();
      var end = foundElement.getEndOffsetInclusive();
      foundText.setForegroundColor(start, end, trigger.color);
      foundElement = text.findText(regex, foundElement);
    }
  });
}
```
### Step 4: Save and Name Your Project
Click the floppy disk icon or File > Save.
Enter a project name and click OK.
### Step 5: Close the Script Editor
Return to your Google Document after saving the script.

### Step 6: Run the Script
After reloading your Google Document, a new menu item labeled "Text Color" will appear in your Google Docs menu bar.

Click on "Text Color".
Select "Update Colors" to manually update the text colors in your document.
Usage
Whenever you need to update the colors of "WORD_ONE" and "WORD_N" ((you can list any number of words) in your document:

Click on Text Color in the Google Docs menu.
Select "Update Colors".
Notes
This script needs to be run manually unless a time-driven trigger is set up for periodic automatic updates.
To set up periodic updates, please refer to the optional createTimeDrivenTriggers function in the script documentation.
