# Laurel Server

Clip server for [Laurel](https://github.com/Yeyito777/Laurel) — serves video clips over HTTPS with nginx.

## Install

```sh
yay -S laurel-server
```

## Setup

1. Edit `/etc/nginx/sites-available/laurel.conf` — replace `clips.example.com` with your domain
2. Add `include /etc/nginx/sites-enabled/*;` to the `http {}` block in `/etc/nginx/nginx.conf`
3. Symlink: `sudo ln -sf /etc/nginx/sites-available/laurel.conf /etc/nginx/sites-enabled/`
4. Test and reload: `sudo nginx -t && sudo systemctl reload nginx`
5. Set up HTTPS: `sudo certbot --nginx -d clips.yourdomain.com`
6. Copy the homepage: `cp /usr/share/laurel-server/index.html /srv/clips/`

## Auto-deploy (optional)

For automatic deployment on `git push`:

```sh
# On the server
git init --bare ~/laurel-server.git
cp /usr/share/laurel-server/post-receive ~/laurel-server.git/hooks/
chmod +x ~/laurel-server.git/hooks/post-receive

# On your local machine
git remote add server user@host:laurel-server.git
git push server main
```

## Forking

Fork this repo to customize the homepage and nginx config for your setup.
The auto-deploy hook will deploy your customized versions on `git push`.
