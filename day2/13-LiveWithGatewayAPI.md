# Live w Gateway API

## Brief description of ingress problem

How do you let people use your services?

Users want to use things in the cluster, but clusters do not allow this by default.
We need something to sit between the cluster and user to mediate ingress.
The first problem for anyone developing in cloud native
No way to solve problems without also solving the ingress problem
Gateway API tries to solve this problem in a standardized way
"Small and narrowly scoped is the opposite of the ingress problem"

Problems:
- monolithic ... the app devs have to highly trust platform engineers, and they stomp all over each other in a resource that is prone to misconfiguration
- limited ... often extensions get involved
- not extensible ... there are no standardized patterns, so home-brew stuff popped up all over without any intelligent, common framework available

## Gateway API

A project w/in K8s SIG network
Started in 2020 as "ingress v2"
In GA in 2023, actively maintained

## Features

Roles within Gateway API
- Infra providers ... AWS
- Cluster operator ... Platform eng team ... cluster is a shared resource to many app dev teams
- App Devs ... They don't want to think about the infra underneath the application. They just want to be engineers on their own business applications

Standard, generic api for common functionality

Extensible for all your needs

Traffic splitting ... route % to `foo-new` and % to `foo-old`. (Canary deployments)

Dynamic request routing ... AB testing ... per user canaries ... progressive delivery
- Headers
- Method
- Path & Query
- Not body!

Both HTTP and gRPC ... similar resources b/c similar requests ... available as of v1.1.1 ... gRPC routes are a bit different in how they're handled as opposed to HTTP, so it's a separate class

## Should I start using it now?

New ingress or service mesh deployment? Consider using Gateway API.
Existing stable deployment? Learn concepts and plan for the future

## Demo

**WORKING DEMO**: [gateway-api-workshop](https://github.com/earlofhemsley/gateway-api-workshop/tree/main)

Pay special attention to the installation instructions. Get all of the dependencies installed.

Demo time! 

faces demo repository ... https://github.com/BuoyantIO/faces-demo

## Gateway API and Gamma

The GAMMA initiative is part of gateway API. Both istio and linkerd use Gateway API

Note: If you don't include a service type, it's going to assume `gateway` by default. If you want to send it to a service you have to specify the service.

Working on Retries, timeouts and rate limiting

## Gotchas

If something goes wrong, check the status first. Reporting common errors in a standardized way.

```
kubectl get httproute {name} -o yaml | yq .status
```

Route stacking not allowed. When a request comes in at a route for a specific service, the routing decision is made once, and the request is routed. Subsequent routing rules will not be applied

https://github.com/kubernetes-sigs/gateway-api

https://gateway-api.sigs.k8s.io


