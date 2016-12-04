# docker-nylas-sync-engine example

This repo is hosted at Github at https://github.com/egyptianbman/docker-nylas-sync-engine/

# What's going on?

The [docker-compose.yml](https://github.com/egyptianbman/docker-nylas-sync-engine/tree/master/example/docker-compose.yml) file contains parts of a usual docker command. This allows you to run a much simpler command to get everything up and running.

The [nylas.cnf](https://github.com/egyptianbman/docker-nylas-sync-engine/tree/master/example/nylas.cnf) file was taken from nylas/sync-engine's [/etc/my.cnf](https://github.com/nylas/sync-engine/blob/master/etc/my.cnf), with the `[client]` section removed. This allows us to maintain the same mysql configuration that nylas expects.

### Notes on docker-compose
- You'll noticed there are `VIRTUAL_HOST` and `CERT_NAME` environment variables passed to the `app` container. These are for the nginx-proxy. Please see [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) for information on what they mean and how to get it all set up. I've also [commented](https://github.com/nylas/sync-engine/issues/296#issuecomment-264374332) on a nylas issue concerning setting up with ssl and security to hopefully get you started. If you don't care about security, feel free to take them out.
