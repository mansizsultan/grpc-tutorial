| ------------------ | ---------- | ------------- |
| Sultan Ibnu Mansiz | 2306275840 | B             |


# Module 8: High Level Networking - Reflection

### *1. What are the key differences between unary, server streaming, and bi-directional streaming RPC methods, and in what scenarios would each be most suitable?*

- **Unary RPC** consists of one request from the client and one corresponding response from the server. It's best suited for straightforward operations like user creation or status checks.
-  **Server-side Streaming** enables the server to send multiple responses following a single client request, making it useful for handling large amounts of data, log streams, or real-time updates. 
- **Bi-directional Streaming** allows both the client and server to continuously send and receive messages over a shared connection, making it ideal for use cases like messaging apps, collaborative platforms, or live monitoring tools.

---

### *2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?*

- **Authentication** confirms a user's identity, commonly through methods like JWTs or mutual TLS.
- **Authorization** controls access to resources, ensuring users can only interact with those allowed by their roles or permissions.  
- **Data encryption** is essential for protecting communication, usually achieved with TLS to prevent eavesdropping or tampering.

---

### *3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?*

- Handling concurrent operations and maintaining message order becomes challenging when several clients are active simultaneously.
- Properly managing backpressure and preventing issues like deadlocks or message loss demands thoughtful system design.  
- Robust error handling and reconnection strategies are crucial for delivering a reliable and consistent user experience.

---

### *4. What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?*

**Advantages:**
- Integrates smoothly with asynchronous programming patterns
- Naturally accommodates backpressure mechanisms
- Can be easily adapted from an existing `mpsc::Receiver`

**Disadvantages:**
- Developers must manually manage the channel’s lifecycle
- Can add complexity in systems with high concurrency or large scale
- Debugging stream termination issues can be tricky

---

### *5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?*

- Structure your code using modules to keep responsibilities distinct, such as separating handlers, services, and models.  
- Create traits to encapsulate service behavior and hide implementation specifics. 
- Place Protobuf-generated code in specific files or separate crates for better organization.
- Apply dependency injection techniques to enhance testability and maintain clear separation of concerns.

---

### *6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?*

- Implement input validation for fields like card numbers and transaction amounts.

- Connect to external payment gateways and ensure robust handling of failures from third-party APIs.

- Maintain transaction logs and incorporate retry and rollback features to ensure data consistency.

- Include fraud detection measures and accommodate various currencies and payment options.

---

### *7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?*

gRPC enables high-performance binary communication and enforces strong typing through Protobuf, boosting both speed and developer reliability.
It supports multiple programming languages, though integration with REST/JSON-based systems may need adapters.
By using a schema-first design, it promotes clear API contracts and consistent versioning over time.

---

### *8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?*

**Advantages:**
- Supports multiple streams over a single connection, minimizing overhead

- Uses header compression and binary framing to enhance performance and efficiency

- Keeps connections open to reduce latency

**Disadvantages:**
- Can be harder to troubleshoot and monitor

- Limited native support in certain environments, such as older browsers

- Typically depends on TLS for secure communication

---

### *9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?*

REST uses a straightforward stateless request-response model, but it falls short for real-time communication needs.
gRPC, on the other hand, supports bidirectional streaming, keeping connections open for fast, low-latency data exchange.
This makes it ideal for responsive applications such as chat systems, online gaming, or real-time analytics dashboards.

---

### *10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?*

Protobuf schemas enforce structure and type safety, reducing bugs and enabling faster parsing.  
This boosts efficiency and compatibility across services.  
However, JSON's schema-less nature offers flexibility and easier human readability, at the cost of potential inconsistencies and slower parsing.