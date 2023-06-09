# Infrarob working zone communication protocols

In this project are described the protocols to communicate between entities in the working zone. Presently, are the protocols to communicate between the drone and the Laptop-PU

## Drone <-> Laptop (AKA **Proto 1**)

The requirements for the communications between drone and latpot are the following:

- Low latency;
- Liveliness check;
- Continuous dataflow;

UDP is a unconfirmed and connectionless protocol that can by used for a consituous dataflow. Thus, it is used as a transport protocols.


### Proto 1 details

- Over UDP
- Drone acts as a server on port 8888:
- Message main contain one or multiple of:
    -  Confi:
        - Define datasink IP and port: Drone will send objects to this IP:PORT;
        - Sending method:
            - Poll only;
            - On new Object;
            - Period;
    - Data:
        - Data relative to the detected objects -> sent to the datasink IP:PORT;
    - Request:
        - Allow both parts to interrogate each other;
- Mandatory parameters:
    - Version of the protocol;
    - Timestamp;
    - Message sequence number;
    - Status

Folder **json/proto1** contains example Json file with the format of the message.

Folder **img/proto1** contains diagrams of the protocol interactions.

Folder **examples/code/proto1/** contains code snipets for the implementation of the protocols.

### Proto 1 data types ###
TBD

## Application

### Server

Waits for connections on port 8888
After configured starts sending the data from the file examples/messages/data_message.json for the configured datasing

**Usage** python examples/code/proto1/example_udp_server.py

### Client

Connects to server on port and IP passed as a parameter
Sends the configuration devined in  examples/messages/data_message.json to the server
Receive is not yet implemented in client. To listn to server just run netcat nc -ul 8000

**Usage** python3 examples/code/proto1/example_udp_client.py 127.0.0.1 8888 CONFIG