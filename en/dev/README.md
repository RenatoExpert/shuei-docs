# Shuei Documentation - Developer's guide
## Network communication
* All messages are send using a single-line JSON string via TCP.
* Clients and Controllers only have direct communication with the Server.
### Connecting
When a client get connected to server, it may send its _type_ at first.
In case of controllers, it may send its _uuid_ also.
Examples
```
{ "type": "controller", "uuid": "jac2345" }
{ "type": "client" }
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
{ "cmd": "setstate", "args":{ "gpio":"3", "pinstate":"1"} }
```
#### Command sheet
| Command	| Description |
| :--------:	| :---------- |
| reboot	| Reboot Device |
| reload	| Restart Shuei Daemon |
| upgrade	| Upgrade Daemon Version |
| setstate	| Set GPIO pin with "1" or "0" |
| revertstate | Flip between "0" or "1" |
| rest		| No command on stack, close socket |

## Client to Server communication
Client may send tcp packages containing comands (or not) and server must responds with all devices status.
Example:
```
# Client
{
  "type": "client",
  "commands": [
    {
      "uuid":"j324u",
      "cmd":"setstate",
      "args": { 
        "gpio":"3",
        "pair_id":"1"
      }
    },
    {
      "uuid":"e432r",
      "cmd":"reboot"
    }
  ]
}
# Server
{
  "j324u": "333",
  "e432r": "302",
  "w334q": "000"
}
```


