# csck-comm

Simple client-server communication app with encryption written in Python.


## Features

 - ✅ One sided communication from client to server
 - ✅ Support for multiple connections
 - ✅ Asymmetrical encryption support via `age` and `x25519`
 - ✅ Configurability via command-line arguments
 - ✅ Dictionary serialization support (`XML`, `JSON`, Binary via `pickle`)
 - ✅ File read/write support
 - ✅ CTRL-C interrupt handler to gracefully shutdown connections
 - ✅ Custom `CsckException`
 - Client to server chat loop with encryption!

## Usage

```bash
chmod +x client.sh
chmod +x server.sh
./server.sh
./client.sh
```

```bash
usage: main.py [-h] -m {Server,Client} [-b BUFFER] [-p PORT] [-ip IP] [-e ENCODING] [-s {NoEncryption,Age}]
               [-dsm {Binary,XML,JSON}] [-r [READ]] [-w [WRITE]]

CSCK-COMM v1, simple TCP/IP communication tool with encryption support.

options:
  -h, --help            show this help message and exit
  -m {Server,Client}, --mode {Server,Client}
                        Sets the mode in which this app should operate
  -b BUFFER, --buffer BUFFER
                        Buffer size in bytes
  -p PORT, --port PORT  Port to use
  -ip IP, --ip IP       IP Address to bind, as a server use 0.0.0.0 to bind on all available interfaces
  -e ENCODING, --encoding ENCODING
                        Text encoding to use
  -s {NoEncryption,Age}, --secure {NoEncryption,Age}
                        Encryption method to use
  -dsm {Binary,XML,JSON}, --serialization-method {Binary,XML,JSON}
                        Data type that will be used for de/serialization for a dictionary
  -r [READ], --read [READ]
                        File path to send over the network
  -w [WRITE], --write [WRITE]
                        File path to save the contents to
```

Example:
```bash
python3 core/main.py -m Server --ip "0.0.0.0"   --port 8222 -dsm Binary
python3 core/main.py -m Client --ip "127.0.0.1" --port 8222 -dsm Binary
```

## Showcase

https://user-images.githubusercontent.com/3373490/194787937-7d8dcbcc-9310-4202-b75f-2cfcc24c9ef3.mov


## Architecture Decision Log

### `ADL-1` - Basic concepts

We expect the code to share a great portion of logic in between server and client, so because of that, ideally this app should behave like a single executable with ability to configure whether to run the app in the `client` or `server` mode.

For testing `pytest` should be used.
This repository was already configured with GitHub workflows to run tests on each commit.

For encryption, we could try to use [age](https://github.com/FiloSottile/age) which is a modern version of public-private key encryption inspired by PGP.


