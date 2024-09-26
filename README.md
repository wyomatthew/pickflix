
# PickFlix

## Development setup

To begin development, you should begin by defining the necessary environment
variables. You can begin by cloning the template:

```bash
cp template.env .env
```

Then fill in the values. For the following commands, you should have these
environment variables exported in your shell. In bash you can do:

```bash
set -o allexport
source .env
set +o allexport
```

Now, create the necessary data directories:

```bash
mkdir -pv ${DATA_ROOT_DIR}/movies
mkdir -pv ${DATA_ROOT_DIR}/shows
mkdir -pv ${DATA_ROOT_DIR}/anime
mkdir -pv ${DATA_ROOT_DIR}/torrents
```

You can then spin up the software stack with
[docker-compose](https://docs.docker.com/compose/):

```bash
docker compose pull
docker compose up
```
