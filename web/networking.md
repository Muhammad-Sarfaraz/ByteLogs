# Networking

#### Network Layer
* Physical Layer: Manages the physical connection between devices, dealing with raw data transmission over the network medium.

* Data Link Layer: Ensures error-free point-to-point or point-to-multipoint communication, framing, and MAC address assignment.

* Network Layer: Assigns logical addresses (IP), determines optimal paths for data packets, and enables communication between devices on different networks.

* Transport Layer: Manages end-to-end communication, ensures reliable data delivery, and handles flow control and error recovery.

* Session Layer: Establishes, maintains, and terminates connections between applications, managing dialog control and synchronization.

* Presentation Layer: Translates data between application and network formats, ensuring compatibility and handling encryption and compression.

* Application Layer: Provides a user interface, network services, and end-user services, supporting communication between software applications.


#### Ports
* Numeric identifiers (0-65535) allowing multiple applications on a device to communicate over a network; distinguish services, 
enable socket programming, and facilitate firewall configurations.

* Well-known ports (0 to 1023) are reserved for system services (e.g., HTTP uses port 80, HTTPS uses port 443).
Registered ports (1024 to 49151) are assigned to specific applications.Dynamic or private ports (49152 to 65535) are used for temporary connections.

* HTTP commonly uses TCP port 80, while DNS typically uses UDP port 53.

#### TCP Vs UDP
* TCP: Ensures reliable web content delivery.
  * TCP (When): Reliable, ordered data; essential for HTTP, FTP, SMTP.
* UDP: Rarely used due to lack of reliability.
  * UDP (When): Low-latency, real-time; used in DNS, DHCP, VoIP.

#### HTTP
Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML.

Flow : Open a TCP connection->Send an HTTP message->Read the response sent by the server->Close or reuse the connection for further requests.

```python
import socket

def send_http_request(host, port, message):
    # Create a TCP socket
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        # Connect to the server
        s.connect((host, port))

        # Send the HTTP request
        s.sendall(message.encode('utf-8'))

        # Receive the response
        response = s.recv(4096)  # You might need to adjust the buffer size

    return response.decode('utf-8')

# Example usage
host = 'example.com'  
port = 80 
http_request = "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n"  

response = send_http_request(host, port, http_request)
print(response)
```
