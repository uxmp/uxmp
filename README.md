# uxmp - ux Music Player

## Setup

Copy .env.dist to .env and adjust the variables according to your server setup

TBD

## Webserver configuration

The config is based on the release tarball folder structure:

- /path/to/ui: Document-Root, containing the gui
- /path/to/core: Folder containing the core source

### nginx

```
root /path/to/ui;

location / {
        index  index.html;
        try_files $uri $uri/ /index.html;
}

location /api/ {
        alias /path/to/core/src/public/;
        
        try_files $uri $uri/ @nested;
}

location @nested {
        rewrite /api/(.*)$ /api/index.php?/$1 last;
}
```

## Add a catalog

uxmp organizes the music library in so called `catalogs`. To start over, simply
use the cli tool to add a catalog.

```shell
./bin/cli catalog:add /path/to/music/library
```

This command will create the catalog and print its id.

To run a catalog update (e.g. to add files after catalog creation), use the catalog update command
and the id of the catalog:

```shell
./bin/cli catalog:update <catalogId>
```
