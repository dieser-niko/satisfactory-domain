# Satisfactory Server with Valid SSL

This repository describes how to provide a Satisfactory server with a valid SSL certificate, so that players don't have to accept a self-signed certificate.

## Setup

Make sure that you have docker running on your system.

- Clone/download the files from this repository onto your system (in a separate folder if possible).
- Copy/rename `.env.example` to `.env` and fill in your details.

If you want to change the default config for the Satisfactory server, refer to [wolveix/satisfactory-server](https://github.com/wolveix/satisfactory-server).

Make sure to open the following ports:
- 80/tcp
- 7777/tcp
- 7777/udp

Deploy with
```bash
docker compose up -d
```

And you're done! It may take a while the first time, as the server itself has to be downloaded.

## Reverse Proxy Setup

If you're using another reverse proxy for your whole system (like me), port 80 may already be blocked.
However, this is required for Certbot to generate an SSL certificate.

If you're using nginx, this shouldn't be a big deal (find out for yourself).

If you're using caddy, you can add `http://` in front of your domain like this:
```caddyfile
http://example.com {
    reverse_proxy :7780
}
```

I don't plan to support DNS challenges, as this only complicates things further.