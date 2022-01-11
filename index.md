This project looks at the problem of simplifying the experience of creating and maintaining K8s NetworkPolicies for zero-trust environments. Recognizing how hard it is for users to create and manage K8s NetworkPolicies to enable just the right amount of connectivity (not more or less), we propose a solution to automating the generation of NetworkPolicies without having to run the applications' code. Our solution can be integrated into the application's CI/CD pipeline, ensuring NetworkPolicies get updated whenever the required cluster connectivity changes. The overall flow of the solution is presented below.

![Flow](flow.png)

The flow consists of two stages:
- **Automatic synthesis stage** - Analyzes application configuration files and takes into account existing network configuration, actual cluster traffic and baseline requirements. Proposes an updated network connectivity restrictions in the form of NetworkPolicy resources.
- **Review and modify stage** - The proposed network connectivity is presented to the DevOps persons for their review. The presentation can be graphic, a concise textual report, or simply the actual NetworkPolicy YAML files. The presentation also includes a semantic diff of connectivity changes from the currently-deployed configuration. Users can make changes to the proposed connectivity, and these changes are then checked against baseline requirements. Only approved changes get deployed to the live cluster.


Our [GitHub Org](https://github.com/np-guard) contains the source code for all components in the above flow (shown as elipsses). In particular it contains the following repos.
- [cluster-topology-analyzer](https://github.com/np-guard/cluster-topology-analyzer) - Scans a GitHub repo and extracts required network links from configuration files.
- [netpol-synthesizer](https://github.com/np-guard/netpol-synthesizer) - Synthesizes a set of K8s NetworkPolicies from the list of required network links and a set of baseline requirements.
- [network-config-analyzer](https://github.com/np-guard/network-config-analyzer) - Allows showing synthesized connectivity as a set of firewall rules. Can also produce connectivity diff between two network configurations.
- [baseline-rules-verifier](https://github.com/np-guard/baseline-rules-verifier) - Checks whether synthesized connectivity satisifies a set of baseline requirements.
- [baseline-rules](https://github.com/np-guard/baseline-rules) - Contains several [examples](https://github.com/np-guard/baseline-rules/tree/master/examples) for baseline requirements.

Check [CI Integration](https://np-guard.github.io/ci-integration.html) to learn how to integrate the above components into a CI/CD pipeline.
