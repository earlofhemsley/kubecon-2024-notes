# Platform Engineering for Software Devs and Architects

In platform engineering, your customer is software engineers

## PaaS

Golden Paths. Develop the platform. Make the platform the product consumed by 

Developer codeplane. 

Clutch and Backstage ... sample tools that manage things end to end

### What is a platform?

> A digital platform is a faoundation of self-service APIs tools, services, knowledge and support which are arranged as a compelling internal product. Autonomous delivery teams can make use of the platform to deliver product features at a higher pace with reduced coordination. 
- Matt Bottcher

### What are the goals of the platform?

- Go faster ... provide value
- Decrease risk by making reusable components
- Increase efficiency ... manage at scale

#### Books
Team Topologies by Matthew skelton and manuel apis

Platform strategy by Gregor Hohpe

Software Architect Elevator by Gregor Hohpe
- You have to use the right language for the right part of the building
- Meet people where they're at

### Platform layers

Application coreography - Clearly in the realm of App developers
Platform Orchestration - Provide "x as a service" ... platform abstractions and apis that can be consumed (argo/flux) and that have actual impact on the infra
Infrastructure/Composition - Clearly in the realm of sysadmins

Book: Infrastructure as Code by Kief Morris
Book: Platform Engineering by Camille Fournier

## Architecture case studies

Hexagonal architecture ... you can create cohesive business code with interfaces into the platform layers ... this is app dev as i know it
- mocking for tests
- loose coupling ... possible to swap out technologies

Software Solutions ... provide SDKs for different languages to interface with platform components ... Dapr/Dagger is an example because it abstractifies cloud providers away, making it far more platform independent

## Microservices

Create cohesive business functional units to reduce blast radius, among other things
Requires
 - rapid provisioning
 - Basic monitoring
 - rapid deployment

"distributed monolith" ... without all the components, the system doesn't work

devops ... you build it, you run it ... what about visibility, security, upgrades, etc.
great as a principle, but you often need some centralization for things like security and observability

## Infrastructure solutions

Heroku! Cloud Foundry! Except the applications didn't always scale. 

"Puppy for christmas!" Day one is exciting, but day two is not so fun.

## Platform Solutions

Platform orchestrators ... Kratix, KusionStack, Humanitec
Dev-configurable CI/CD ... Dagger (less terraform, more code)

## Cell based architecture

An evolution of microservices. Lower blast radii. Proofing isolation.  [book](infoq.com/minibooks/cell-based-architecture-2024)

## Key insights

Principles matter: SOLID, CUPID, principle of least surprise ... these are just as important when it comes to paltforms

Devs don't want magic. They want to be magicians.

Size of spell (abstractions) matters too

You can't have good devex without having good ux
- design api, then cli, then ui
- optimize for automation
- minimize cognitive load
- [build for progressive disclosure](syntasso.io/post/when-backstage-met-terraform-and-platform-orchestrators-webinar-recap)
    - this is the idea that you shouldn't just dump full k8s config files on unsuspecting engineers who don't know how to manage them or what to do with them

Don't forget the product focus

*What gets measured gets managed*
- impact metrics
- guardrail metrics
- product health metrics "are folks adopting my platform"
- lagging vs leading metrics
    - leading
        - adoption rates
        - onboarding times
    - lagging
        - retention
        - patch cycle resourcing
        - change fail percent
        - speed of delivery

goldilocks zone: devex framework
- [DORA](https://devops.com/what-is-dora-and-why-you-should-care/)
- [SPACE](https://getdx.com/blog/space-metrics/)
- DevEx

Developers are customers of the platform
- Speed
- Safety
- Scale
- Enable APIs, CLI, UI (portals)

This is a team sport

APIs, abstractions, and automation is key. Coupling and cohesion are universal concepts. Golden paths vs Golden Bricks.
- Golden Paths can quickly become a golden cage. There's only one way to do things. Having composable units drive platform architecture can probably be better.
