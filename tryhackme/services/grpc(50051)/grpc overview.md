## Use of Plaintext communication
   - gRPC servers by default allow communication to happen in plaintext.
   - In addition to this, when developing the client-end code, developers may use the usePlaintext() method while building a communication channel. They may use it to test the client-server interaction while the software is yet to go in production. However, this feature often gets continued to production environment.
   - poor coding practice leads to exposure of sensitive information that is being exchanged between client and server.
   - One can confirm this vulnerability via 2 tools — gRPC cURL and Wireshark.
   - When initiating an interaction with a gRPC endpoint via gRPC Curl, simply include the flag “-plaintext”. If you can view the transactions, then it is confirmed that the server communicates in plaintext.
![[grpc1.webp]]

   - One may also start Wireshark to listen for the specific port that the gRPC application is using and capture the data that is being exchanged.

![[grpc2.webp]]

## Unwanted Service Exposure via Service Reflection
   - This is a useful yet risky feature. It basically allows the server to broadcast the available services that a gRPC server is offering.
   - This can be useful when the application is being developed and can be easily used for testing. However, it can turn into a pain point as it may allow an attacker to enumerate the possible services that are being offered/exposed by the gRPC server. Thus, it is important for developers to selectively use this feature.
     ![[grpc3.webp]]

## Vulnerable Dependencies
   - Although gRPC is a modern technology, there are times when applications are found using outdated vulnerable dependencies. In our case, the application was using vulnerable versions of gRPC-Protobuf.
   - These packages could further expose the application to vulnerabilities like Prototype pollution, RCE etc.
     ![[grpc4.webp]]

## Insecure Protobuf Definition
   - The Protobuf file is the core component of gRPC. It contains the services, messages, and their definitions.
   - In our case, an improper configuration of the Protobuf file caused a service to cause unwanted data exposure.

## SQL Injection
   - gRPC applications are indeed vulnerable to injection-based attacks.
   - These types of attacks come as freebies to any application that accepts user input in any form. In our case too, we had some CRUD operations that accepted input parameters.
   - Upon tampering with the input fields, the application malfunctioned, and it revealed more data than it was required