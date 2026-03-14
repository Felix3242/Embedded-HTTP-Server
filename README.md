# ⚙️ Embedded HTTP Server
A lightweight HTTP server implemented in C from scratch that handles concurrent connections with multi-threading. Supports file serving, GET/POST requests, and dynamic routing with configurable directory support.

## Features
- HTTP GET and POST request handling
- Static file serving from a configurable directory
- Echo endpoint for request data
- User-Agent header retrieval
- File upload and download functionality
- Multi-threaded connection handling with fork-based concurrency
- Socket-based server architecture with port reuse
- Command-line argument parsing for directory specification

## Tech Stack
- **Language**: C
- **Networking**: POSIX sockets
- **Concurrency**: Multi-threading with fork()
- **Protocol**: HTTP/1.1

## Getting Started
**Prerequisites**
- GCC compiler
- POSIX-compliant system (Linux/Unix/macOS)

**Installation**
```bash
git clone https://github.com/yourusername/embedded-http-server.git
cd embedded-http-server/app
gcc server.c -o server
```
**Running the Server**
```bash
./server --directory /path/to/directory
```
If no directory is specified, the server uses the current directory. Server listens on port 4221.

### Testing the Server

**Simple GET request**:
```bash
curl -v http://localhost:4221/
```
**Echo endpoint**:
```bash
curl -v http://localhost:4221/echo/hello
```
**User-Agent retrieval**:
```bash
curl -v http://localhost:4221/user-agent
```
**File upload**:
```bash
curl -v -X POST http://localhost:4221/files/upload.txt -d 'Hello World'
```
**File download**:
```bash
curl -v http://localhost:4221/files/upload.txt
```

## Architecture
- **main()**: Initializes server socket, parses arguments, listens for connections
- **handle_connection()**: Processes client requests, parses HTTP methods, routes requests, and sends responses
- **Socket Management**: SO_REUSEPORT configuration, bind, listen, accept patterns
- **Concurrency**: Fork-based multi-process handling for concurrent client connections
