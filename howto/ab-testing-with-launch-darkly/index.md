# A/B Testing with LaunchDarly
[LaunchDarkly](https://launchdarkly.com) is a feature management and experimentation for banking, payments, insurance, and wealth management firms.

## Create a feature flag
A feature flag is to control whether we should show feature A (usually the current behavior) or feature B (the new behavior) during the testing period. Using a feature flag, we could isolate the logic controlling the switch that may depend on different criteria like user type, characteristics, and environment.
```
Application -------- request w/ user data & environment --------> LaunchDarkly
                                                                        |
                                                                   perform pre-configured logic
                                                                        |
Feature A or B <--------- respond w/ the feature value <---------- pick value A or B
    in App
```
