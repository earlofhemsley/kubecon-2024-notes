# SLSA Compliant Supply Chain Security

## Why is supply chain security important?

61% of US businesses were impacted by attacks between 22 and 23

The SolarWinds hack was one of these attacks. Everything they built for a while was rife with malicious code. 18k orgs impacted.

## What is SLSA?

Security Levels for Software Artifacts ... open framework for security software builds/packages/containers

"Provenance" is an attestation. i.e. validation that something is actually what it claims to be. details about when and where it was built.

The threats involved are attacks against source code (unauthorized changes, compromising a source repo), dependency attacks (a dirty lib is pulled into a build) and others.

There are security levels associated with SLSA that basically are different standards of "hardness" of builds. L3 is the gold standard. (SLSA 1.0 really only deals with build threats).

## Implementation

[this is the repo and sample implementation](https://github.com/AEnguerrand/kubecon-cloudnativecon-na-2024-supply-chain-security-lab)

The slides talk about the various dependencies in more detail. Reference the github repo to review the dependencies involved with this lab.

### Sigstore

`cosign sign image` ... this command can be run in a github job

when you do this, you get a cert from soemthing like fulcio, which is published onto rekor. The image is pushed to a registry. When the image is used, the authenticity of the integrity of the image can be checked against the certificate uploaded to rekor. Look at the github action logs in the sample implementation. You can see these steps inside of a job logs, which are public.

`in-toto` is an open framework for building attestations. it uses these tools, and platforms like npmjs are capable of supplying this "provenance" to consumers to prove that the library is what it says it is. [he uses a github action](https://github.com/AEnguerrand/kubecon-cloudnativecon-na-2024-supply-chain-security-lab/blob/main/.github/workflows/docker.yaml) on the marketplace for provenance. It's [this one](https://github.com/actions/attest-build-provenance).

The thing that enforces the security policy on the k8s cluster side of this is `kyverno`. it will enforce signature validation on containers. It does this with a k8s manifest. Example in the slides. Kubescape provides continuous analysis on the images in the cluster also.

## Going further with Hardware Security Module

Lots of good definitions on this slide about the various components that are involved re: certs (fulcio)
