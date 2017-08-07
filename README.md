# VirtoCommerce Windows Container / Docker

This is a repository for Virto Commerce Docker images. They allow you to quickly configure fully running Virto Commerce envirnment including storefront and administration site. You can also use dockerfiles to create your own custom images.

# How to use these Images

Copy `docker-compose.yml` to your app directory. You would then be able to run the sites from the app directory.

```
$ docker-compose up -d
```

### Verify in the browser

Once the container starts, you'll need to finds your computer IP address so that you can connect to your running container from a browser. You use the `ipconfig` command to do that:

`ipconfig`

You will see an output similar to this:

```
Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : attlocal.net
   IPv6 Address. . . . . . . . . . . : 2605:304:ce8c:8c23:3119:24e1:13e2:a1de
   Temporary IPv6 Address. . . . . . : 2604:304:ce8c:8c23:24a9:9s71:9779:4325
   Link-local IPv6 Address . . . . . : fe82::3248:23e1:12e1:a4de%10
   IPv4 Address. . . . . . . . . . . : 192.168.1.101
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
```

Admin: `http://IP_ADDRESS:8090`.

Storefront: `http://IP_ADDRESS:8080`.

You can change mapped addresses inside docker-compose.yml.

### Known Issues

The following issues will require some changes to source repositories and will be addressed shortly.

1. Storefront needs to be manually added under "storefront/source" in order to be able to build storefront docker image.
2. Images are not correctly referenced in admin.
