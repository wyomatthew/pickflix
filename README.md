
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
docker compose up -d
```

Now, you should be able to access all the services detailed below:

### Jellyfin

Accessed at <https://streaming.localhost>

You will be prompted to setup the instance on first accessing it, including
creating credentials and setting up the media libraries. To mirror the pickflix
production instance, you should setup three libraries as such:

- Movies (Folder `/data/movies`)
- Shows (Folder `/data/shows`)
- Anime (Folder `/data/anime`)

### Jellyseerr

Accessed at <https://requests.localhost>

You will be prompted to setup the instance on first access. You should opt to
sign in via "Use your Jellyfin account" with the following details:

Jellyfin URL: `http://vpn:8096`
Email Address: `<your email>`
Username: `<username created in Jellyfin>`
Password: `<password created in Jellyfin>`

You can add the Radarr/Sonarr integrations here as well if you already have them
setup, otherwise simply continue without and return to integrate them later.

### Radarr

Accessed at <https://localhost/radarr>

You will be prompted to setup the instance on first access. Feel free to use
any credentials that ✨spark joy✨.

You can setup the integration with qBittorrent by going to Settings > Download
Clients and adding an integration with qBittorrent with the following settings:

Host: `localhost`
Port: `8080`
Username: `admin`
Password: `admin`

For Radarr to properly commmunicate with Jellyfin, you need to configure the
media root folder to point to the shared volume. Go to Settings > Media
Management and add the movie volume to "Root Folders", by default
`/data/movies`.

To improve the releases grabbed by Radarr, it is recommended to reconfigure
your quality profile. A detailed setup is provided by this guide:
<https://trash-guides.info/Radarr/radarr-setup-quality-profiles/>

### Sonarr

Accessed at <https://localhost/sonarr>

You will be prompted to setup the instance on first access. Feel free to use
any credentials that ✨spark joy✨.

You can setup the integration with qBittorrent by going to Settings > Download
Clients and adding an integration with qBittorrent with the following settings:

Host: `localhost`
Port: `8080`
Username: `admin`
Password: `admin`

For Sonarr to properly commmunicate with Jellyfin, you need to configure the
media root folders to point to the shared volumes. Go to Settings > Media
Management and add the shows/anime volumes to "Root Folders", by default
`/data/shows` and `/data/anime` respectively.

To improve the releases grabbed by Sonarr, it is recommended to reconfigure
your quality profiles. The following guides provide detailed setups:

- Shows <https://trash-guides.info/Sonarr/sonarr-setup-quality-profiles/>
- Anime <https://trash-guides.info/Sonarr/sonarr-setup-quality-profiles-anime/>

### Prowlarr

Accessed at <https://localhost/prowlarr>

You will be prompted to setup the instance on first access. Feel free to use
any credentials that ✨spark joy✨.

You can setup the integration with Radarr and Sonarr respectively by going to
Settings > Apps and adding an integration with Radarr with the following
settings:

Radarr Server: `http://localhost:7878/radarr`
API Key: `<key found in Radarr at Settings > General > API Key>`

with Sonarr:

Sonarr Server: `http://localhost:8989/sonarr`
API Key: `<key found in Sonarr at Settings > General > API Key>`

### Bazarr

Accessed at <https://localhost/bazarr>

You can setup integration with Radarr on the left navigation bar with the
following settings:

Address: `localhost`
Port: `7878`
Base URL: `radarr`
API Key: `<key found in Radarr at Settings > General > API Key>`

You can setup integration with Sonarr on the left navigation bar with the
following settings:

Address: `localhost`
Port: `8989`
Base URL: `sonarr`
API Key: `<key found in Sonarr at Settings > General > API Key>`

### qBittorrent

Accessed at <https://localhost/qbittorrent>

By default, the credentials are:

Username: `admin`
Password: `admin`

For Radarr/Sonarr and qBittorrent to properly communicate, you will need
to make sure torrented media are written to the directory mounted as a
volume. Go to Settings > Downloads and overwrite "Default Save Path (complete)"
to point to the mounted volume, by default this is `/data/torrents`.
