# gRPC

<https://grpc.io/docs/>

Proto3 Language Specification: <https://protobuf.dev/reference/protobuf/proto3-spec/>

## Overview

In gRPC, a client application can directly call a method on a server application on a different machine as if it were a local object.

As in many RPC systems, gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types.

On the server side, the server implements this interface and runs a gRPC server to handle client calls.

On the client side, the client has a stub (referred to as just a client in some languages) that provides the same methods as the server.

## Protocol Buffers

Google’s mature open source mechanism for serializing structured data.

The first step when working with protocol buffers is to define the structure for the data you want to serialize in a proto file: this is an ordinary text file with a .proto extension. Protocol buffer data is structured as messages, where each message is a small logical record of information containing a series of name-value pairs called fields.

```proto
message Person {
  string name = 1;
  int32 id = 2;
  bool has_ponycopter = 3;
}
```

Then, once you’ve specified your data structures, you use the protocol buffer compiler protoc to generate data access classes in your preferred language(s) from your proto definition. These provide simple accessors for each field, like name() and set_name(), as well as methods to serialize/parse the whole structure to/from raw bytes.

```proto
// The greeter service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```

## Python

<https://grpc.io/docs/languages/python/basics/>

### Generating client and server code

```bash
python -m grpc_tools.protoc -Iproto --python_out=stubs --pyi_out=stubs --grpc_python_out=stubs proto/bio.proto
```
