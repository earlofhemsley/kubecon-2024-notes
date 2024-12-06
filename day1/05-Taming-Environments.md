# Making your applications cross-environment friendly

What's an environment?
 - a local machine?
 - docker compose?
 - Kind cluster?
 - VM?
 - CI pipeline?

The answer to this question is it's complicated.

In their demo, they have a producer and consumer, connected with RabbitMQ. The Rabbit MQ is provisionsed by docker compose.

## What all environments share

- A runtime
- An infrastructure required by the app runtime
- Infra configuration
- Orchestration of their lifecycles
    - This is managed manually in a local, and in a much more automated fashion in a cloud

The way to resolve this is through APIs

## Here's the pitch: Dapr

It's an api layer that is consistent across environments. It's middleware. Dapr sits between your application and your environment.

It abstactifies away the environment away from the infrastructure underneath. Dapr connects api endpoints to various providers, and engineers write their application code against a monolithic api provided by Dapr.

This is a pretty good idea because it disconnects the application runtime from the underlying infrastructure. If every interaction is abstracted away from the environment via an api and a middleware that sits between the application and the environment infrastructure, then the application doesn't have to worry about integrating with specific technologies or apis.

## Dagger?

Not sure what this is, but it was a logo that flashed on the screen

Today's CI/CD problems, as we deploy things through environments, look a lot like old application problems, according to them.

They aim to standardize the SDLC, which is to say they are trying to abstractify the DevOps processes enough such that everyone can use the same apis and abstractions to deploy their applications regardless of the providers underneath.

dagger is written in golang.

The remainder of the presentation was demoing their software. [dagger.io](https://dagger.io/)
