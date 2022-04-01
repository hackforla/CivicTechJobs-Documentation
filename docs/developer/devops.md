# DevOps Architecture

```yml
├── .github/
│   └── ISSUE_TEMPLATE/
├── app/
│    ├── config/
│          └── settings.py
│    ├── frontend/
│    ├── server/
│    ├── .babelrc
│    ├── manage.py
│    ├── requirements.txt
│    ├── package.json
│    ├── package-lock.json
│    └── webpack.config.js
├── dev/ # DevOps
│    ├── django.dockerfile
│    ├── webpack.dockerfile
│    └── dev.env
├── stage/ # DevOps
│    ├── django.dockerfile
│    ├── nginx.dockerfile
│    ├── stage.env
│    └── nginx.conf
├── .dockerignore # DevOps
├── .gitignore
├── jsconfig.json
├── CONTRIBUTING.md
├── docker-compose.yml # DevOps
├── docker-compose.stage.yml # DevOps
├── LICENSE
└── README.md
```

_<p style="text-align: center;">Overall project structure</p>_

```yml
├── dev/
│    ├── django.dockerfile
│    ├── webpack.dockerfile
│    └── dev.env
├── stage/
│    ├── django.dockerfile
│    ├── nginx.dockerfile
│    ├── stage.env
│    └── nginx.conf
├── .dockerignore
├── docker-compose.yml
└── docker-compose.stage.yml
```

_<p style="text-align: center;">DevOps Architecture</p>_

## Summary

**DevOps Tech Stack**: Docker, Gunicorn, Nginx, PostgreSQL

Note, some files are added to .gitignore so they are not here. In order to gain access to these files, you must have admin access to our 1password. Please ask the lead developer for such access if your issues requires access to other environments.

## Overview of Directories and Files

- **dev/:** contains two dockerfiles and an env file. `django.dockerfile` contains information for our Django server setup. `webpack.dockerfile` contains information to start our webpack watch plugin. `dev.env` is read into docker-compose.yml (below) in order to create our local dev env.
- **.dockerignore:** This file tells Docker to ignore certain files when building the container. These are usually files that pertain to docker or git, which are not important when building the webserver.
- **docker-compose.yml:** Contains instructions for docker when we run "docker compose". To know more about what each line does, please consult [Docker's documentation](https://docs.docker.com/compose/compose-file/).

## Docker

Docker is a platform that allows packaging and virtualizing applications within a container, giving it the powerful ability to collaborate in a stable, inter-developer environment, and deploying web applications with the greatest of ease. We will not be going too much into Docker here, but we will explain in greater depth some of the Docker configurations we have made.

### `docker-compose.yml`

This file contains configuration directions for docker compose. It consists of three services: pgdb (our database), webpack (our webpack bundler), and django (our django server). The webpack and django service relies in separate dockerfiles, located in the `docker` directory to build the container. This separation of dockerfiles enable each container to be build with its own set of dependencies. It also makes rebuilding the container simple when dependencies are migrated to a newer version.

For those of you used to creating applications without Docker, most would run webpack and django in separate terminals, so that they can both run at the same time. For the purposes of brevity, the different services can be considered to be Docker's way of running separate terminals.

One will also notice that the Django command uses a placeholder server name, 0.0.0.0:8000. This placeholder is important, since Docker creates an isolated environment. As a result, servers that are run in Docker does not recognize a browser from outside of that environment. Without this server name, localhost:8000 will not reach the server, as the server would recognize your browser as coming from a foreign machine. Therefore, all warnings related to 0.0.0.0, should they pop-up, should be ignored.

## Useful Commands

```bash
docker exec -it <container> sh   # enter into the container's shell
docker compose -f <filename> <docker command>    # used to specify an alternate docker-compose file
docker compose run <container> <command> # used to run commands inside a container, such as an npm or pip command
docker compose build --progress=plain # used to show more verbose output while building your image
docker compose up -d # run the container in the background
```

## Additional Resources

[Docker Documentation](https://docs.docker.com/)<br>
