# Shuei Documentation - Admin's manual
## Getting started
Do not forget to read the [user manual](../user) to understand the basics under the project.
Once you are familiar with its usage, lets work on how to **setup** your own *Shuei System*.
### Products
The Shuei project is divided in __three software applications__, one __schmematics for electronics__ and a __complete documentation__ (which you are currently reading).
### Software Architecture
We have three software that work on different hardware and functions:
* [Controller](https://github.com/renatoexpert/shuei-controller/):
Its the software that is run by the controller.
It keeps listening to Shuei Server commands to turn on/off eletrical connections and sends its sensors data.
You may have as many controllers as you want.
Each controller can take care of multiple eletrical devices.
* [Server](https://github.com/renatoexpert/shuei-server/):
Server handles requests from clients and send their commands to controllers.
It also log everything that goes with them.
The entire system needs only a single server.
You may use our cloud service or setup your own physical server.
* [Client](https://github.com/renatoexpert/shuei-client/):
Users may view and manage their devices using this App.
You may install it on your phone or computer.
It comunicates directly on your Shuei Server.

## Controller
### Download and run
In order to control the gadgets, a hardware with GPIO(General-purpose input/output) support is necessary.
We recommend _Raspberry Pi Zero 2W_ since its cheap but strong enough to take the job done.
1. Download iso images from [Controller Repository](https://github.com/renatoexpert/shuei-controller) and make a bootable microSD card.
2. Make sure all electronic connections are fine and boot the controller.
3. Connect to its hotspot WLAN
4. Once into its hotspot, access 192.168.0.1 using a browser and configure it.
5. Accept the new controller using Shuei Client.

## Server
### Download and run
Server is originally made in ruby. We are working on a alternative Java GUI version.
