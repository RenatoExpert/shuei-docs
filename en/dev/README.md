# Shuei Documentation - English Developer's guide
## API
### Controller
In the current date, it receive POST http requests. But we need the reverse direction: controller must make TCP requests to server, and server must answer one of these commands.
| Command	|Request			| Description |
| :--------:	|:-----------			| :---------- |
| reboot	| /reboot			| Reboot Device |
| reload	| /reload			| Restart Shuei Daemon |
| upgrade	| /upgrade			| Upgrade Daemon Version |
| getstate	| /getstate/gpio\_pin		| Returns status from a GPIO pin |
| setstate	| /setstate/gpio\_pin/state	| Set GPIO pin with "1" or "0" |
#### Possible states
Each gadget has 2 bits:
 one for its gpio write pin, and another one to its gpio read pin.
| Write | Read | Binary | Decimal |
| :---: | :---: | :---: | :-: |
| LOW | LOW | 00 | 0 |
| LOW | HIGH | 01 | 1 |
| HIGH | LOW | 10 | 2 |
| HIGH | HIGH | 11 | 3 |
#### Controller to Server communication
Controllers send an single-line JSON in a TCP message to Serve that
contains only uuid and gstatus.
Server responds with a command code (cmd) and wait until controller
to send it back the exit code for that command.
Server
Example:
```
# Controller
{ "uuid":"j324u", "gstatus":"333" }
# Server
{ "cmd": "upgrade" }
# Controller
{ "exitcode":"0" }
```
| Value | Meaning |
| ---- | ---- |
| uuid | Extract with `grep /proc/cpuinfo 'Serial'`, use sed to get only the final string |
| gstatus | Gadgets status. See [possible states](#possible-states) |
| cmd | Command to be done by controller |
| exitcode | Exit code. Returns "0" on success and "1" at failure |




