# swift-server

Lightweight HTTP server implemented in pure C++

## Features

### Core Functions
- **HTTP/1.1 Compliance**: GET, POST and DELETE methods implemented
- **Static File Serving**: Serves static files from a configurable document root
- **CGI Execution**: Enables dynamic content generation using CGI scripts
- **File Upload**: Supports client file uploads in various formats (eg .pdf, .jpeg, and .png)
- **Multiple Server Support**: Capable of running multiple virtual servers concurrently
- **Concurrent keep-Alive Connections**: Supports simultaneous, long-lived connections from multiple clients

### Security 
- **Malformed Request Handling**: Detects and gracefully rejects malformed HTTP requests
- **Secure Path Handling**: Prevents directory traversal attacks
- **Request Size Limits**: Prevent Denial-of-Service (DoS) attacks by limiting client request body size
- **Request Timeout**: Prevents requests from hanging indefinitely

### Architecture
- **Event-Driven I/O**: Uses epoll for all I/O operations, ensuring non-blocking behavior
- **Multi-process for CGI**: Utilizes forking to execute multiple CGI instances


## Setup

### Prerequisites
- C++ Compiler
- GNU Make
- Linux environment (for POSIX library)
- Valgrind (optional for memory leak and error checking)

### Build Instructions

```bash
# Clone the repository
git clone https://github.com/YanYi-Now/swift-server.git swift-server
cd swift-server

# Build the project
make
```


## Usage

### Run server

```bash
# Run with config file
./swift config.conf

```

### Configuration Options 

| Parameter | Example | Description |
|---|---|---|
| `listen` | 8080 | **Listening IP address and port** 
| `server` |   | **Configuration for server block** |
| `location` | / | **Configuration for specific URI patterns** |
| `server_name` | test.com |  **Virtual host names** |
| `root` | www | **Document root directory** |
| `index` | index.html login.html | **Default files for directory request** |
| `error_page` | 404 /error_pages/404.html | **Map custom error page** |
| `limit_except` | GET POST | **Allowed HTTP methods**  |
| `autoindex` | on | **En(dis)able automatic directory listings**  |
| `client_max_body_size` | 1M | **Maximum size of client request body** |
| `cgi_exec` | .py /usr/bin/python3 | **Map CGI script extension to CGI script** |



## Project Structure
```
swift-server/
├── src/            # Source code
├── includes/       # Header files
├── www/            # Root directory for web server files
│   ├── cgi-bin/        # CGI scripts
│   ├── error_pages/    # Custom error pages
│   ├── login/          # Location of login.html file
│   ├── uploads/        # Location for file uploads
│   ├── color.html
│   ├── index.html
│   └── kirby.png
├── obj/            # Build output (generated)
├── Makefile        # Build instructions
└── config.conf     # Server configuration file
```
