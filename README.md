[hub]: https://hub.docker.com/r/chanwit/fivem
[git]: https://github.com/chanwit/fivem

# [chanwit/fivem][hub]

[![](https://images.microbadger.com/badges/image/spritsail/fivem.svg)](https://microbadger.com/images/spritsail/fivem)
[![Latest Version](https://images.microbadger.com/badges/version/spritsail/fivem.svg)][hub]
[![Git Commit](https://images.microbadger.com/badges/commit/spritsail/fivem.svg)][git]
[![Docker Pulls](https://img.shields.io/docker/pulls/spritsail/fivem.svg)][hub]
[![Docker Stars](https://img.shields.io/docker/stars/spritsail/fivem.svg)][hub]
[![Build Status](https://drone.spritsail.io/api/badges/spritsail/fivem/status.svg)][drone]

This docker image allows you to run a server for FiveM, a modded GTA multiplayer program.
Upon first run, the configuration is generated in the host mount for the `/config` directory.
The container should be stopped so fivem can be configured to the user requirements in the `server.cfg`.

## License Key

A freely obtained license key is required to use this server, which should be declared as `$LICENSE_KEY`. A tutorial on how to obtain a license key can be found [here](https://forum.fivem.net/t/explained-how-to-make-add-a-server-key/56120).

## Usage

Use the `docker-compose` script provided if you wish to run a couchdb server with FiveM, else use the line below:

```sh
export LICENSE_KEY=<your license key>

docker run -d -it \
  --name fivem \
  --restart=on-failure \
  -e LICENSE_KEY=$LICENSE_KEY \
  -p 30120:30120/tcp \
  -p 30120:30120/udp \
  -v /volumes/fivem:/config \
  chanwit/fivem
```

_It is important that you use `interactive` and `pseudo-tty` options otherwise the container will crash on startup_
See [issue #3](https://github.com/spritsail/fivem/issues/3)

### Environment Variables

- `LICENSE_KEY` - This is a required variable for the license key needed to start the server.
- `RCON_PASSWORD` - A password to use for the RCON functionality of the fxserver. If not specified, a random 16 character password is assigned. This is only used upon creation of the default configs
- `NO_DEFAULT_CONFIG` - Optional. Set to any non-zero value to disable the default exec config.
- `NO_LICENSE_KEY` - Optional. Set to any non-zero length value to disable specifying the license key in the environment. Useful if your license key is in a config file.
- `NO_ONESYNC` - Optional. Set to any non-zero value to disable OneSync being added to the default configs.
