# My Docker Cheatsheet

## Container Lifecycle
| Command | Description | Example |
|---------|-------------|---------|
| docker run | Create and start NEW container | docker run -it ubuntu:22.04 bash |
| docker exec | Run command in EXISTING container | docker exec -it NAME bash |
| ... | ... | ... |

## Useful Flags
| Flag | Meaning | When to use |
|------|---------|-------------|
| -d | Detached/background | Services like nginx, mysql |
| -it | Interactive terminal | When you need a shell |
| --rm | remove | removes container after run/exit |
| -v | volume | maps volume to directory in container |
| ... | ... | ... |

## Docker files


| Concept | Description |
|---------|-------------|
| Dockerfile | Text file with instructions to build an image |
| `FROM` | Specifies the base image |
| `RUN` | Executes a command during build |
| `COPY` | Copies files from your computer into the image |
| `.dockerignore` | Excludes files from the build context |

| Command | Purpose |
|---------|---------|
| `docker build -t name:tag .` | Build an image from a Dockerfile |
| `docker images` | List images |
| `docker history IMAGE` | Show image layers |
| `docker rmi IMAGE` | Remove an image |

## Compose Commands

| Command | What it does |
|---------|--------------|
| `docker compose up` | Start all services (foreground) |
| `docker compose up -d` | Start all services (background) |
| `docker compose down` | Stop and remove containers |
| `docker compose down -v` | Also remove volumes (careful!) |
| `docker compose ps` | List running services |
| `docker compose logs` | View all logs |
| `docker compose logs web` | View specific service logs |
| `docker compose exec web bash` | Shell into running service |