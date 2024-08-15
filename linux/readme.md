# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application that allows you to quickly configure Virto Commerce v3 to run in a Linux and Windows environment. 
You can also use docker files to create your custom images (check issues section below before creating images).

Before stating the setup process ensure that your system have needed software installed:
    [git](https://git-scm.com/downloads)
    [docker](https://docs.docker.com/engine/install/)
    [Node.js v20](https://nodejs.org/en/download/) (**20.11.0** or later)
    [.Net SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)

## How to use these multi-container application
    1. Run the backend part:
        clone `vc-docker` repository:
            mkdir ./vc-backend
            cd ./vc-backend
            git clone --branch feat/net8 https://github.com/VirtoCommerce/vc-docker.git
            cd .\vc-docker\linux\
        create a network for backend:
            docker network create virto
        create a dev certificate for backend ([more details](https://learn.microsoft.com/en-us/aspnet/core/security/docker-compose-https?view=aspnetcore-8.0)) .Net SDK should be installed to run commands:
            dotnet dev-certs https -ep "$env:userprofile\.aspnet\https\aspnetapp.pfx"  -p 'Password1!'
            dotnet dev-certs https --trust # this command on Windows shows the Security Warning about the certificate, need to confirm the installation
        run `docker-compose up -d`, login to the backend https://localhost:8091 (login:admin, password: store) and wait for the VirtoCommerce modules to be installed, when finished press the `restart` button. 
        If the backend container does not restart automatically, use `docker ps -a` command to get the container id and `docker start containerIdFromPreviousCommand` command to start it. 
        Wait for the backend to become up and make your choice for the `Choose sample data type` popup, choose samples installation to get the demo data to be installed. 
        The last step for the backend installation is to change the `admin` password. 
    2. The frontend part should be run locally and have a connection to the backend.
        Prerequisites for the frontend installation:
            - Enable [corepack](https://yarnpkg.com/corepack) *(run as administrator on Windows)*
                ```bash/powershell
                corepack enable
                ```
            - If you have installed `yarn` globally, uninstall it:
            - via `npm`
                ```bash/powershell
                npm uninstall --global yarn
                ```
            - or through your Operation System installation tools
                - `Control Panel`, `Chocolatey` or `Scoop` on *Windows*
                - `Launchpad`, `Finder`, `Homebrew` or `MacPorts` on *macOs*
                - Native package manager such as `apt` on *Linux*
        Clone repository:
            ```bash/powershell
            mkdir ./vc-frontend
            cd ./vc-frontend
            git clone --branch master https://github.com/VirtoCommerce/vc-theme-b2b-vue.git
            cd ./vc-theme-b2b-vue
            ```
        Check yarn version:
            ```bash/powershell
            yarn -v
            ```
            `Yarn` should be of version **4.1.0** or greater, not 1.XX.
        Install dependencies:
            ```bash/powershell
            yarn install
            ```
        Build:
        Run with hot reload for development
        - Add new **.env.local** file
        - Copy **APP_BACKEND_URL** from **.env** file and change it's value to the correct endpoint to `Virto Commerce Platform`:
            ```
            # .env.local file
            APP_BACKEND_URL=https://localhost:8091
            ```
        - Run command: `yarn dev` or `yarn dev-expose` (on windows for the first run the Security Warning about the certificate is shown, need to confirm the installation)
        - Follow the link in the terminal. 
            The first time you'll get a white page with no content, to fix this go to the backend in your browser (https://localhost:8091) and set the 'Store URL' (Stores > B2B Store > Store URL) to 'https://localhost:3000', press 'Save' and refresh a frontend page. This time the frontend will show the content.

## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

- To create docker images, you will need to copy the publish folder from the platform directory.
- If you get errors when installing VirtoCommerce modules saying that the platform version is not comparable, remove the platform image `virtocommerce/platform` marked as `latest` from local storage using `docker rmi virtocommerce/platform:latest` and run compose again to fetch fresh image.