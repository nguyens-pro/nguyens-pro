# A/B Testing with LaunchDarly
[LaunchDarkly](https://launchdarkly.com) is a feature management and experimentation for banking, payments, insurance, and wealth management firms.
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

## Problem Statement
We'd like to understand user behaviors when the feature A is replaced by a new one, B.
* The user segment to be tested is Norwegian users.
* The distribution rate for users in the segment is 50/50.
* The metrics (mesurement) include the rate of user interactions to the new feature.

## Step 1: Create a feature flag
A feature flag is to control whether we should show feature A (usually the current behavior) or feature B (the new behavior) during the testing period. Using a feature flag, we could isolate the logic controlling the switch that may depend on different criteria like user type, characteristics, and environment.
```
User Context ----> Feature Flag 1 ----> Rule 1 ----> A
                       |                  |
                       |                  |--------> B
                       |
                       |--------------> Rule 2 ----> A
                       |                  |
                       |                  |--------> B
                       |
                       |--------> Default Rule ----> A
```
1. Log in to the LaunchDarkly Dashboard
2. Navigate to **Flags** tab
3. Select **Create Flag** button
4. Name the flag with corresponding key and description
5. Select **Experiment** as the flag configuration
6. Select **Boolean** as the flag type
7. Name the **Variations** with
    - Variation: "Feature A (Current)"; Value: false; Description: "Current feature"
    - Variation: "Feature B (New)"; Value: true ; Description: "New feature"
8. Set the **Default variations** to
    - Serve when targeting is ON: "Feature B (New)"
    - Serve when targeting is OFF: "Feature A (Current)"
9. Under **Client-side SDK availability** section, select:
    -  **SDKs using Mobile key**
    -  **SDKs using Client-side ID**
10. Save the flag

## Step 2: Create a segment
A segment is to build groups for the A/B testing. The groups could be determined by rules or by listing out member contexts. Segments will be referenced by the feature flag as the A/B testing targets.
```
User Context ----> Segment 1 ----> Rule 1 ----> Included
                       |             |
                       |             |--------> Excluded
                       |
                       |---------> Rule 2 ----> Included
                                     |
                                     |--------> Excluded
```
1. Log in to the LaunchDarkly Dashboard
2. Navigate to **Segments** tab
3. _Select an appropriate environment if necessary_
4. Select **Create Segment** button
5. Select **Rule-based segments** as the type
6. Name the flag with corresponding key and description
7. Add the first rule to the segment:
     - Name: Users from Norway
     - Condition: user -> country -> is one of -> NO
     - Include: all targets
8. Save the flag

## Step 3: Connect the flag and the segment

## Step 4: Create a metric
Metrics refer to the data and insights collected regarding the performance and usage of feature flags within an application. LaunchDarkly provides a set of metrics and analytics tools to monitor the impact of feature changes align with the business goals.
```
App Event  ---->  Metric 1  ---->  event key  ---->  recorded (count)
                     |                 |
                     |                 |---------->  ignored (no count)
                     |
                     |---------->  refresh data and insights
```
1. Log in to the LaunchDarkly Dashboard
2. Navigate to **Metrics** tab
3. _Select an appropriate environment if necessary_
4. Select **Create** -> **Create metric** to create a new metric
5. Select **Custom** as the event type
6. Enter the key of the event to be measured
7. Select **Count** (Number of times an event occured) to measure
8. Select **Metric definition** as:
     - **Average** of event `count` per **userId** where **higher is better**
9. Name the metric with a corresponding key
10. Save the metric

