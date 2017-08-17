# VirtoCommerce Windows Container / Docker

This is a repository for Virto Commerce Docker images. They allow you to quickly configure fully running Virto Commerce envirnment including storefront and administration site. You can also use dockerfiles to create your own custom images.

# How to use these Images

Copy `docker-compose.yml` to your app directory. You would then be able to run the sites from the app directory.

```
$ docker-compose up -d
```

### Verify in the browser

Once the container starts, you'll need to finds its IP address so that you can connect to your running container from a browser. You use the docker inspect command to do that:

docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" docker_vc-platform-web_1

You will see an output similar to this:

172.28.103.186

You can connect the running container using the IP address and configured port, http://172.28.103.186:8090 in the example shown.


Admin: `http://IP_ADDRESS:8090`.

Storefront: `http://IP_ADDRESS:8080`.

You can change mapped addresses inside docker-compose.yml.

### Known Issues

No known issues

