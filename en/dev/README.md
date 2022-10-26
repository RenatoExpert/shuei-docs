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
#### Controller to Server package
Server must receive on pure TCP an single-line JSON from controllers.
Example:
```
{ "uuid":"j324u", "gstatus":"333" }
```
| Value | Meaning |
| ---- | ---- |
| uuid | Extract with `grep /proc/cpuinfo 'Serial'`, use sed to get only the final string |
| gstatus | Gadgets status. See [possible states](#possible-states) |
| cmd | Info about a previous command send by server |
| cmd.id | Command number |
| cmd.exit | Exit code. Returns "0" on success and "1" at failure |




