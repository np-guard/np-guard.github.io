---
title: CI Integrarion
---

There are several options to integrate the various components in this project into a useful CI/CD pipeline. One possible option is depicted below.

![CI-integration](ci-integration-option.png)

In this flow, the Analysis and Synthsis phase is manually triggered by a DevOps person. This results in a new PR, containing the synthesized NetworkPolicies. Opening the PR triggers running the other components which provide connectivity map, connectivity diff and policy verification results as PR comments.

To enable CI/CD integrations, this project provides several GitHub Actions as well as Tekton Tasks. Use the table below to get the relevant CI-stage encapsulation for your needs.

|CI stage|GitHub Action|Tekton Task|
|--------|-------------|-----------|
|Analysis & Synthesis|[link](https://github.com/marketplace/actions/k8s-networkpolicy-auto-synthesis)|[link](https://github.com/np-guard/netpol-synthesizer/tree/master/tekton)|
|Connectivity map|[link](https://github.com/marketplace/actions/k8s-networkpolicy-connectivity-report)|[link](https://github.com/np-guard/network-config-analyzer/tree/master/tekton#k8s-netpol-report)|
|Connectivity diff|[link](https://github.com/marketplace/actions/k8s-networkpolicy-diff)|[link](https://github.com/np-guard/network-config-analyzer/tree/master/tekton#k8s-netpol-diff)|
|Connectivity verification|[link](https://github.com/marketplace/actions/k8s-networkpolicy-verification)|[link](https://github.com/np-guard/baseline-rules-verifier/tree/master/tekton)|

An example implementation of the CI pipeline depicted above for a [demo Kubernetes application](https://github.com/np-guard/online-boutique) using our GitHub Actions can be found [here](https://github.com/np-guard/online-boutique/tree/master/.github/workflows). See a resulting PR [here](https://github.com/np-guard/online-boutique/pull/46).
