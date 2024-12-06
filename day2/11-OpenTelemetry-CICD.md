# OpenTelemetry in CICD

It's about measuring health. They are using health & fitness apps as an analog to observability in CICD

## Challenges in Modern CI/CD

Very complex tools. Getting visibility is important.

OpenTelemetry receiver for GitLab.

## CI/CD at Clario (presenter's implementation)
- Gitlab
- Docker Image build
- Prerelease
    - Security scan
    - Deployment to test env
    - code analysis
- deploy built image to prod

They wanted visibility in all of this, which is a good use case for opentelemetry

In their pipeline, they have a otel export job, and then the otel export sends it down the line to the collectors, etc. that put the metrics into something like splunk/datadog

## OpenTelemetry Collector

They use gitlab webhooks as a trigger. This allows them to move logic out of the pipeline job, and move the heavy lifting into the collector.

The OTel collector is the key in this. It is custom and isn't publicly available, but they are thinking of releasing the implementation of their collector publicly

## Benefits

Having the telemetry can allow you to visualize and see if something is an outlier in terms of performance.

Alerts and notifications for exceptionally bad builds can be configured.

Allows for tracing of specific releases through environments. Easier to answer ... "Hey, what is deployed?" and "What was the change that prompted the behavior I'm seeing?"

## Other notes

OpenTelemetry supports CI/CD annotations.

There is already a GitHub receiver available out there somewhere.

What end-to-end processes do you have that you can monitor and visualize using open telemetry?
