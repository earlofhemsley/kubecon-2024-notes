# Software supply chain security

Pre-Build onboarding -> Build & Integrations -> Post-Build Deployment -> Post-Deployment Operations

Each of these layers - processes, workflows, people - and processes need to be secured
In return, you get integrity, security and trust

## General process for a secure CI/CD pipeline, start to finish

Reference Architecture
In github, you should have
 - App repo
     - CI spec ... logic and local dev support
 - Deployment configuration
     - CD spec ... CD steps, environments, deployments, stateful infra, observability, monitoring, etc.
 - Platform defined templates that marry CI with CD
 
 PR process
 - static analysis
 - quality checks
 - unit tests
 - signed commit validation (!)
 - scanning for secrets,
 - owasp protection, etc.

When PR is raised, CI pipeline executes
 - Prebuild tests
 - Provisioning of resources
 - A build to create an artifact ... the finished thing that will move through environments
 - scan the artifact for vulnerabilities
 - integration tests, security tests, load testing, pen testing
 - sign the artifact
 - push the artifact to an artifact store

Once the artifact is pushed, it's time to roll it out
 - change request to update the artifact version in various envs
 - pre-deploy validations
 - provision resources
 - update caches (replication across regions) ... artifacts that are pulled are pulled from this cache, not the original store
 - deploy and wait
 - post deployment testing
 - notify the user that the deployment has succeeded (slack, etc.)

AI value cases include analysis of failure logging, pattern detection in deployments, log analysis, test selection, vulnerability scanning, anomaly detection, etc.

## Adobe's implementation

They just went through the technologies they use at adobe for CI/CD

## Sealed Paved Roads

Concept ---------------> Code ----------------------------> Cloud ------------------> Customer
        Bootstrap     Hello World    CI/CD pipeline      Deployed, Observability

Reference the slide for more details. The idea is that there is a defined route through which code makes its way to the customer in a secure way.

But why sealed?
 - Opinionated
 - Best Practices Included
 - Enforcements
 - Resonable Defaults
 - Abstractions

## Autodesk

Their CI/CD is essentially the same, except that they have a diverse array of tech and needed something that was going to be able to wrap them effectively

They highlight ideation as an early phase of the SDLC.

They allow users of the CI/CD platform to define what the steps look like, but they can't skip any steps. "Set your own rules, but your rules will be applied"

Use of high-level abstractions not maintained by consuming teams means that they get the benefits of the abstraction with the dedicated security and attention that comes from having a team dedicated to platform development.

### CI/CD telemetry

They obtain and pour data at every stage of their CI/CD pipelines into a data lake. Full visibility on CI/CD telemetry, etc.

They have tooling that allows them to verify and witness that each individual stage actually occurs, cryptographically signed and sent into a data lake. This allows them to irrefutably verify that each individual stage actually occurs. There is evidence of a commit, a build, a push, etc. Each action is "witnessed" and sent into a data lake that is exposed behind a graphql api.

this allows them to analyze their pipelines, spot weaknesses, make improvements, and verify deployments, etc.


## Takeaways

Supply chain security is table stakes. Secure continuously.

Don't rely on people to secure things. make it easy. Create sealed paved roads for other eng

improving security is an iterative process. Start with the most important concerns

CI & CD are not the same thing. Separate them!
