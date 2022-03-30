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
├── config.json
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

## Useful Commands

```bash
docker exec -it <container> sh   # enter into the container's shell
docker compose -f <filename> <docker command>    # used to specify an alternate docker-compose file
docker compose run <container> <command> # used to run commands inside a container, such as an npm or pip command
```
