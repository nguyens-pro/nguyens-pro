# A/B Testing with LaunchDarly
[LaunchDarkly](https://launchdarkly.com) is a feature management and experimentation for banking, payments, insurance, and wealth management firms.

## Problem Statement
We'd like to understand user behaviors when the feature A is replaced by a new one, B.
* The user segment to be tested is Norwegian users.
* The distribution rate for users in the segment is 50/50.
* The metrics (mesurement) include the rate of user interactions to the new feature.

## Create a feature flag
A feature flag is to control whether we should show feature A (usually the current behavior) or feature B (the new behavior) during the testing period. Using a feature flag, we could isolate the logic controlling the switch that may depend on different criteria like user type, characteristics, and environment.
```
Application   --------        request w/     -------->   LaunchDarkly
                      user data & environment                  |
                                                               |
                                                     pre-configured logic
                                                               |
                                                               |
Feature A or B <---------    respond w/   <----------  pick value A or B
    in App                the feature value
```
1. Log in to the LaunchDarkly Dashboard
2. Navigate to **Feature Flag** tab
3. Select **Create Flag** button
4. Name the flag with corresponding key and description.
5. Select **Experiment** as the flag configuration
6. Select **Boolean** as the flag type
7. Name the **Variations** with
    - "Feature A (Current)": false
    - "Feature B (New)": true
8. Set the **Default variations** to
    - Serve when targeting is ON: "Feature B (New)"
    - Serve when targeting is OFF: "Feature A (Current)"
9. Select **SDKs using Mobile key** under **Client-side SDK availability** section

