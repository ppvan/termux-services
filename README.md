# Termux services

## Install

```
pkg install termux-services
```

## Usage

### Setup
Restart your shell so that the service-daemon is started. You can verify it by

```
$ ps -aux | grep runsvdir
```

> 2 matches should be returned, if not, clear Termux app and retry

### Commands

```
sv up <service> # Start service
sv down <service> # Stop service
sv-enable <service> # start when termux start
sv-disable <service> # undo sv-enable

pstree # list all running service as a tree

```

> For more complex command, check [upsteam docs](https://smarden.org/runit/sv.8)

### Checking service log

```
cat $PREFIX/var/log/sv/<service>/current
```


A service is disabled if `$PREFIX/var/service/<service>/down` exists, so the `sv-enable` and `sv-disable` scripts touches, or removes, this file.


# Custom services

> Some services packaged with termux-service file by default, like nginx and sshd, so you may not need this section.

All of the services are in: `$PREFIX/var/service`

So to create a custom services: Create <service_name> folder with following structure:
```
.
├── log -> directory
└── run -> sh script
```

And add command to the `run` file:

```
#!/data/data/com.termux/files/usr/bin/sh

exec <any command you like, run this foreground mode>

```
