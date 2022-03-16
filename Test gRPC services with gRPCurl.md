# Test gRPC services with gRPCurl

The gRPC functions can only be called by gRPC clients. My team just started migrating to gRPC stack, and I found gRPCCurl is a very helpful CLI tool to test and debug. 

## Installation

```shell
brew install grpcurl
```



## Usage

Start your gRPC service and check the service metadata. My service is running on port of 10030.

Use "-plaintext" if your service does not use TLS.

```shell
grpcurl -plaintext localhost:10030 describe
grpc.health.v1.Health is a service:
service Health {
  rpc Check ( .grpc.health.v1.HealthCheckRequest ) returns ( .grpc.health.v1.HealthCheckResponse );
  rpc Watch ( .grpc.health.v1.HealthCheckRequest ) returns ( stream .grpc.health.v1.HealthCheckResponse );
}
grpc.reflection.v1alpha.ServerReflection is a service:
service ServerReflection {
  rpc ServerReflectionInfo ( stream .grpc.reflection.v1alpha.ServerReflectionRequest ) returns ( stream .grpc.reflection.v1alpha.ServerReflectionResponse );
}
sample_module.sample_package.SayHi is a service:
service SayHi {
  rpc SayHello ( .sample_module.sample_package.HelloRequest ) returns ( .sample_module.sample_package.HelloReply );
}
```

Call sample_module.sample_package.SayHi service.

```shell
grpcurl -d '{"msg": "jimmy"}' -plaintext localhost:10030 sample_module.sample_package.SayHi/SayHello
{
  "msg": "SayHijimmy",
  "code": "1"
}
```

