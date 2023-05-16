## How to release api/web?

### 1. Push docker image with new and latest tags:
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

### 2. Pull new images on google cloud motifind vm instance:
1. Go to [google cloud console](https://console.cloud.google.com/)
2. Make sure you're logged in to the right account
<img width="1411" alt="Screenshot 2023-05-16 at 23 27 54" src="https://github.com/Motifind/.github/assets/42270585/170f70db-0edb-4861-986e-7a2881830854">

3. Open vm instances page
<img width="1372" alt="Screenshot 2023-05-16 at 23 29 35" src="https://github.com/Motifind/.github/assets/42270585/f62ed360-02d1-45a9-9a20-da6ae422d173">

4. Connect to motifind vm instance shell
<img width="519" alt="Screenshot 2023-05-16 at 23 32 00" src="https://github.com/Motifind/.github/assets/42270585/79d0ab2d-b3c5-4395-ba28-aa720f65f790">

5. Go to edas_lakavicius user directory
```
cd ../edas_lakavicius
```
6. Stop running containers and remove the volumes (**this step turns down everything currently running in production**)
```
docker-compose --profile all down -v
```
7. Remove the image of service you want to update
- api:
```
docker rmi motifind/api
```
- web:
```
docker rmi motifind/web
```
8. Run docker compose
```
docker-compose --profile all up --build -d
```
