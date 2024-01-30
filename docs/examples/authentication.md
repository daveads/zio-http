---
id: authentication
title: "Authentication Example"
sidebar_label: "Authentication"
---

## Authentication Server Example

```scala mdoc:passthrough
import utils._
printSource("zio-http-example/src/main/scala/example/AuthenticationServer.scala")
```

## Authentication Client Example

```scala mdoc:passthrough
import utils._
printSource("zio-http-example/src/main/scala/example/AuthenticationClient.scala")
```

## Middleware Basic Authentication Example

Basic authentication is a method of enforcing access control to an HTTP server by requiring clients to provide valid credentials.

This code demonstrates how to configure an HTTP server with basic authentication:

```scala mdoc:passthrough
import utils._
printSource("zio-http-example/src/main/scala/example/BasicAuth.scala")
```