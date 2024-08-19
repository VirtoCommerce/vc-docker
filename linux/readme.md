# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application that allows you to quickly configure Virto Commerce v3 to run in a Linux or Windows environment. 
You can also use docker files to create your own images (check the issues section below before creating images).

Before proceeding with the setup process, please ensure that you have the required software installed on your system:

- [git](https://git-scm.com/downloads)
  
- [docker](https://docs.docker.com/engine/install/)
  
- [Node.js v20](https://nodejs.org/en/download/) (**20.11.0** or later)
  
- [.Net SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)

## How to use this multi-container application
1. Run the backend part:
   
    - clone `vc-docker` repository:
  
        open bash/powershell terminal at the root level of your project (the default is user's home directory)

        `mkdir ./vc-backend`

        `cd ./vc-backend`

        <!-- `git clone --branch feat/net8 https://github.com/VirtoCommerce/vc-docker.git` -->

        `git clone --branch VCST-1654 https://github.com/VirtoCommerce/vc-docker.git`

        `cd ./vc-docker/linux/`

    - create a network for the backend:

        `docker network create virto` *may require root privileges on Linux*

    - create a dev certificate for the backend ([more details](https://learn.microsoft.com/en-us/aspnet/core/security/docker-compose-https?view=aspnetcore-8.0)) 
    
        .Net SDK should be installed to run commands:

        *for Windows:*

        `dotnet dev-certs https -ep "$env:userprofile\.aspnet\https\aspnetapp.pfx" -p 'Password1!'` 

        `dotnet dev-certs https --trust` # *on Windows will show security warning about certificate, need to confirm installation*

        *for Linux:*

        `dotnet dev-certs https` 

        `sudo -E dotnet dev-certs https -ep ${HOME}/.aspnet/https/aspnetapp.pfx -p 'Password1!' --format PFX` 

        `sudo openssl pkcs12 -in ${HOME}/.aspnet/https/aspnetapp.pfx -clcerts -nokeys -out /usr/local/share/ca-certificates/aspnetapp.crt -password pass:Password1!`
        <!-- `sudo cp ${HOME}/.aspnet/https/aspnetapp.pfx /usr/local/share/ca-certificates/aspnetapp.crt` -->

        `sudo update-ca-certificates`

        edit the `docker-compose.yml` file string #49 to replace *~/vc-backend/cms-content-volume:/opt/virtocommerce/platform/wwwroot/cms-content* with *%HOMEDIRECTORY%/vc-backend/cms-content-volume:/opt/virtocommerce/platform/wwwroot/cms-content* *replace %HOMEDIRECTORY% placeholder with the user's home directory(can be found using `echo ${HOME}' command - e.g. /home/user)*

        edit the `docker-compose.yml` file string #50 to replace *~/vc-backend/modules-volume:/opt/virtocommerce/platform/modules* with *%HOMEDIRECTORY%/vc-backend/modules-volume:/opt/virtocommerce/platform/modules* *replace %HOMEDIRECTORY% placeholder with the user's home directory(can be found using `echo ${HOME}' command - e.g. /home/user)*

        edit the `docker-compose.yml` file string #51 to replace *~/.aspnet/https:/https:ro* with *%HOMEDIRECTORY%/.aspnet/https:/https:ro* *replace %HOMEDIRECTORY% placeholder with the user's home directory(can be found using `echo ${HOME}' command - e.g. /home/user)*

    - run `docker-compose up -d` *on Linux you may need root privileges;* *on Windows you will see the `Docker Desktop - Filesharing` and `Windows Firewall allow communication` dialogs - accept both*
     
    - login to the backend https://localhost:8091 (login:admin, password: store) and wait for the VirtoCommerce modules to be installed, when finished press the Restart button.
    If the backend container does not restart automatically, use the `docker ps -a` command to get the container id and the `docker start containerIdFromPreviousCommand` command to start it. 
    Wait for the backend to start and make your choice for the `Choose sample data type` popup, choose samples installation to get the demo data to install. 
    - the last step for the backend installation is to change the `admin` password. 

    > *The frontend part should be run locally and have a connection to the backend.*
    > 
    > Prerequisites for the frontend installation:
    > 
    >    - enable [corepack](https://yarnpkg.com/corepack) *(run as administrator on Windows)*
    > 
    >        `corepack enable`
    > 
    >    - if you have installed yarn globally, uninstall it:
    > 
    >    - via npm
    > 
    >        `npm uninstall --global yarn`

2. Run the frontend part:
   
   - open bash/powershell terminal at the root level of your project (the default is user's home directory)
  
   - clone a repository:
     
       `mkdir ./vc-frontend`

       `cd ./vc-frontend`

       `git clone --branch master https://github.com/VirtoCommerce/vc-theme-b2b-vue.git`

       `cd ./vc-theme-b2b-vue`

   - check yarn version:
  
      `yarn -v` *Yarn should be of version **4.1.0** or greater, not 1.XX. Confirm to allow download of the yarn.js script if requested*

   - install the dependencies:
  
      `yarn install`

   - copy the frontend config file:
  
      `cp ./.env ./.env.local`

   - set the correct backend url in the `.env.local` file
  
      APP_BACKEND_URL=https://localhost:8091

   - start the frontend application: 
  
      `yarn dev` *on Windows a security warning will appear about installing a certificate - accept it*

   - go to the backend in your browser (https://localhost:8091) and set the 'Store URL' (Stores > B2B Store > Store URL) to 'https://localhost:3000', press 'Save'
  
   - open the frontend 'https://localhost:3000' page in your browser
  
## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

To create Docker images, you must copy the publish folder from the platform directory.
  
If you get errors when installing VirtoCommerce modules saying that the platform version is not comparable, remove the platform image `virtocommerce/platform` marked as `latest` from local storage using `docker rmi virtocommerce/platform:latest` and run compose again to get a fresh image.


## How to install a custom module

Suppose you've set up the solution as described above, and you need to use a module that is not automatically installed from a bundle, or to use a different version of an installed module.

To add/remove/replace a module while the solution is running, use the following steps:

*as an example we need to replace the ApplicationInsights module from the installed version to 3.800.0* 

### *on Linux:*

*run the shell as root to eliminate access restrictions on docker files `sudo -s`*

1. go to the backend interface and note the current version of the ApplicationInsights module (Home > More > Modules).

2. go to the modules-data directory and remove the files of the current version of the module:

   `cd %HOMEDIRECTORY%/vc-backend/modules-volume/VirtoCommerce.ApplicationInsights` *replace the %HOMEDIRECTORY% placeholder with the user's home directory (can be found using the `echo ${HOME}' command - e.g. /home/user)*`

   `rm -r *`

3. download the required version and extract it to the module:

   `curl -LO "https://github.com/VirtoCommerce/vc-module-app-insights/releases/download/3.800.0/VirtoCommerce.ApplicationInsights_3.800.0.zip"`

   `unzip ./VirtoCommerce.ApplicationInsights_3.800.0.zip` *if your system doesn't have unzip run `apt install unzip` to install it*
   *if the module files are not available via http, just copy the needed files the appropriate local directory and move to the next step*

4. clean up the `app_data/modules` directory in the running platform container:

   `docker ps -a` and copy a container ID for the platform

   `docker exec %CONTAINERID% rm -r app_data/modules` replace the %CONTAINERID% placeholder with the platform container ID

   `docker restart %CONTAINERID%` replace the %CONTAINERID% placeholder with the platform container ID

5. Go to the backend interface and ensure that the current version of the ApplicationInsights module is now 3.800.0 (Home > More > Modules).

### *on Windows running Docker Desktop in WSL mode:*

1. go to the backend interface and note the current version of the ApplicationInsights module (Home > More > Modules).

2. open a bash/powershell terminal at the root level of your project (the default is the user's home directory)

3. go to the modules-data directory and remove the files of the current version of the module:

   `cd ./vc-backend/modules-volume/VirtoCommerce.ApplicationInsights`

   `rm -r *`

4. download the required version and extract it to the module:

   `Invoke-WebRequest -Uri "https://github.com/VirtoCommerce/vc-module-app-insights/releases/download/3.800.0/VirtoCommerce.ApplicationInsights_3.800.0.zip" -OutFile "VirtoCommerce.ApplicationInsights_3.800.0.zip"`

   `Expand-Archive -Path "./VirtoCommerce.ApplicationInsights_3.800.0.zip" -DestinationPath "./"`

   *if the module files are not available via http, simply copy the required files to the appropriate local directory and proceed to the next step.*

5. clean up the `app_data/modules` directory in the running platform container:

   `docker ps -a` and copy a container ID for the platform

   `docker exec %CONTAINERID% rm -r app_data/modules` replace the %CONTAINERID% placeholder with the platform container ID

   `docker restart %CONTAINERID%` replace the %CONTAINERID% placeholder with the platform container ID

6. Go to the backend interface and ensure that the current version of the ApplicationInsights module is now 3.800.0 (Home > More > Modules).