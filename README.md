# Dockerized Superset

While trying to setting up a minimal Apache Superset instance, I've struggled quite a lot to get it up and running.

After struggling a little with virtual envs, I tried to follow the intructions for the container version, but it looks like the official instructions are not working on MacOS 10.14.4 (Mojave).

This is the cleanest and quickest way I;ve found to play with Apache Superset and explore its features.

The only pre-requisite is a working Docker installation. For help on this, take a look at:

- https://docs.docker.com/install/

**NOTE: All data is saved in a `sqlite` database that lives in the file "data/superset.db". Not the best setup for a  production environment, of course! 😅**

## First time setup

Checkout this repo and from its root run:

```bash
docker-compose run superset superset-init
```

The `latest` Docker image from https://hub.docker.com/r/amancevice/superset/ will be dowloaded automatically (~600 MB at time of writing).

You will be asked a few questions:

```text
Username [admin]:
User first name [admin]:
User last name [user]:
Email [admin@fab.org]:
Password:
Repeat for confirmation:
```

Just press the **[RETURN]** key to accept the defaul value for the first four questions, and pick a password for your admin user in the last two.

You'll get a few more messages from the init script while the database is created and setup.

To see the nice maps provided by Mapbox, put [your access token](https://account.mapbox.com/access-tokens/) in the variable `MAPBOX_API_KEY` in the file `config.py` (that will become at run time `/etc/superset/superset_config.py`).

While you are there, it would also be nice if you add some random character to the variable `SECRET_KEY`.

## Bring it up!

You are now ready to start the server. The following command will start Superset and a Redis instance to speed data retrieval via caching:

```bash
docker-compose up
```

In a few seconds the service should be reachable at:

> http://localhost:8088/

Log in with the username and password chosen in the initialisation step.

_Hurray!_ 🎊

## Not enough? Someone said PostgreSQL?

For more advanced configuration, take a look at the `examples` folder of the source repo fo the Docker image:

- https://github.com/amancevice/docker-superset/tree/master/examples

PostgreSQL, MySQL, Celery... Enjoy!
