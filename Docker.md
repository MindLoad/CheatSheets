---
Title: Docker
Date: 2024-09-09 00:30
tags:
  - cheatsheet
  - docker
---
### Ctop
> [!example]- Run ctop as docker container
> ```bash
> docker run --rm -ti --name=ctop --volume /var/run/docker.sock:/var/run/docker.sock:ro quay.io/vektorlab/ctop:latest


