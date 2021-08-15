The Kubernetes services provide the ability to automate the processes of controlling and managing the operation of containerised applications. The following guide is an example of creating and deploying an application image with the use of the Kubernetes ecosystem. Before we start, note the following:
You need to have Docker downloaded and installed on your desktop (for this, see [Get started with Docker](https://www.docker.com/get-started)). 
As an example of an application for creating and deploying the image, we are using the ``application.py`` file that is put into one of the subdirectories.
For launching the application image with the Kubernetes cluster, we are using the ExampleApp that accepts requests on port 8800.

To create and deploy the application image, follow the steps below:

1. Create the quickstart_docker directory and its subdirectories using the ``mkdir`` command.
```

mkdir quickstart_docker #the directory of the whole project
mkdir quickstart_docker/application #the subdirectory for keeping the application code 
mkdir quickstart_docker/docker #the subdirectory for keeping the Docker tools
mkdir quickstart_docker/docker/application #the subdirectory for keeping the Dockerfile
```

2. Locate the ``application.py`` file in the ``quickstart_docker/application`` subdirectory.

```
import http.server
import socketserver

PORT = 8000

Handler = http.server.SimpleHTTPRequestHandler

httpd = socketserver.TCPServer(("", PORT), Handler)

print("serving at port", PORT)
httpd.serve_forever()
```
3. Locate the ``Dockerfile`` in the ``quickstart_docker/docker/application`` subdirectory with the following Docker instructions:
```
FROM python:3.5 #Use base image from the registry

WORKDIR /app #Set the working directory to /app

COPY ./application /app #Copy the 'application' directory contents into the container at /app

EXPOSE 8000 #Make port 8000 available to the world outside this container

CMD ["python", "/app/application.py"] #Execute 'python /app/application.py' when container launches
```
4. In the terminal, use the ``docker build . -f-docker/application/Dockerfile -t exampleapp`` command to get the instructions executed. The command line consists of the following parts:

``.``  - working directory which is the context of the build;


`` -f docker/application/Dockerfile`` - flagged Dockerfile;


``-t exampleapp`` - tagged image (tagging allows identifying images later in the repository).


5. Use the ``$ docker images`` command to view the existing images:
```
$ docker images
REPOSITORY             TAG             IMAGE ID            CREATED             SIZE
exampleapp             latest          83wse0edc28a        2 seconds ago       153MB
python                 3.6             05sob8636w3f        6 weeks ago         153MB
```
6. The images now can be shared across repositories.

