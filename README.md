# Developers Portal

## Development

Clone the project with the following command:

```bash
$ git clone https://github.com/Remmeauth/Documentation.git
$ cd Documentation
```

To build the project, use the following command:

```bash
$ docker build -t developers-portal . -f Dockerfile.development
```

To run the project, use the following command. It will start the server and occupate current terminal session:

```bash
$ docker run -p 8080:8080 -v $PWD:/developers-portal --name developers-portal developers-portal
```

If you need to enter the bash of the container, use the following command:

```bash
$ docker exec -it heroku-load-balancer bash
```

Clean all containers with the following command:

```bash
$ docker rm $(docker ps -a -q) -f
```

Clean all images with the following command:

```bash
$ docker rmi $(docker images -q) -f
```

## Production

To build the project, use the following command:

```bash
$ docker build -t developers-portal . -f Dockerfile.production
```

To run the project, use the following command. It will start the server and occupate current terminal session:

```bash
$ docker run -p 7979:7979 -e PORT=7979 -v $PWD:/developers-portal --name developers-portal developers-portal
```
