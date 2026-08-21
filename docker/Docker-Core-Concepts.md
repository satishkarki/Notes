# Docker : Core Concepts

* Docker: The tool/platform that manages everything
* Image: The packaged blueprint/template for an application
* Container: an instance created from that image, usually where the application actually runs

```bash
Dockerfile
    |
    | docker build
    v
  IMAGE
    |
    | docker run
    v
 CONTAINER
 ```

## Two important principles of images
* Images are immutable. Once an image is created, it can't be modified. You can only make a new image or add changes on top of it.
* Containers are composed of layers. Each layer represents a set of file system changes that add, remove, or modify files.

```bash
                IMAGE

        ┌─────────────────┐
        │ Layer 4: app.py │
        ├─────────────────┤
        │ Layer 3: Flask  │
        ├─────────────────┤
        │ Layer 2: Python │
        ├─────────────────┤
        │ Layer 1: Ubuntu │
        └─────────────────┘
              ↑
        all read-only
        all immutable


docker run
     ↓


             CONTAINER

        ┌─────────────────┐
        │ Writable layer  │ ← container changes
        ├─────────────────┤
        │ Layer 4         │
        ├─────────────────┤
        │ Layer 3         │
        ├─────────────────┤
        │ Layer 2         │
        ├─────────────────┤
        │ Layer 1         │
        └─────────────────┘
```
> Docker doesn't edit an existing image. It builds new filesystem changes as layers, while containers get their own writable layer on top of the image.

## Registry 
An image registry is a place where Docker images are stored and distributed.

Think of it like an app store for Docker images.
[Docker Hub](https://hub.docker.com/) is a public registry that anyone can use and is the default registry.



> Note : A registry is a centralized location that stores and manages container images, whereas a repository is a collection of related container images within a registry. 

```bash
Docker Hub                ← Registry

nginx                     ← Repository
├── nginx:1.27
├── nginx:1.28
└── nginx:latest

redis                     ← Repository
├── redis:7
├── redis:8
└── redis:latest
```

## Docker Compose

`Dockerfile` describes how to build an image and `compose.yaml` describes how to run one or more containers together.
```bash
Dockerfile
    |
    | docker build
    v
  IMAGE
    |
    |
    +-------------------+
                        |
                  compose.yaml
                        |
                        | docker compose up
                        v
                 CONTAINER(S)
```
Conceptually :

```bash
docker compose up -d --build
```

```bash
Dockerfile
    |
    | --build
    v
new/rebuilt image
    |
    | up
    v
container
    |
    | -d
    v
runs in background
```
# Docker Workshop

I am following the [Docker Workshop](https://docs.docker.com/get-started/workshop/) guide.


## Part 1: Containerize an application
### A. Clone the repo
```bash
git clone https://github.com/docker/getting-started-app.git
```

### B. Creating the dockerfile
```dockerfile
# syntax=docker/dockerfile:1

FROM node:24-alpine
WORKDIR /app
COPY . .
RUN npm install --omit=dev
CMD ["node", "src/index.js"]
EXPOSE 3000
```
This Dockerfile does the following:

* Uses node:24-alpine as the base image, a lightweight Linux image with Node.js pre-installed
* Sets /app as the working directory
* Copies source code into the image
* Installs the necessary dependencies
* Specifies the command to start the application
* Documents that the app listens on port 3000

```bash
Your final image
┌───────────────────────┐
│ Your application      │
├───────────────────────┤
│ npm dependencies      │
├───────────────────────┤
│ Node.js               │
├───────────────────────┤
│ Alpine Linux          │
└───────────────────────┘
```

### C. Build the image
```bash
docker build -t getting-started .
```
```bash
docker build -t getting-started .
│      │     │        │         │
│      │     │        │         └─ build context: current directory
│      │     │        └───────── image name
│      │     └────────────────── tag/name option
│      └──────────────────────── build an image
└─────────────────────────────── Docker CLI
```

### D. Start an app container
```bash
docker run -d -p 127.0.0.1:3000:3000 getting-started
```
```bash
docker run -d -p 127.0.0.1:3000:3000 getting-started
│      │   │  │         │    │       │
│      │   │  │         │    │       └─ image
│      │   │  │         │    └──────── container port
│      │   │  │         └───────────── host port
│      │   │  └─────────────────────── host IP
│      │   └────────────────────────── publish a port
│      └────────────────────────────── detached/background
└───────────────────────────────────── Docker
```
## Part 2 : Update the application
