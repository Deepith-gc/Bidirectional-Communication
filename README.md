# Bidirectional-Communication
1. Project Overview
This project implements a complete, self-contained system featuring a client and a server that communicate using a custom lightweight protocol. The primary goals were to design a reliable communication protocol from scratch, implement it in Python, and deploy the entire system using Docker containers for isolated, reproducible environments.
The system supports bidirectional communication, including features like connection handshake, state transitions, and robust error handling as specified in the problem statement.

2. Features & Protocol Design
The core of this project is the custom protocol, designed to meet the following requirements:
Protocol Features
 * Handshaking: A defined initial sequence for connection establishment and parameter negotiation.
 * Bidirectional Exchange: Supports reliable, simultaneous data transfer from both the Client and the Server.
 * Acknowledgment (ACK): Implements mechanisms for message sequencing and acknowledgment to ensure reliability.
 * Payload Management: Handles structured data exchange (control requests, status updates, responses, etc.).
 * State Management: Clearly defined state transitions for connection, establishment, and termination.
Implementation Details
 * Language: Python
 * Protocol Layer: Custom (Layer 5/6 concept over TCP/UDP/IP)
 * Message Format: Implemented a fixed/variable message format, including:
   * Type: Message category (e.g., DATA, ACK, HELLO, FIN)
   * Sequence Number: For ordering and duplication detection.
   * Payload Length: Specifies the size of the application data.
   * Payload: The application-specific structured data.
   
3. System Architecture
The project utilizes a standard Client-Server model deployed via Docker.
 * Client (client.py): Initiates connections and sends control/data requests.
 * Server (server.py): Listens for incoming connections, processes client requests, and manages state.
 * protocol/: Contains the shared protocol logic, message files, and handler functions used by both the client and server.
 * Docker: Used for packaging and deployment, ensuring consistency across environments.
   * docker/client/Dockerfile and docker/server/Dockerfile build the images.
   * docker-compose.yml orchestrates the client and server containers, setting up networking.
   
4. Getting Started
Prerequisites
You must have the following installed on your system:
 * Docker
 * Docker Compose
Running with Docker Compose
To build and run the entire system in isolated containers:
 * Clone the repository:
   git clone [YOUR_REPOSITORY_URL]
cd Project-root/

 * Build and run the containers:
   docker-compose up --build

   (The --build flag ensures your latest code is packaged.)
 * View Logs:
   The logs from both the client and server will be displayed in your terminal.
   * To run in the background, use docker-compose up -d.
 * Stop the system:
   docker-compose down

5. Analysis and Documentation
The project includes thorough documentation and performance analysis to validate the protocol design:
 * 📄 Protocol Specification Document: (Check docs/ folder) Contains the formal specification, including the Protocol State Diagram and message formats.
 * 📊 Performance Benchmarks: Reports on latency, throughput, and reliability under various conditions (e.g., packet loss simulation).
 * 📋 Wireshark PCAP Files: Included for in-depth protocol analysis and message sequence validation.
 * 🧪 Test Suite: Comprehensive unit and integration tests for protocol handler and core functionality.
 
6. Project Structure
Project-root/
│
├── client/
│   ├── client.py
│   └── protocol/         # Shared protocol handler and message files
│
├── server/
│   ├── server.py
│   └── protocol/
│
├── docker/
│   ├── client/
│   │   └── Dockerfile    # Client container build
│   └── server/
│       └── Dockerfile    # Server container build
│
└── docker-compose.yml    # Orchestrates the Client and Server containers
