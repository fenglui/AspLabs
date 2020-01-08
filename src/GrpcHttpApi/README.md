ASP.NET Core gRPC HTTP API
==========================

This project is an extension for ASP.NET Core gRPC server that allows RESTful HTTP APIs for gRPC endpoints. HTTP API concepts like a URL parameter binding, HTTP verbs and JSON request/response can be used to invoke gRPC services.

### Usage:

1. Add a package reference to `Microsoft.AspNetCore.Grpc.HttpApi`.
2. Register services in *Startup.cs* with `AddGrpcHttpApi()`.
2. Include `<Protobuf>` reference to *google/api/http.proto* and *google/api/http.proto*.
3. Annotate gRPC methods in your *.proto* file with your HTTP bindings and routes:

```protobuf
syntax = "proto3";

import "google/api/annotations.proto";

package greet;

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {
    option (google.api.http) = {
      get: "v1/greeter/{name}"
    };
  }
}

message HelloRequest {
  string name = 1;
  string test_name = 2;
}

message HelloReply {
  string message = 1;
}
```

The `SayHello` gRPC method can now be invoked with Protobuf+gRPC and with `GET /v1/greeter/world` to return `{ "message": "Hello world" }`. See [HttpRule](https://cloud.google.com/service-infrastructure/docs/service-management/reference/rpc/google.api#google.api.HttpRule) for more customization options.

### Experimental project

This project is experimental. It is not complete or fully tested. There is no commitment to completing it.

We want to gauge developer interest in gRPC+HTTP API. If gRPC+HTTP API is interesting to you then please give feedback.
