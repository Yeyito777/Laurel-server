# Laurel Server

Server component for [Laurel](https://github.com/Yeyito777/Laurel) — serves clips, provides a management UI, and handles the clip API.

## Setup

### 1. Create a bare repo on your server

```sh
git init --bare ~/laurel-server.git
```

### 2. Configure your server

```sh
sudo cp laurel-server.conf.example /etc/laurel-server.conf
sudo nano /etc/laurel-server.conf
```

Set your `DOMAIN`, `USER`, and any other overrides.

### 3. Install the deploy hook

```sh
cp post-receive ~/laurel-server.git/hooks/
chmod +x ~/laurel-server.git/hooks/post-receive
```

### 4. Set up SSL (Let's Encrypt)

```sh
sudo certbot --nginx -d your-domain.com
```

### 5. Push to deploy

From your local machine:

```sh
git remote add server ssh://user@your-server/~/laurel-server.git
git push server main
```

Every push templates the nginx config and systemd service from `/etc/laurel-server.conf`, deploys the homepage, and restarts the API.

## What's included

- **Homepage** — clip browser with rename/delete (ident cookie auth)
- **laurel-api** — lightweight Python API for clip management
- **nginx config** — static clip serving + API proxy (templated with your domain)
- **systemd service** — manages the API process

## Clip directory structure

```
/srv/clips/<slug>/
├── index.html          # Embeddable clip page
├── Replay_*.mp4        # The video
├── thumb.jpg           # First-frame thumbnail
├── .owner              # Ident token (hidden from web)
└── .name               # Display name (hidden from web, optional)
```
