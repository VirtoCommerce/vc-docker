# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application that allows you to quickly configure Virto Commerce v3 to run in a Linux or Windows environment. 
You can also use docker files to create your custom images (check issues section below before creating images).

Before stating the setup process ensure that your system have needed software installed:
    [git](https://git-scm.com/downloads)
    [docker](https://docs.docker.com/engine/install/)
    [Node.js v20](https://nodejs.org/en/download/) (**20.11.0** or later)
    [.Net SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)

## How to use these multi-container application
Run the backend part:
    - clone `vc-docker` repository:
        open bash/powershell terminal at the root level of your project (the default is user's home directory)
        mkdir ./vc-backend
        cd ./vc-backend
        <!-- git clone --branch feat/net8 https://github.com/VirtoCommerce/vc-docker.git -->
        git clone --branch VCST-1654 https://github.com/VirtoCommerce/vc-docker.git
        cd .\vc-docker\linux\
    - create a network for backend:
        docker network create virto
    - create a dev certificate for backend ([more details](https://learn.microsoft.com/en-us/aspnet/core/security/docker-compose-https?view=aspnetcore-8.0)) .Net SDK should be installed to run commands:
        dotnet dev-certs https -ep "$env:userprofile\.aspnet\https\aspnetapp.pfx"  -p 'Password1!'
        dotnet dev-certs https --trust # this command on Windows shows the Security Warning about the certificate, need to confirm the installation
    - run `docker-compose up -d`, login to the backend https://localhost:8091 (login:admin, password: store) and wait for the VirtoCommerce modules to be installed, when finished press the `restart` button. 
    If the backend container does not restart automatically, use `docker ps -a` command to get the container id and `docker start containerIdFromPreviousCommand` command to start it. 
    Wait for the backend to become up and make your choice for the `Choose sample data type` popup, choose samples installation to get the demo data to be installed. 
    The last step for the backend installation is to change the `admin` password. 
Run the backend part:
The frontend part should be run locally and have a connection to the backend.
    Prerequisites for the frontend installation:
        - enable [corepack](https://yarnpkg.com/corepack) *(run as administrator on Windows)*
            corepack enable
        - if you have installed `yarn` globally, uninstall it:
        - via `npm`
            npm uninstall --global yarn
        - or through your Operation System installation tools
            - `Control Panel`, `Chocolatey` or `Scoop` on *Windows*
            - `Launchpad`, `Finder`, `Homebrew` or `MacPorts` on *macOs*
            - Native package manager such as `apt` on *Linux*
    Actions to do in sequense:
        - open bash/powershell terminal at the root level of your project (the default is user's home directory)
        - clone a repository:
            mkdir ./vc-frontend
            cd ./vc-frontend
            git clone --branch master https://github.com/VirtoCommerce/vc-theme-b2b-vue.git
            cd ./vc-theme-b2b-vue
        - check yarn version:
            yarn -v
            `Yarn` should be of version **4.1.0** or greater, not 1.XX.
        - install dependencies:
            yarn install
        - copy frontend config file:
            cp ./.env ./.env.local
        - set the correct backend url in `.env.local` file
            APP_BACKEND_URL=https://localhost:8091
        - run command: `yarn dev`
        - go to the backend in your browser (https://localhost:8091) and set the 'Store URL' (Stores > B2B Store > Store URL) to 'https://localhost:3000', press 'Save'
        - open the frontend 'https://localhost:3000' page in browser
## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

- To create docker images, you will need to copy the publish folder from the platform directory.
- If you get errors when installing VirtoCommerce modules saying that the platform version is not comparable, remove the platform image `virtocommerce/platform` marked as `latest` from local storage using `docker rmi virtocommerce/platform:latest` and run compose again to fetch fresh image.