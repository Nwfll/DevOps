# DevOps

1-1 For which reason is it better to run the container with a flag -e to give the environment variables rather than put them directly in the Dockerfile?
Because of cyber-security purpose

1-2 Why do we need a volume to be attached to our postgres container?
We need a volume to persist PostgreSQL data outside the container lifecycle.
Without a volume, all data would be lost when the container stops or is removed.

1-3 Document your database container essentials: commands and Dockerfile.
docker build -t
docker run --rm -d --name pg_container --network app-network -e POSTGRES_DB=db -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd -p 5432:5432   ba50e227fef6
docker run -p "8080:8080" --net=app-network --name=adminer -d adminer

1-4 Why do we need a multistage build? And explain each step of this dockerfile.
We need a multistage build to separate the build environment (which may be heavy) from the runtime environment (which should be lightweight), reducing the final image size and improving security.  

1-5 Why do we need a reverse proxy?
We need a reverse proxy to forward client requests to a backend application while hiding the backend's details.
It also allows us to add features like load balancing, SSL, or static content delivery without modifying the backend.

1-6 Why is docker-compose so important?
Docker Compose allows you to manage multi-container applications easily by defining all services in one file.
It simplifies starting, stopping, building, and networking containers together with a single command.

1-7 Document docker-compose most important commands.
docker compose up --build → Builds and starts all services.
docker compose down → Stops and removes all services, networks, and volumes.
docker compose ps → Lists running services.
docker compose logs -f → Streams logs from all services.
docker compose exec <service> <cmd> → Runs a command in a running container.

1-8 Document your docker-compose file.
backend service builds the Python app and connects to the database.
database service uses a PostgreSQL image with environment variables for DB setup.
httpd service builds the Apache server, serving static files and acting as a reverse proxy.
All services share the same custom network app-network.

1-9 Document your publication commands and published images in Docker Hub
docker login → Logs into Docker Hub.
docker tag my-image Nawfel/my-image:tag → Tags the image with my Docker Hub repo name.
docker push Nawfel/my-image:tag → Pushes the image to Docker Hub.

1-10 Why do we put our images into an online repo?
We store images in an online repository like Docker Hub to make them accessible from anywhere.
It allows easy sharing, deployment, and collaboration across environments and teams.

2-1 What are testcontainers?
Testcontainers are a Java (and other languages) library that provides lightweight, throwaway Docker containers for automated tests

2-2 For what purpose do we need to use secured variables ?
Secured variables (or secrets) are used to store sensitive information like passwords, API keys, or tokens without exposing them in the code.
They help prevent credential leaks and ensure safer automated workflows in CI/CD pipelines.

2-3 Why did we put needs: build-and-test-backend on this job? Maybe try without this and you will see!
We use needs: build-and-test-backend to ensure the Docker image is only built if the backend compiles and tests pass.
Without it, the image could be built and pushed even if the application is broken.

2-4 For what purpose do we need to push docker images?
Pushing Docker images makes them available remotely for deployment or sharing across environments.
It ensures consistent builds and allows others (or servers) to pull and run the exact same version of the app.

The link of my other repo github: https://github.com/Nwfll/tp-devops-1-docker





