# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application, that allows you to quickly configure running Virto Commerce v3 on a Linux environment. You can also use docker files to create your custom images (check issues section below before creating images).

## How to use these multi-container application

1. Execute `docker-compose up -d` to build and run containers.

## Verify in the browser

Once the container starts you can connect the running container using the localhost address and configured port:

Platform (Admin) - http://localhost:8090 (login:admin, password: store)
Strofront - http://localhost:8080

You can change mapped addresses inside docker-compose.yml.

## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

- In order to build docker images you must copy publish folder from platform and storefront under "publish" directory.
- Make sure to comment out all credentials (like AppId) in appsettings for storefront, otherwise storefront won't be able to connect to platform
- Make sure to install storefront theme manually as it is currently not included in the demo data set
