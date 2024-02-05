# Redash.karpov.courses.font-size
This script will help You increase the font size in the editor window to make the coding process more convenient.

<div style="display: flex;">
  <img src="/pictures/Redash_fonts_size_before.png" alt="Before" style="width: 49%;">
  <img src="/pictures/Redash_fonts_size_after.png" alt="After" style="width: 49%;">
</div>
<br/><br/>
1. Firstly install Tampermonkey extension for your web browser  

   For Google Chrome: https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en-US&utm_source=ext_sidebar  
   For Microsoft Edge: https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepeloendndfphd?hl=ru  
2. Secondly open Tampermonkey settings
<div style="display: flex;">
  <img src="/pictures/setup.png" alt="Settings" style="width: 98%;">
  </div>
<br/><br/>
3. Firdly press the “Create a new script...” button and paste the script from the window below here.
<div style="display: flex;">
  <img src="/pictures/new_script.png" alt="Create a new script" style="width: 98%;">
  </div>
<br/><br/>

```
// ==UserScript==
// @name         Redash.karpov.courses.font-size
// @namespace    your-namespace
// @version      1.0
// @description  Increases the font size in the SQL query writing window in Redash
// @match        https://redash.public.karpov.courses/queries/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Set the desired font size in pixels
    var fontSize = '20px';
    var fontSize_autocomplete = '18px';

    // Function to change font size
    function changeFontSize() {
        var editor = document.getElementsByClassName('ace_editor')[0];
        if (editor) {
            editor.style.fontSize = fontSize;
        }

        var autocomplete = document.getElementsByClassName('ace_autocomplete')[0];
        if (autocomplete) {
            autocomplete.style.fontSize = fontSize_autocomplete;
;
        }
    }

    // Waiting for the element to load using MutationObserver
    var observer = new MutationObserver(function(mutations) {
        mutations.forEach(function(mutation) {
            if (mutation.addedNodes && mutation.addedNodes.length > 0) {
                changeFontSize();
            }
        });
    });

    // Find an element with the "ace_editor" class and start monitoring the changes
    var targetNode = document.body;
    var config = { childList: true, subtree: true };
    observer.observe(targetNode, config);

    // Changing the font size immediately after the page loads
    changeFontSize();
})();
```
To make the font even larger, its size can be set using the fontSize and fontSize_autocomplete parameters.
<br/><br/>
4. Fourthly press the "File" -> "Save" button to save the script.
<div style="display: flex;">
  <img src="/pictures/save_script.png" alt="Save script" style="width: 98%;">
  </div>
<br/><br/>

5. Fifthly, make sure that the Enabled button has been pressed in one of two places.
<div style="display: flex;">
  <img src="/pictures/enable_script_1.png" alt="Enable script" style="width: 49%;">
  <img src="/pictures/enable_script_2.png" alt="Enable script" style="width: 49%;">
  </div>
<br/><br/>

Now, when the page loads, the fonts will be loaded in the size set in the script and you no longer need to go to the developer menu to change them every time.
