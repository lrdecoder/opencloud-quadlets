## Opencloud with podman quadlets

An example setup for an opencloud installation using podman quadlets. I do not plan to keep it up to date, but put it here because it may be useful for somebody who wants a similar setup. The files are based on a setup that I have working on an ARM vps, but redacted and somewhat simplified. The setup is heavily inspired by the opencloud full docker deployment (https://github.com/opencloud-eu/opencloud/tree/main/deployments/examples/opencloud_full)

All containers are in the same podman network (opencloud.network) Unfortunately, source ip adresses are not preserved in the reverse proxy. Regarding this, see:

*   https://github.com/eriksjolund/podman-networking-docs
*   https://github.com/eriksjolund/podman-caddy-socket-activation

The containers are:

*   caddy.container: the reverse proxy, see also the very simple Caddyfile (if this container is down, the collaboration container does not start!)
*   opencloud.container: the main opencloud container (only starts after the clamav container is online)
*   tika.container:  full text search
*   clamav.container: virus scanner (uses quite some resources and takes some time to become available!)
*   collabora.container: online file editor
*   collaboration.container: the opencloud collaboration server (runs the opencloud wopiserver, only starts after both the opencloud container and the collabora container are online)
*   s3proxy.container: proxy between opencloud and the external s3 server, in this case used for client-side encryption