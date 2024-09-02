# Creating a Custom Docker Image

This README.md file covers the following:

1. Writing the Dockerfile

2. Defining the base image

3. Installing packages

4. Defining the start command

5. Building the Docker image

6. Running the Docker container

7. Accessing the Apache2 web server

## Steps

### 1. Writing the Dockerfile

1. Create a new file named `Dockerfile` using the text editor of your choice (e.g., `vim Dockerfile`).

### 2. Defining the Base Image

The first instruction in the Dockerfile is the `FROM` command, which specifies the base image to use. In this case, we're using the latest Ubuntu image.

### 3. Installing Packages

Next, we'll update the package list and install the Apache2 web server.

This command updates the package list and installs the Apache2 package.

> **Note:** By default, the Dockerfile runs commands as the root user. If you need to secure the image or run commands with limited permissions, you should create a new user, add them to the necessary groups, and adjust permissions accordingly.

### 4. Defining the Start Command

To ensure the container remains active after starting, we need to add the `CMD` instruction to run the Apache2 server in the foreground.
```
FROM ubuntu
RUN apt update && apt install -y apache2
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

This command starts the Apache2 server and keeps the container running.

### 5. Building the Docker Image

To build the Docker image, run the following command in the same directory as the `Dockerfile`:
```
docker build --tag ubuntu-apache2:v1 .
```

This command builds the Docker image and tags it as `ubuntu-apache2:v1`.

### 6. Running the Docker Container

Start the Docker container using the following command:
```
docker run --name ubuntu-test -d -p 8080:80 ubuntu-apache2:v1
```

This command:
- Creates a new container named `ubuntu-test`
- Runs the container in detached mode (`-d`)
- Maps port 8080 on the host machine to port 80 inside the container (`-p 8080:80`)
- Uses the `ubuntu-apache2:v1` image to create the container

### 7. Accessing the Apache2 Web Server

After running the container, you can access the Apache2 web server by opening a web browser and navigating to `http://localhost:8080`. You should see the default Apache2 welcome page, indicating that the server is running correctly inside the Docker container.

## Conclusion

This guide covered the process of creating a custom Docker image with the Apache2 web server. By using a Dockerfile, you can automate the creation of Docker images and ensure consistent deployment of your applications.
