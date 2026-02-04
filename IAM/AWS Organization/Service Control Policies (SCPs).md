A Service Control Policy (SCP) is a type of organizational policy within AWS Organizations that provides **centralized control over the maximum available permissions** for all accounts in your organization. Think of an SCP as a **"guardrail"** or a master switch that sets the boundaries for what's allowed.

---

## How SCPs Work

An SCP does not grant permissions. Instead, it **filters and restricts** the permissions that can be granted by standard IAM policies. This means that even if an IAM policy allows a specific action, an SCP attached to the account or a parent Organizational Unit (OU) can explicitly deny it.

SCPs control the permission or policy which is allowed to user through IAM policy at Account level

The evaluation logic follows a strict "deny-by-default" model:

1. **Implicit Deny:** By default, all actions are implicitly denied unless a policy allows them.
    
2. **Explicit Deny:** If any SCP in the hierarchy (from the root down to the account) has a `Deny` statement for an action, that action is forbidden for all users and roles in that account, regardless of any `Allow` statements in other policies.
    
3. **Allow:** For an action to be permitted, it must be explicitly allowed by both an IAM policy **and** all applicable SCPs in the account's hierarchy.
    

### Key Characteristics:

- **Hierarchical Inheritance:** SCPs are applied at the root of your organization, to OUs, and to individual accounts. Policies applied at a higher level are inherited by all accounts and OUs below them.
    
- **Affects All Principals:** SCPs apply to all IAM users and roles in member accounts, including the root user of the account. They do not affect service-linked roles.
    
- **JSON Format:** SCPs are written in JSON, similar to IAM policies, using `Effect`, `Action`, `Resource`, and `Condition` elements to define their rules.
    
- **Two Strategies:** You can use an **allow list** strategy (everything is denied except for what's explicitly allowed) or a **deny list** strategy (everything is allowed except for what's explicitly denied). The default `FullAWSAccess` SCP allows all actions, which is the starting point for a deny list strategy.
    

Creating an AWS Service Control Policy is a video that walks through the process of creating an SCP and applying it to an organizational unit to see its effect.

### Three Layer for policy
1. **The root level**
2. **Organizational unit (OUs)**
3. **Individual account**

When you first create an organization, a default Service Control Policy (SCP) called `FullAWSAccess` is automatically created and attached to the root of your organization

This means that when you add a new account to your organization, it inherits the `FullAWSAccess` SCP from the root

**There is an alternative strategy:** You can detach the default `FullAWSAccess` SCP from the root. When you do this, the root, and all OUs and accounts below it, will have an **implicit deny**. In this case, you would use an **allow-list** strategy by explicitly attaching SCPs that permit only the necessary actions. This is often used in highly regulated or security-focused environments.

- **Key Principle:** The most restrictive policy always wins. An explicit `Deny` in an SCP will override any `Allow` statement in an IAM policy or another SCP.