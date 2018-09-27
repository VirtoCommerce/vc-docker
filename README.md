# VirtoCommerce Containers / Docker

This is a repository for Virto Commerce Docker images. They allow you to quickly configure fully running Virto Commerce environment including storefront and administration site. You can also use docker files to create your own custom images.

# How to use these Images

Copy [docker-compose.yml](https://github.com/VirtoCommerce/vc-docker/blob/master/windows/aspnetcore/docker-compose.yml) to your app directory. You would then be able to run the sites from the app directory.

```
$ docker-compose up -d
```

PS: make sure to run "docker-compose pull" to get the latest version of the docker images from the registry if you already ran docker before.

### Verify in the browser

Once the container starts, you'll need to finds its IP address so that you can connect to your running container from a browser. You use the docker inspect command to do that:

docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" vcdocker_vc-platform-web_1

You will see an output similar to this:

172.28.103.186

You can connect the running container using the IP address and configured port, http://172.28.103.186 in the example shown. You can also reference individual containers by HOST computer ip address using addresses below:

Admin: `http://HOST_IP_ADDRESS:8090`.

Storefront: `http://HOST_IP_ADDRESS:8080`.

You can change mapped addresses inside docker-compose.yml.

### Troubleshooting Docker Instances

To see running instances run `docker ps` 
To connect to specific instance run `docker exec -it vcdocker_vc-platform-web_1 cmd`

### Known Issues

No known issues

