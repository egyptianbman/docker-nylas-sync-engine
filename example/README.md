# docker-nylas-sync-engine example

This repo is hosted at Github at https://github.com/egyptianbman/docker-nylas-sync-engine/

## What's going on?

The [docker-compose.yml](https://github.com/egyptianbman/docker-nylas-sync-engine/tree/master/example/docker-compose.yml) file contains parts of a usual docker command. This allows you to run a much simpler command to get everything up and running.

The [nylas.cnf](https://github.com/egyptianbman/docker-nylas-sync-engine/tree/master/example/nylas.cnf) file was taken from nylas/sync-engine's [/etc/my.cnf](https://github.com/nylas/sync-engine/blob/master/etc/my.cnf), with the `[client]` section removed. This allows us to maintain the same mysql configuration that nylas expects.

To pull the latest version of the containers, run `docker-compose pull`.

To start the containers, run `docker-compose up -d --remove-orphans`.

To stop the containers, run `docker-compose stop`.

To remove the containers, run `docker-compose rm -f && docker rmi $(echo "${${PWD##*/}/./}_app" | sed "s/[^a-zA-Z0-9_]//g")`.
**Note:** You have to stop the containers before you can remove them. Also, the `docker rmi` portion will remove the images associated with the containers.

## I've got the containers running. Now what?

Once you have the containers running, you need to authenticate your account(s). To do this, run the following commands:

```bash
# The following will allow you to open a prompt into the app container (where the sync engine is running)
$ docker-compose exec app bash

# Now that you're in the container, become the inbox user
$ sudo su inbox

# You should now be the inbox user in the /opt/inboxapp directory. Now you need to authenticate an account. You can run this command for each e-mail address you need to authenticate.
$ ./bin/inbox-auth your@e-mail.com
```

### Notes
- You'll noticed there are `VIRTUAL_HOST` and `CERT_NAME` environment variables passed to the `app` container. These are for the nginx-proxy. Please see [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) for information on what they mean and how to get it all set up. I've also [commented](https://github.com/nylas/sync-engine/issues/296#issuecomment-264374332) on a nylas issue concerning setting up with ssl and security to hopefully get you started. If you don't care about security, feel free to take them out.
- This docker-compose setup is configured to store mysql, redis and all your attachments in the local directory. Make sure you have enough hard drive space to hold all that or modify docker-compose.yml to use a directory elsewhere.
