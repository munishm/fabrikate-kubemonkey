# fabrikate-kubemonkey

This repository is high level deployment definition for Kubemonkey implementation by [astobi/kubemonkey](https://github.com/asobti/kube-monkey) 


> Requires at least [0.1.4](https://github.com/Microsoft/fabrikate/releases) or later of [Fabrikate](https://github.com/Microsoft/fabrikate).

## Common Configs

Custom chart modifications:

```toml
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