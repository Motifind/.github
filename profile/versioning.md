## How to release api/web?

1. Push docker image with new and latest tags:
  - Update automatically by creating a new version in api or web github repositories
  - Update manually by pushing docker image from your local machine, e.g:
    - api
    ```
    docker buildx build --platform linux/amd64 -t motifind/api:1.0.7-alpha -t motifind/api:latest  . --push
    ```
    - web
    ```
    docker buildx build --platform linux/amd64 -t motifind/web:1.0.7-alpha -t motifind/web:latest  . --push 
    ```
 Note:
 - Make sure the project your creating a new docker image for builds
 - Check the current latest version of the image in dockerhub ([api](https://hub.docker.com/repository/docker/motifind/api/general), [web](https://hub.docker.com/repository/docker/motifind/web/general))
