# Users and Roles

Our system provides a range of services for partner users.

The user groups associated with different providers are completely separate within the system.

TPartners may have access to the same features; however, the features and user permissions are configured individually for each partner.

## Types of end users

The table below outlines the basic types of end-user roles:

|User Type|Description|
|---|---|
|guest|Session length: 20 minutes<br/> Max. number of operations per day: 5<br/> Max. number of operations per week: 20. <br/> Transitions to Idle when the maximum number of operations per week is exceeded.|
|basic|KYC-verified client. Session length: unlimited<br/> Max. number of operations per day: 20<br/> Max. number of operations per week: 50. <br/> Transitions to Idle when the maximum number of operations per week is exceeded. |
|company| No limits |
|advanced| No limits |

## Role Model Diagram

```mermaid
graph TD
    subgraph Partners
        Partner1["Partner 1"]
        Partner2["Partner 2"]
        Partner3["Partner 3"]
    end
    
    subgraph Users
        Guest["Guest"]
        Basic["Basic"]
        Advanced["Advanced"]
        Company["Company"]
    end
    
    Partner1 -->|Configured Functions & Rights| Users
    Partner2 -->|Configured Functions & Rights| Users
    Partner3 -->|Configured Functions & Rights| Users

    Guest -->|KYC Procedure| Basic
    Basic -->|Upgrade| Advanced
    Advanced -->|Demotion| Basic
    Basic -->|Demotion| Guest
    Advanced -->|Transition| Company
    Company -->|Transition| Advanced
    
    classDef sessionLimit fill:#f9f,stroke:#333,stroke-width:2px;
    Guest:::sessionLimit -->|Session Limit: 20 minutes| Idle[Idle State]
    Idle -->|Action Restriction| Guest

    classDef limits fill:#aaf,stroke:#333,stroke-width:2px;
    Guest:::limits -->|Daily Ops Limit: 5| Basic
    Basic:::limits -->|Daily Ops Limit: 20| Advanced
    Guest -->|7-Day Ops Limit: 20| Basic
    Basic -->|7-Day Ops Limit: 50| Advanced
```

**Explanation:**

1. **Partners**:
   - Represented as separate nodes in the `Partners` section.
   - Each partner has a unique set of permissions and functions.

2. **Users**:
   - Represented by different types: `Guest`, `Basic`, `Advanced`, `Company`.
   - Specific limits and states are defined for each user type.

3. **Status Transitions**:
   - Illustrated with arrows showing the conditions for transitions between statuses.

4. **Restrictions**:
   - Special classes for session and operation limits are highlighted to emphasize key rules.