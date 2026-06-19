# Docker

Docker is an **OS-level virtualization (containerization) platform** that allows applications to run inside **containers**. It automate the deployment, scaling, and management of applications by containers.
Containers are lightweight, portable units that bundle an application with all dependencies, libraries, and configuration files, ensuring that the application runs consistently across different computing environment.

- **Lightweight:** Containers share the host OS kernel, reducing resource usage.
- **Portable:** Containers can run on any system with Docker installed.
- **Fast Startup:** Containers start within seconds.
- **Isolation:** Each container operates independently from others.
- **Consistency:** Eliminates environment-related issues.

```
+--------------------------------------------------+
|                  Host Machine                    |
|            (Windows / Linux / macOS)             |
|                                                  |
|  +--------------------------------------------+  |
|  |              Docker Engine                 |  |
|  +--------------------------------------------+  |
|            |               |               |     |
|            v               v               v     |
|  +---------------+ +---------------+ +-------+   |
|  |  Container 1  | |  Container 2  | | Cntr3 |   |
|  |     Nginx     | |     MySQL     | |  App  |   |
|  | Application   | |  Database     | |       |   |
|  +---------------+ +---------------+ +-------+   |
|                                                  |
+--------------------------------------------------+
```

## Before Docker

Before Docker, deploying applications across different environments was challenging. Differences in operating systems, software versions, libraries, and dependencies often caused applications to work correctly on one machine but fail on another. This issue became widely known as the **"Works on My Machine"** problem.

### What is `docker-compose.yml`?

A **`docker-compose.yml`** file is a **YAML configuration file** used by **Docker Compose** to define, configure, and manage multiple Docker containers (services) in a single place.

Instead of running many `docker run` commands manually, you can describe all your containers, networks, volumes, and settings in a `docker-compose.yml` file and start everything with one command.

`docker-compose.yml` is a file that tells Docker **which containers to create and how to run them**.

Instead of typing many Docker commands one by one, you write all the settings in this file and Docker does everything automatically.

