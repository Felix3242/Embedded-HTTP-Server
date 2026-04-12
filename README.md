# Embedded HTTP Server
A lightweight HTTP server in C built from scratch. Handles concurrent connections with fork-based multi-processing, supports file serving, and parses HTTP/1.1 requests.
 
## Features
- HTTP GET and POST request handling
- Static file serving from configurable directory
- Echo and User-Agent endpoints
- File upload and download
- Fork-based concurrent connection handling
- Command-line directory configuration
 
## Tech Stack
- Language: C
- Networking: POSIX sockets
- Concurrency: fork()
- Protocol: HTTP/1.1
 
## Getting Started
Prerequisites: GCC compiler, POSIX-compliant system (Linux/Unix/macOS)
 
```
cd app
gcc server.c -o server
./server --directory /path/to/directory
```
 
Server listens on port 4221. If no directory is specified, uses the current directory.
 
### Testing
```bash
# GET request
curl -v http://localhost:4221/
 
# Echo endpoint
curl -v http://localhost:4221/echo/hello
 
# File upload
curl -v -X POST http://localhost:4221/files/upload.txt -d 'Hello World'
 
# File download
curl -v http://localhost:4221/files/upload.txt
```
 
## Architecture
- `main()`: Initializes server socket, parses arguments, listens for connections
- `handle_connection()`: Parses HTTP methods, routes requests, sends responses
- Socket management with SO_REUSEPORT, bind, listen, accept
- Fork-based multi-process handling for concurrent clients
