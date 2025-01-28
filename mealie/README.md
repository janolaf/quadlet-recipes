# Mealie Quadlet Pod

This quadlet creates a Pod with a postgres container and mealie container

## Installation

Make sure you have podman installed.

Make sure `~/.config/containers/systemd` exists.


```bash
mkdir -p ~/.config/containers/systemd/
```

Generate random postgresql password and store it as a secret.


```bash
openssl rand -base64 64 | podman secret create mealie-db-password -
```

Copy `.pod`, `.container` in Pod directory to `~/.config/containers/systemd/`.

Change `BASE_URL` to your subdomain or ip address.

```bash
systemctl --user daemon-reload
```

```
systemctl --user start mealie-pod.service
```
