# Open Telemetry tutorials

Main goals of OTel are

- Unified telemetry ... an open standard
- Vendor neutrality ... integration with several different data backends
- Cross platform ... supports various programming languages

[Cloned a repo](https://github.com/lftraining/LFS148-code/tree/main/exercises/otel-in-action) into my local git folder .... LFS148-code

there is a docker-compose file here. docker compose up to run a bunch of stuff, and then you can explore traces in jaeger and metrics in prometheus

prometheus <-> grafana
jaeger <-> datadog/splunk

## Automatic instrumentation

attaching an agent in java: `java -javaAgent:./MyAgent.jar -jar MyApp.jar`

there are ways to do instrumentations with annotations in java if you want fine grained control. `@WithSpan`

the benefits of using method annotations for otel will automatically add more information (class name, namespaces, package names, etc.)

they have a list of notes called `allcommands.md`, but this file is not part of the repository, which will make replicating their demo quite difficult

it is also possible to add context by adding path variables, other in-code values into spans and traces as _tags_ with the `@SpanAttribute` annotation

this is valuable because it immediately becomes possible to filter requests by input values into your api

## Manual Instrumentation

Doing manual instrumentation really gets you up close with how this all works.
This involves calling api methods on instrumentation objects from an instrumentation SDK within application code. 
Highly customizable, but involves a lot of code. Prime candidate for aspect-oriented code
spands are processed in-app, and exported via a scan exporter, which are run on a thread inside of the application

Steps for configuring otel in a spring app
- add configuration class that provides an `OpenTelemetry` Bean, which comes from a library/sdk that I missed
    - span processor and span exporter are configured in this bean
- Instantiate a `Tracer` in classes where you want telemetry using the `OpenTelemetry` class as a dependency 
- use the tracer to start and end traces which are then exported via the `OpenTelemetry` configuration class
- nesting spans
    - spans can be started and ended inside of each method where instrumentation is desired
    - use try-w-resources-finally to associate spans with a scope ... lots of nesting in control blocks

## Linux Foundation Course associated with this code

[go here](https://training.linuxfoundation.org/training/getting-started-with-opentelemetry-lfs148/)

## Questions (just mine)
- there is no `manual-instrumentation-java` in the github repo
- will you post your slides to the agenda?
- thymeleaf/flask are good. Where to go to get resources on how to integrate otel into these frameworks like vue, react, angular?



