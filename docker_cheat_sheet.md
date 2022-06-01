# Docker guide

## Images

### Build an image

```bash
# Build image based on Dockerfile (current folder)
$ docker build .

# Give a name to the image
$ docker build -t [NAME] .
```

### Handle local images

```bash
# List all the downloaded and built images
$ docker image list     # or docker image ls

# Remove an image
$ docker image rm [IMG_ID]
```

## Containers

### Run a container

```bash
# Run a local image inside a container
$ docker run [IMG_NAME]

# Run a container in detach mode and give it a name
$ docker run -d --name node-app [IMG_NAME]

# Port mapping to redirect traffic to the container
$ docker run -p [LOC_PORT]:[CONT_PORT] [IMG_NAME]
```

### Containers status

```bash
# Show the currently running containers
$ docker ps
```

### Stop / Delete a running container

```bash
# Delete a running container
# -f = force, no need to stop the container to delete it
$ docker rm [CONT_NAME] -f
```

### Interact with a container

```bash
# Exec a command inside the container
$ docker exec -it [CONT_NAME] [CMD]

# Ex: open a bash shell
$ docker exec -it [CONT_NAME] bash

# Exit the container
$ exit # or (CTRL-D)
```

## Volumes

- Allow us to have persistent data in our containers
- **Bind mount volume**

  - syncs a folder of the local machine to a folder within the container
  - you'll also need to restart the process in order to visualize the updates when you change your code (ex: nodemon for node)
    \
     &nbsp;

  ```bash
  # Insert the FULL local path
  $ docker run -d -v [LOC_PATH]:[CONT_PATH] [IMG_NAME]

  # You can also use system variables
  $ docker run -d -v $(pwd):[CONT_PATH] [IMG_NAME]

  # Read-only bind mount (container can't create/modify local files)
  $ docker run -d -v $(pwd):[CONT_PATH]:ro [IMG_NAME]
  ```

- **Anonymous volume**
  - we can use it to prevent the bind mount volume to override/delete some folders inside the container
    \
     &nbsp;
  ```bash
  # Ex: Preserve the node_modules folder when deleting the local one
  $ docker run -d -v [LOC_PATH]:[CONT_PATH] -v [CONT_PATH]/node_modules [IMG_NAME]
  ```

## Environment variables

## Node stuff

- Automatically restart the node process when we change our source code
  ```bash
  # Install nodemon module
  $ npm install nodemon --save-dev
  ```

## Troubleshooting

### Logs

```bash
# Print the docker logs for a container
$ docker logs [CONT_NAME]
```
