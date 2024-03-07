# Find the process name for a popup window on mac

##### Metadata
created:: 2023-12-19 14:31
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: 
platform:: 
***

From https://superuser.com/a/1578707
You can use the [Automator.app](https://support.apple.com/en-gb/guide/automator/welcome/mac) for this:

1. Start Automator (in spotlight type `Automator.app` + Enter)
2. Create a new workflow.
3. On the menu select **Workflow** > **Record** (or click the 🔴 _[Record]_ button on the toolbar).
4. Interact with the window you wish to inspect and then click the ⬛️ _[Stop]_ button in the recording toolbar when done. (❗️ _If the system prompts you about missing accessibility access then grant it in System Settings_)
5. Drag the recorded steps of interest from the **Watch Me Do** section to the empty panel below (a plus button will appear during drag). _HINT_: You can also select all steps and drag them all together in order to create a single script.
6. Inspect the generated AppleScript to get the details you need.