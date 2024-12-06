# What if Kubernetes was a compiler target?

Tackling distributed systems is difficult. Multiple layers across several distributed systems.

The aim is to abstractify away some of this complexity ... what if you could write your app as a single program?

Multi-tier programming
- Dev writes the app as one application that gets compiled into a distributed system
- Logical "tiers" instead of individual components.
- The compiler then builds multiple deployable units

Example: Chat app using scalaloci

## Distributed component application frameworks

Under this approach to engineering, devleopers focus on business logic, the compiler and architecture orchestration focuses on managing all these components in a distributed system.

## What if we didn't have to worry about microservices?
## What if we could revert to the monolith style?

That's the idea here. The multi-tier program gets compiled into components that can run on a k8s cluster

"Companies that are building software think about writing software in tiers, but their software doesn't conform well to that"

## Key ideas

Goroutines ~> Kubernetes Pods
Channels ~> Network requests

## Demo
Kompile is the k8s compiler that they wrote.
They replace the channels in their sample golang code with http requests (they called it find and replace) and wrap goroutines in separate pods.

Another way of thinking of this is similar to "functions as a service." It's a slick way to roll your own functions by architecting applications in this manner

## Takeaways

There are programming paradigms we don't even know about yet.

K8s is the platform everything is running on.

How to we write our application to take advantage of that architecture in smart ways? Think outside the box!

