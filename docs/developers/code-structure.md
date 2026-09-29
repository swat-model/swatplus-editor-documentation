# Code Structure & Contributions

Want to contribute to SWAT+ Editor development? Please consult with [Jaclyn Tech](mailto:jaclyn.tech@ag.tamu.edu) before development begins to ensure feasibility as well as lack of conflicts or repeated efforts. General bug fixes are welcome.

As described on the [home page](../index.md) of this documentation, there are two programming languages used in the editor: Python for all business operations, and Javascript/Typescript with Vue.js for the user interface.

## Back-end Organization

Connectivity between the Vue.js front-end and Python back-end for simple database CRUD (create, read, update, delete) operations are compiled into the `swatplus_rest_api`. The code for this is located in `/src/api/rest` and uses the [Flask](https://flask.palletsprojects.com/){ target="_blank" } framework.

Longer-running data processing actions such as weather imports, file writing, and reading output are compiled into `swatplus_api`. The code for this is located in `/src/api/actions`. This section is reserved for any process that is too long for a simple web request that is handled in the `swatplus_rest_api`. For more information about using the `swatplus_api` in your own coding projects, read the [Programmatic Access](index.md) documentation.

## Front-end Organization

There are multiple aspects to the front-end development. SWAT+ Editor is developed using web framework technology, so the GUI is given to the user with HTML, CSS, and Javascript. In order to compile this into a desktop application, the [Electron](https://electron.atom.io/){ target="_blank" } package is used. 

Connectivity to Electron is located in `/src/main`, while the Vue.js application resides in `/src/renderer`.

## Pull Requests

Pull requests should target the `dev` branch and not the `main`. All changes and current developments within SWAT+ Editor reside in the `dev` branch, so if you target the `main` you may already be behind and have to resolve conflicts.