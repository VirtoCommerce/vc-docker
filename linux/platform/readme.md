# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application, that allows you to quickly configure running Virto Commerce Platform v3 on a Linux environment. You can also use docker files to create your custom images.

## How to use these multi-container application

1. Execute `docker-compose up -d` to build and run containers.

## Verify in the browser

Once the container starts you can connect the running container using the localhost address and configured port, https://localhost:8090.

You can change mapped addresses inside docker-compose.yml.

## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

In docker-compose file in DB connection sting parameter *MultipleActiveResultSets* set to *False* in a reason to installing demo data. This may cause application crashes in some cases.

In Docker file used direct link to download Virto Commerce Platform V3 RC.