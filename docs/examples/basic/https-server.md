---
id: https-server
title: Https Server Example
sidebar_label: Https Server
---

```scala mdoc:silent
import zio._

import zio.http._

object HttpsHelloWorld extends ZIOAppDefault {
  // Create HTTP route
  val app: HttpApp[Any] = Routes(
    Method.GET / "text" -> handler(Response.text("Hello World!")),
    Method.GET / "json" -> handler(Response.json("""{"greetings": "Hello World!"}""")),
  ).toHttpApp

  /**
   * In this example, a private key and certificate are loaded from resources.
   * For testing this example with curl, make sure the private key "server.key",
   * and the certificate "server.crt" are inside the resources directory,
   * which is by default "src/main/resources".
   *
   * You can use the following command to create a self-signed TLS certificate.
   * This command will create two files: "server.key" and "server.crt".
   *
   *     openssl req -x509 -newkey rsa:4096 -sha256 -days 365 -nodes \
   *       -keyout server.key -out server.crt \
   *       -subj "/CN=example.com/OU=?/O=?/L=?/ST=?/C=??" \
   *       -addext "subjectAltName=DNS:example.com,DNS:www.example.com,IP:10.0.0.1"
   */

  val sslConfig = SSLConfig.fromResource(
    behaviour = SSLConfig.HttpBehaviour.Accept,
    certPath = "server.crt",
    keyPath = "server.key",
  )

  private val config = Server.Config.default
    .port(8090)
    .ssl(sslConfig)

  private val configLayer = ZLayer.succeed(config)

  override val run =
    Server.serve(app).provide(configLayer, Server.live)

}

```