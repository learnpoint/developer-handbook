# JavaScript Guidelines

## Naming JavaScript files

- JavaScript files are located in the ```Scripts``` folder.
- JavaScript files are named with lowercase letters.
- Multiple words are separated with a dash. For example: ```simple-confirm.js```.
- Every component, control and page is coded in its own JavaScript file.
- JavaScript files for controls and pages are prefixed with ```ascx``` or ```aspx```. For example: ```ascx-intership-settings.js```.

## Including JavaScript files

JavaScript files for controls and pages must be explicitly included. This is done like so:

1. Declare the JavaScript file in ```Code/Javascript/Includes.vb```.
2. Include the JavaScript file in the load handler in code behind of the control or page:
    ```vb
    Private Sub LoadHandler(...) Handles Me.Load
        Javascript.Includes.Add(Javascript.Includes.ASCX_GRADING, Me)
    End Sub
    ```

JavaScript files for components are included in the same way. Except for those that are very commonly used, like ```simple-confirm``` or ```flash-message```. They should always be available and therefore included directly in the master page.
