# Shuei Documentation - English Developer's guide
## API
### Controller
In the current date, it receive POST http requests. But we need the reverse direction: controller must make TCP requests to server, and server must answer one of these commands.
Command		|Request			| Description
:--------:	|:-----------			| :----------
reboot		| /reboot			| Reboot Device
reload		| /reload			| Restart Shuei Daemon
upgrade		| /upgrade			| Upgrade Daemon Version
getstate	| /getstate/gpio\_pin		| Returns status from a GPIO pin
setstate	| /setstate/gpio\_pin/state	| Set GPIO pin with "1" or "0"
