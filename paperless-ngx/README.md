# Paperless-NGX Quadlet Pod

Unsupport Quadlet Pod for Paperless-NGX

> [!WARNING]
> Documentation work in progress

## Installation

Create 2 random secrets

`openssl rand -base64 64 | podman secret create paperless-db-password -`

`openssl rand -base64 64 | podman secret create paperless-secret-key -`

copy `.container`, `.volume`, `.pod` to ~/.config/containers/systemd/

> [!Note]
> I only use `.volume` for testing. You can replacing `.volume` with local directories. 

### Change .Volume to directory

 For example you can create directories in `/opt/paperless/` for each volume.
  ```
 sudo mkdir -p /opt/paperless/{db,broker,data,media,export,consume}
 sudo chown -R { user }: /opt/paperless
 ```
 change each `Volume=` in `paperless-db.container`, `paperless-webserver.container`, `paperless-broker.contaner` point to coorect directory. For example in `paperless-webserver.container`, change  Volume=/opt/paperless/data:/data:z`


```bash
cp paperless* ~/.config/containers/systemd/
```

Run `systemctl --user daemon-reload`

```bash
systemctl --user start paperless-pod.service
```

### Creating Admin user

Before you can login for the first time, you need to create a admin account. We will enter the container and create account.

```bash
podman contaniner exec -it paperless-webserver /bin/bash

python3 manage.py createsuperuser
```
