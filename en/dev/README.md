# Shuei Documentation - Developer's guide
## Network communication
* All messages are send using a single-line JSON string via TCP.
* Clients and Controllers only have direct communication with the Server.
### Connecting
#### Controller
When a controller get connected to server, it may send its _type_ and _uuid_.
Server does not aswer to it.
```
# Controller
{ "type": "controller", "uuid": "jac2345" }
```
#### Client
Clients may send only its type. It receives back status from all controllers at once.
```
# Client
{ "type": "client" }
# Server
{ "controller_A": "210", "controller_B": "203", "controller_C": "000" }
```

### Controller reports to Server
When controller pins change its status, server shall be reported.
Example:
```
{ "gpio_status" : "230" }
```
#### Understanding gpio status code
Each gadget has 2 bits:
 one for its gpio write pin, and another one to its gpio read pin.
| Write | Read | Binary | Decimal |
| :---: | :---: | :---: | :-: |
| LOW | LOW | 00 | 0 |
| LOW | HIGH | 01 | 1 |
| HIGH | LOW | 10 | 2 |
| HIGH | HIGH | 11 | 3 |

Each controller holds 3 gadgets.
### Client sends a new command to Server
When a gadget button is pressed, client sends a signal to lock or unlock that gadget's Write Pin.
Some commands may need an argument.
They may be included as following:
```
{ "uuid": "mycontroller", "command": "setstate", "args":{ "gpio":"3", "pinstate":"1"} }
```
Server may send only command and args to the right controller:
```
{ "command": "setstate", "args":{ "gpio":"3", "pinstate":"1"} }
```
#### Command sheet
| Command	| Description |
| :--------:	| :---------- |
| reboot	| Reboot Device |
| reload	| Restart Shuei Daemon |
| upgrade	| Upgrade Daemon Version |
| setstate	| Set GPIO pin with "1" or "0" |
| revertstate | Flip between "0" or "1" |

### Server as a router
* When server receives a gpio status reporting from controller, it broadcasts this status to all clients.
* But when it receives a command from a client, it sends only for the right controller.
* If a controller were disconnected from server, client must be notified.
