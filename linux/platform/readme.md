# VirtoCommerce Platform v3 Linux Container

This is a multi-container Docker application, that allows you to quickly configure running Virto Commerce Platform v3 on a Linux environment. You can also use docker files to create your custom images.

## How to use these multi-container application

Virto Commerce Platform v3 uses HTTPS by default. HTTPS relies on certificates for trust, identity, and encryption.
This document describes how to use [self-signed development certificates](https://en.wikipedia.org/wiki/Self-signed_certificate) for hosting Virto Commerce Platform v3 image over localhost in Docker Desktop for Windows for Linux containers.

1. Create local folder `{your_local_folder}` for Docker files.
2. Download and extract repository.zip to created folder.
3. Generate certificate and configure local machine:

```cmd
dotnet dev-certs https -ep {your_local_folder}\vc-docker\linux\platform\https\virto.pfx -p {your_password}
dotnet dev-certs https --trust
```

Replace `{your_password}` with a password.

4. Navigate to `{your_local_folder}`\vc-docker\linux\platform and open **.env** file in text editor.
5. In **DOCKER_PLATFORM_CERT_PASS={your_password}** replace `{your_password}` with a password and save changes.
6. Execute `docker-compose up -d` to build and run containers.

## Verify in the browser

Once the container starts you can connect the running container using the localhost address and configured port, https://localhost:8091.

You can change mapped addresses inside docker-compose.yml.

## Troubleshooting Docker Instances

To see running instances run `docker ps`

To connect to specific instance run `docker exec -it platform_vc-platform-web_1 bash`

## Known Issues

In docker-compose file in DB connection sting parameter *MultipleActiveResultSets* set to *False* in a reason to installing demo data. This may cause application crashes in some cases.

In Docker file used direct link to download Virto Commerce Platform V3 RC.