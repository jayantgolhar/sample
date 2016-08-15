# Distributed File System

This is a distributed file system which uses Raft algorithm for consensus. It is divided into three layers i.e File System , Raft Node and Raft State machine.
`Raft state machine` implements the Raft consensus algorithm. It is moduler deterministic state machine. `Raft node` does all the wiring between different state machine modules.
`File System` provides four basic operation i.e read, write, cas and delete.

# File System Operations

**Write**

create a file, or update the file’s contents if it already exists.

`write filename numbytes_ [exptime]\r\n`

`content bytes \r\n`

The server responds with the following

`OK version\r\n`


**Read**

Given a filename, retrieve the corresponding file:

`read filename\r\n`

The server responds with the following format (or one of the errors described later)

`CONTENTS version numbytes exptime \r\n`

`content bytes \r\n`

**Compare and swap**

This replaces the old file contents with the new content provided the version is still the same.

`cas filename version numbytes [exptime]\r\n`

`content bytes\r\n`

The server responds with the new version if successful (or one of the errors described later)

`OK version\r\n`

**Delete file**

`delete filename\r\n`

Server response (if successful)

`OK\r\n`

**Error Response**

`ERR_FILE_NOT_FOUND` - If requested file is not present.

`ERR_VERSION newversion` - If version given in cas command is wrong. newversion is right version.

`ERR_CMD_ERR` - Error response for malformed command.

`ERR_INTERNAL` - For Miscellaneous internal errors.

`ERR_REDIRECT newleader` - Redirect error to clients if trying to connect other than Leader. newleader is leader Id.
# Usage

Raft generally uses 5 server for its operations. But we can use either 3 or 7 depending on replication need. First create executable using `go build` command.
Then start each file server in different terminal using `./FileServerExecutable SERVER_ID`. Now you can issue above mentioned file system operations using telnet or netcat.
Eg. telnet localhost 8081

# Installation

git clone https://git.cse.iitb.ac.in/golharj/cs733.git

cd cs733/assignment4/

go test


# Contact

Jayant Golhar(jayant.golhar68@gmail.com)
