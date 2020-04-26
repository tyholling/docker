ubuntu-xrdp-lxde
==

Usage:
```
docker build --tag ubuntu-xrdp-lxde .
docker run -d -p 53389:3389 ubuntu-xrdp-lxde
```
Once the container is running, connect Remote Desktop to localhost:53389.
