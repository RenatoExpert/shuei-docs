# Shuei Documentation - English
## Admin's manual
### Getting started
Do not forget to read the [user manual](../user) to understand the basics under the project.
Once you are familiar with its usage, lets work on how to **setup** your own *Shuei System*.
### Products
The Shuei project is divided in __three software applications__, one __schmematics__ and a __complete documentation__(that you are currently reading).
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

