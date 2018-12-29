# globus-identifiers-client
Client SDK and CLI for the Globus Identifiers Service

## Summary
The globus-identifiers-client package provides command line and SDK interfaces to the Globus Identifiers Service.

## Pre-Requisites
Building and installing the globus-identifiers-client requires the use of the [`pipenv`](https://pipenv.readthedocs.io/en/latest/) tool. Pre-install it with the command `pip install --user --upgrade pipenv` or a similar command suitable for your installation.

## Building
The default method of building the client is simply to use `make install` which creates the local executable file `globus-identifiers-client`. This default method assumes a build using Python version 3.6. Other versions of Python may be forced by setting the `PYTHON_VERSION` environment variable prior to running `make install`. For example, the command `PYTHON_VERSION=2.7 make install` will build for use with version 2.7 of the python interpreter.

At present, only python versions 2.7 and 3.6 have been tested.

## Running
A completed build will create an executable file `globus-identifiers-client` in the base directory for the project.  Additional help running the command can be found using the command `globus-identifiers-client --help`. Typically, the first command to be executed will be `globus-identifiers-client login` to create a cache of the credentials needed to interact with the service in subsequent invocations of the command. The `login` command will open a web browser which will step you through logging in with your Globus identity and for providing consent for the command line tool to perform operations on the Globus Identifiers Service on your behalf.

## Use as an SDK
The SDK functionality is encapsulated in the source file `identifiers_client/identifiers_api.py`. The Doc String comments on the various methods of the `IdentifierClient` class describe the parameters to the operations. 

### Examples

```
from identifiers_client.identifiers_api import identifiers_client
from identifiers_client.config import config
# Loads tokens stored from config
client = identifiers_client(config)
client.create_identifier(namespace='<my_namespace>', visible_to=['public'])

## Use as a Command Line Client

A client comes with the installation, and can be used with `globus-identifiers-client`

### Examples

Below are example commands

#### Print information on all options for creating identifiers
```
$ globus-identifiers-client identifier-create --help
```

#### Create an Identifier

```
globus-identifiers-client identifier-create --namespace <my_namespace> --visible-to public
```

### Update an identifier

#### Add a location

```
globus-identifiers-client identifier-update --identifier <myidentifier> --locations https://foo.example.com
```

#### Add many fields

```
globus-identifiers-client identifier-update --identifier <myidentifier> --locations https://foo.example.com https://example.com/foo --checksum-sha256 sha256checksum --checksum-md5 mymd5checksum --metadata file://foo.json
```