# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application that allows you to quickly configure running Virto Commerce v3 on a Linux environment. You can also use docker files to create your custom images (check the issues section below before creating images).

Build images:
```cmd
docker build -t virtocommerce/platform:v3 .
```


## How to use these multi-container applications

1. Execute `docker-compose up -d` to build and run containers.

## Verify in the browser

Once the container starts, you can connect to the running container using the localhost address and the configured port:

- Platform (Admin) - http://localhost:8090 (login:admin, password: store)

You can change mapped addresses inside docker-compose.yml.

## Troubleshooting Docker Instances

* To see running instances, run `docker ps`
* To connect to a specific instance, run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues
