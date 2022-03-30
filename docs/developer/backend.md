# Backend Architecture

```yml
├── .github/
│   └── ISSUE_TEMPLATE/
├── config/    # Backend
├── docker/    # Backend
├── frontend/    # Backend
│   ├── migrations/    # Backend
│   ├── src/
│       ├── assets/
│       ├── components/
│       ├── pages/
│       └── templates/
│   ├── static/
│       └── frontend/
│   └── templates/
│       └── frontend/
├── server/    # Backend
│   └── migrations/    # Backend
└── <loose files>    # Backend
```

_<p style="text-align: center;">Overall project structure</p>_

```yml
├── config/
│   ├── <Django Project Files>
├── docker/
│   ├── django
│   └── webpack
├── frontend/
│   └── <Django App Files>
├── server/
│   ├── <Django App Files>
│   └── <RESTFramework Files>
├── .dockerignore
├── docker-compose.yml
├── manage.py
└── requirements.txt
```

_<p style="text-align: center;">Backend Architecture</p>_

## Summary

**Backend Tech Stack**: Django, DjangoRESTFramework

The backend architecture is consists the `docker/` directory, the Django `config/` project, the `frontend/` and `server/` Django apps, and a couple of Django or Docker-related loose files. In addition to serving as part of our backend, the `frontend/` directory also serves our frontend architecture. More about the `frontend/` directory as it relates our frontend architecture can be found in our guide on [Frontend Architecture](../../developer/frontend/).

## Overview of Directories and Files

- **config/:** houses the Django project files.
  - **<Django Project Files\>:** More on the files in this directory can be found in [Django's documentation](https://docs.djangoproject.com/en/4.0/).
- **docker/:** contains two dockerfiles. `django` contains information for our Django server setup. `webpack` contains information to start our webpack watch plugin.
- **<Django App\>:** currently we have two directories that are Django apps: `frontend/` and `server/`. Within these directories are the default `<Django App Files>` that are created with every app as well as `<RESTFramework Files>`.
  - **<Django App Files\>:** These files make up a Django App. To know more about these apps, read the section about [Django App Files](#django-app-files).
  - **<RESTFramework Files\>:** Currently consists of only `serializers.py`, these files are additional files that support Django via the [DjangoRestFramework library](https://www.django-rest-framework.org/).
- **.dockerignore:** This file tells Docker to ignore certain files when building the container. These are usually files that pertain to docker or git, which are not important when building the webserver.
- **docker-compose.yml:** Contains instructions for docker when we run "docker compose". To know more about what each line does, please consult [Docker's documentation](https://docs.docker.com/compose/compose-file/).
- **manage.py:** Part of Django, this is the entry point file for starting the Django server. This file handles a lot of critical settings, so be sure to read up on it in [Django's documentation](https://docs.djangoproject.com/en/4.0/ref/django-admin/).
- **requirements.txt:** A Python file that contains all dependencies for a project. It is the Python equivalent to Javascript's `package.json`.

## Docker

Docker is a platform that allows packaging and virtualizing applications within a container, giving it the powerful ability to collaborate in a stable, inter-developer environment, and deploying web applications with the greatest of ease. We will not be going too much into Docker here, but we will explain in greater depth some of the Docker configurations we have made.

### `docker-compose.yml`

This file contains configuration directions for docker compose. It consists of three services: pgdb (our database), webpack (our webpack bundler), and django (our django server). The webpack and django service relies in separate dockerfiles, located in the `docker` directory to build the container. This separation of dockerfiles enable each container to be build with its own set of dependencies. It also makes rebuilding the container simple when dependencies are migrated to a newer version.

For those of you used to creating applications without Docker, most would run webpack and django in separate terminals, so that they can both run at the same time. For the purposes of brevity, the different services can be considered to be Docker's way of running separate terminals.

One will also notice that the Django command uses a placeholder server name, 0.0.0.0:8000. This placeholder is important, since Docker creates an isolated environment. As a result, servers that are run in Docker does not recognize a browser from outside of that environment. Without this server name, localhost:8000 will not reach the server, as the server would recognize your browser as coming from a foreign machine. Therefore, all warnings related to 0.0.0.0, should they pop-up, should be ignored.

## Django App Files

```yml
├── migrations/
│   └── __init__.py
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
├── urls.py
└── views.py
```

_<p style="text-align: center;">Files generated by Django when creating a new Django app</p>_

As of right now, no specific changes have been made to these files, so please refer to [Django's documentation](https://docs.djangoproject.com/en/4.0/) for now to learn what they do in a general sense.

## Django REST Framework Files

```yml
├── serializers.py
```

_<p style="text-align: center;">RESTFramework files used to create a Django REST API</p>_

As of right now, no specific changes have been made to these files, so please refer to [DjangoRESTFramework's documentation](https://www.django-rest-framework.org/) for now to learn what they do in a general sense.

## Additional Resources

[Docker Documentation](https://docs.docker.com/)<br>
[Django 4.0 Documentation](https://docs.djangoproject.com/en/4.0/)<br>
[DjangoRestFramework Documentation](https://www.django-rest-framework.org/)<br>
