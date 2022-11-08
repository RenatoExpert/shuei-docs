# Shuei Documentation - Developer's guide
## Network communication
* All messages are send using a single-line JSON string via TCP.
* Clients and Controllers only have direct communication with the Server.
### Controller
#### Handshake
When a controller get connected to server, it may send its _type_ and _uuid_.
```
# Controller
{ "type": "controller", "uuid": "jac2345" }
```
Then it sends a status message, that will be re-sended on every change.
#### Status reporting
It consists of a list of gadgets, with its parameters and states.
Its sent after handshake and on any change.
```
# Controller
[
  {
    "sensor": "true",
    "relay": "true",
    "mode": "serial",
    "theme": "heater"
  },
  {
    "sensor": "false",
    "relay": "true",
    "mode": "paralel",
    "theme": "light"
  }
]
```
Check controller's configuration section to better understanding these parameters.
### Client
#### Handshake
Clients may send only its type. It receives back status from all controllers at once.
```
# Client
{ "type": "client" }
```
Server may answer with status from all controllers.
#### Status reporting
Clients receives a status report after handshake and after each change on any device.
It maps lists of gadgets andressed by its respective controller uuid.
```
# Server
{
  "j324u": [
    {
      "sensor": "true",
      "relay": "true",
      "mode": "serial",
      "theme": "heater"
    },
    {
      "sensor": "false",
      "relay": "true",
      "mode": "paralel",
      "theme": "light"
    }
  ],
  "r123a": [
    // All its gadgets
   ],
   ...
}
```
### Command communication
#### Client to server
When a gadget button is pressed, client sends a signal to lock or unlock that gadget's Write Pin.
Some commands may need an argument.
They may be included as following:
```
{
  "uuid": "mycontroller",
  "command": "tap",
  "gadget": "1"
}
```
#### Server to controller
Server may send only command and args to the right controller:
```
{
  "command": "tap",
  "gadget": "1"
}
```
#### Command sheet
| Command	| Description |
| :--------:	| :---------- |
| reboot	| Reboot Device |
| reload	| Restart Shuei Daemon |
| upgrade	| Upgrade Daemon Version |
| setstate	| Set GPIO pin with "1" or "0" |
| tap | Invert relay state |
