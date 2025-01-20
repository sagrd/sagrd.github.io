---
layout: post
---
As applications evolve, so must the data they store. This post explores how to handle schema changes, data encoding formats, and dataflow modes to ensure seamless data evolution and compatibility in your applications.

## Handling Schema Changes in Databases

- Application Changes:
  - Application feature updates often necessitate corresponding changes to the stored data.

- Schema Management:
  - Relational Databases: Conform to a single schema at any given time. Schema changes are possible but require careful handling.
  - Schemaless Databases: Handle multiple data formats simultaneously (schema-on-read).

## Rolling Upgrades in Large Applications

- Gradual Deployment:
  - Perform rolling upgrades by deploying new versions to a few nodes at a time, minimizing service downtime.

- Compatibility Requirements:
  - Maintain both backward and forward compatibility:
    - Backward Compatibility: Newer code can read data written by older code.
    - Forward Compatibility: Older code can read data written by newer code.

## Data Encoding Formats

- In-Memory vs. Persistent Data:
  - In-memory data needs encoding (serialization) for storage or network transmission.
  - Decoding (deserialization) translates byte sequences back into in-memory representations.

- Built-In Language Support:
  - While programming languages offer built-in encoding support, they are often tied to specific languages and can pose security risks.

- Standardized Encodings:
  - Human-Readable Formats: JSON, XML, and CSV are popular for data interchange but have limitations (e.g., number encoding ambiguities, lack of binary string support).
  - Binary Formats: Thrift, Protocol Buffers (protobuf), and Avro provide more efficiency and flexibility.

## Handling Schema Evolution

- Thrift and Protocol Buffers:
  - Use field tags (numbers) instead of field names for encoding data.
  - Ensure compatibility by:
    - Ignoring unrecognized tags for forward compatibility.
    - Assigning unique tag numbers to each field for backward compatibility.
  - Handle schema changes (adding/removing fields) with care to maintain compatibility.

- Apache Avro:
  - Supports two schema languages: Avro IDL (human-editable) and JSON (machine-readable).
  - Uses schemas to define data types during encoding and decoding.
  - Supports schema evolution with forward and backward compatibility:
    - Forward Compatibility: New schema writer, old schema reader.
    - Backward Compatibility: Old schema writer, new schema reader.
  - Ensure new fields have default values to maintain compatibility.

## Dataflow Modes

- Via Databases:
  - Encoded data is written to and read from databases.
  - Older and newer versions of code and data coexist.
  - Schema changes may require explicit data rewriting.

- Via Service Calls:
  - Processes communicate over networks using services.
  - RPC vs. RESTful APIs:
    - RPC can be problematic due to network unpredictability.
    - REST APIs are better for experimentation and debugging.
  - Modern RPC frameworks highlight the differences between local and remote calls.

- Via Asynchronous Message Passing:
  - Clients send messages to a broker, which stores and forwards them.
  - Advantages include buffering, crash recovery, and decoupling sender and recipient.
  - Open-source brokers: RabbitMQ, ActiveMQ, HornetQ, NATS, Apache Kafka.

## Distributed Actor Frameworks

- Actor Model:
  - Encapsulates logic and state within actors, which communicate via asynchronous messages.
  - Suitable for scaling applications across multiple nodes.

- Frameworks:
  - Akka: Uses Java's built-in serialization (replaceable with Protocol Buffers).
  - Orleans: Uses a custom encoding format.
  - Erlang OTP: Challenges with schema changes in records.

## Distributed Databases
- Reasons for Distribution:
  - Scalability.
  - Fault tolerance and high availability.
  - Lower latency with geographically distributed servers.
