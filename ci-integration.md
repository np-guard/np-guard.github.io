There are several options to integrate the various components in this project into a useful CI/CD pipeline. One possible option is depiced below.

![CI-integration](ci-integration-option.png)

In this flow, the Analysis and Synthsis phase is manually triggered. This results in a new PR, containing the synthesized NetworkPolicies. This triggers running the other components which provide connectivity map, connectivity diff and policy verification results as PR comments.
