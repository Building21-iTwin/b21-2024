# Steps to setup a local viewer

## Install Pre-requisites (Should already be done)

1. Install Docker desktop
    - https://docs.docker.com/engine/install/ubuntu/
    - https://docs.docker.com/engine/install/linux-postinstall/
1. Install the Dev Container Extension in VSCode
    - Search for `ms-vscode-remote.remote-containers`

## Initialize the Viewer

There is a [standard tutorial](https://developer.bentley.com/tutorials/web-application-quick-start/) but we will use the slightly modified tutorial below.

1. Create an empty application by running the command below in the terminal:
    ```bash
    npx create-react-app phila-city --template @itwin/web-viewer --scripts-version @bentley/react-scripts
    ```
    - This will generate a new application based on the iTwin Viewer React component.
    - By default, the viewer will be stored in a directory called `phila-city`
1. Run `cd phila-city` to move into the app directory
1. In the terminal, run `mkdir .devcontainer`
1. Setup the DevContainer configuration by copying the following files into a `.devcontainer` folder
    - [./devcontainer/devcontainer.json](./devcontainer/devcontainer.json)
    - [./devcontainer/Dockerfile](./devcontainer/Dockerfile)
1. In VSCode, press `Crtl+P` to open the command palette and search `Dev Containers: Reopen folder locally`.
    - This may take some time the first time you run it
1. Once the container finishes initializing, open the terminal and run `npm install`
1. Open the .env file
1. Enter the appropriate values for:
```
IMJS_AUTH_CLIENT_CLIENT_ID = ""
IMJS_AUTH_CLIENT_REDIRECT_URI = "http://localhost:3000/signin-oidc"
IMJS_AUTH_CLIENT_LOGOUT_URI = ""
IMJS_AUTH_CLIENT_SCOPES ="imodelaccess:read imodels:read realitydata:read"
IMJS_AUTH_AUTHORITY="https://ims.bentley.com"
```
1. Set the iTwin and iModel Ids:
```
IMJS_ITWIN_ID = ""
IMJS_IMODEL_ID = ""
```
1. In the terminal window, enter `npm start`. This will serve the application with live reloading.
