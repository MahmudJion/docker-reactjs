# docker-reactjs
dockerize react and nextjs application

## React Application

Build and tag the Docker image:

```sh
$ docker build -t sample:dev .
```

Then, spin up the container once the build is done:

```sh
$ docker run \
    -it \
    --rm \
    -v ${PWD}:/app \
    -v /app/node_modules \
    -p 3001:3000 \
    -e CHOKIDAR_USEPOLLING=true \
    sample:dev
```

Build with Docker Compose image and fire up the container:

```sh
$ docker-compose up -d --build
```

Ensure the app is running in the browser and test hot-reloading again. Bring down the container before moving on:

```sh
$ docker-compose stop
```

### Production

Using the production Dockerfile, build and tag the Docker image:

```sh
$ docker build -f Dockerfile.prod -t sample:prod .
```

Spin up the container:

```sh
$ docker run -it --rm -p 1337:80 sample:prod
```

Navigate to http://localhost:1337/ in your browser to view the app.

Fire up the container with docker-compose.prod.yml:

```sh
$ docker-compose -f docker-compose.prod.yml up -d --build
```


## NextJS Application

### Building your Docker image
You are all set up to build your Docker image, we’ll call it “client”. You can do so with the following command:

```sh
docker build -t client .
```

### Deploying your Docker container
Consider now that you want to browse the pages build in your container, for this you’ll need to run the container built and then bind a port from your container to your local environment.

```sh
docker build -t client . && docker run --name CLIENT_CONTAINER -p 0.0.0.0:5000:3000 client
```