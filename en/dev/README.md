# Shuei Documentation - English Developer's guide
## Controller to Server communication
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

### Possible states
Each gadget has 2 bits:
 one for its gpio write pin, and another one to its gpio read pin.
| Write | Read | Binary | Decimal |
| :---: | :---: | :---: | :-: |
| LOW | LOW | 00 | 0 |
| LOW | HIGH | 01 | 1 |
| HIGH | LOW | 10 | 2 |
| HIGH | HIGH | 11 | 3 |
### Commands
| Command	| Description |
| :--------:	| :---------- |
| reboot	| Reboot Device |
| reload	| Restart Shuei Daemon |
| upgrade	| Upgrade Daemon Version |
| getstate	| Returns status from a GPIO pin |
| setstate	| Set GPIO pin with "1" or "0" |
| rest		| No command on stack, close socket |
### Arguments
Some commands may need an argument.
They may be included as following:
```
{ "cmd": "setstate", "args":{ "gpio":"3", "pinstate":"1"} }
```

