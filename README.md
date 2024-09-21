# Satisfactory Server with HTTPS

This repository describes how to deploy a Satisfactory Server that has a valid SSL certificate so that the players don't have to accept a self-signed one.

## Setup

Make sure that you have docker running on your system.

Configure `Caddyfile` with the correct mail address and domain.

If you don't have another reverse proxy on your system, change port 7780 to 80 in the `docker-compose.yml`.

If you want to change the default config, refer to [wolveix/satisfactory-server](https://github.com/wolveix/satisfactory-server).

Make sure to open the following ports:
- 80/tcp
- 7777/tcp
- 7777/udp

Deploy with
```bash
docker compose up -d
```
And you're done! It might take a bit on the first run because the server itself needs to be downloaded first.

## Reverse Proxy Setup

If you're using another reverse proxy for your whole system (like I do) the port 80 might already be blocked.
However, this is required for Caddy/Certbot to generate a SSL certificate.

I might change things up and use the certbot directly instead of caddy. This could allow other methods of verifying the domain.

But for now just make sure to forward your domain directly to the caddy reverse proxy.
If you're using nginx, then that shouldn't be a big deal. If you're using caddy, you can add `http://` infront of your domain like this:
```caddyfile
http://example.com {
    reverse_proxy :7780
}
```
