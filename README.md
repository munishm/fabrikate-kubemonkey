# fabrikate-kubemonkey

This repository is high level deployment definition for Kubemonkey implementation by [astobi/kubemonkey](https://github.com/asobti/kube-monkey) 

kube-monkey is an implementation of Netflix's Chaos Monkey for Kubernetes clusters. It randomly deletes Kubernetes (k8s) pods in the cluster encouraging and validating the development of failure-resilient services.

More details for Kubemonkey is available at https://github.com/asobti/kube-monkey


## Deploy

Kubemonkey can de deployed via Microsoft [Fabrikate](https://github.com/Microsoft/fabrikate)
Fabrikate will take this high level definition and will render the Kubernetes resource manifest for the kubemonkey.

> Requires at least [0.1.4](https://github.com/Microsoft/fabrikate/releases) or later of [Fabrikate](https://github.com/Microsoft/fabrikate).

## Configure

kube-monkey is configured by environment variables or a toml file and expects the configmap to exist before the kubemonkey deployment.

Example config file:

```yaml
[kubemonkey]
dry_run = true                           # Terminations are only logged
run_hour = 8                             # Run scheduling at 8am on weekdays
start_hour = 10                          # Don't schedule any pod deaths before 10am
end_hour = 16                            # Don't schedule any pod deaths after 4pm
blacklisted_namespaces = ["kube-system"] # Critical apps live here
time_zone = "America/New_York"           # Set tzdata timezone example. Note the field is time_zone not timezone
```
This example runs the kubemonkey at scheduled time 8AM, start the pod deaths from 10 AM- 4 PM, New York time zone and will not run on kube-system namespace.  





The corresponding Fabrikate configuration can be done via the config common.yaml file as

```yaml
dryRun = true                           # Terminations are only logged
runHour = 8                             # Run scheduling at 8am on weekdays
startHour = 10                          # Don't schedule any pod deaths before 10am
endHour = 16                            # Don't schedule any pod deaths after 4pm
blacklistedNamespaces = ["kube-system"] # Critical apps live here
timezone = "America/New_York"           # Set tzdata timezone example. Note the field is time_zone not timezone
debug:
    enabled: false # if you want to enable debugging and see how pods killed immediately set enabled and                                   schedule_immediate_kill to true
    schedule_immediate_kill: false
```




