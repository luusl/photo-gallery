Photo Gallery
==============

![](https://img.shields.io/github/check-runs/rigon/photo-gallery/master.svg "Build Status")
![](https://img.shields.io/github/tag/rigon/photo-gallery.svg "Latest version")
![](https://img.shields.io/docker/image-size/rigon/photo-gallery.svg "Docker image size")
![](https://img.shields.io/docker/pulls/rigon/photo-gallery.svg "Pulls from DockerHub")
[![Docker Hub](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=fff)](https://hub.docker.com/r/rigon/photo-gallery)

Photo Gallery is a self-hosted performant application to organize your photos. Built for speed with React and Go, explore your photos quick and easy!

## [Live Demo](https://demo.photogallery.rigon.uk/)
<p style="text-align: center;">
<img src="screenshot.jpg" alt="Photo Gallery" style="text-align: center; width: 100%; max-width: 683px"/>
</p>

## Quick start

Using docker, run:

    docker run -p 3080:3080 --name photo-gallery rigon/photo-gallery:demo

That's it, enjoy! Just open in your browser [http://localhost:3080](http://localhost:3080).

This image however includes a demo gallery, for your own use please use `rigon/photo-gallery`.

## Serving under a subpath

This project can be served under a configurable base path (subpath) such as `/gallery`.

- Frontend: the Vite build can be configured with `--base` (or env vars) so assets and routes resolve correctly under a subpath. Example build command:

    npm run build -- --base /gallery/

  This will set `import.meta.env.BASE_URL` (and `%BASE_URL%` in HTML) to `/gallery/`.

- Backend: the server now accepts a `--base-path` CLI flag to mount API, WebDAV and the web UI under the chosen base path. Example:

    cd server && ./photo-gallery --port 3080 --base-path /gallery -c "name=Photos,path=/photos,thumbs=/thumbs"

  The API will then be available at `http://localhost:3080/gallery/api/...`.

- Docker: the image entrypoint supports passing `--base-path`. Example:

    docker run -p 3080:3080 --name photo-gallery -v /media/photos:/photos -v /data/thumbs:/thumbs rigon/photo-gallery --base-path /gallery -c "name=Photos,path=/photos,thumbs=/thumbs"

Notes and caveats:

- When building the frontend for a subpath use Vite's `--base` flag so `import.meta.env.BASE_URL` is set at build time. PWA/service-worker paths should be verified after deploying under a subpath.
- If you front the application with a reverse proxy (nginx, Caddy), prefer routing `{base}/api/*` to the backend and `{base}/*` to the static files. Alternatively you can rewrite paths in the proxy, but configuring the app is more robust.

## [The rest of README unchanged]
