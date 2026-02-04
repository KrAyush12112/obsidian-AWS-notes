## 🔑 What is AWS Organizations?

- A **management service** for handling **multiple AWS accounts** under one roof.
- You get **centralized billing, governance, and policy control**.
- Instead of cramming everything into one account (messy, insecure), you split workloads into multiple accounts (prod, dev, sandbox, security, etc.) and still manage them together.
- The root account is called Organization
- This account pays all bill
## ⚙️ Core Components

1. **Management Account (a.k.a. Root Account)**
    - The first account that creates the organization.
    - Has full control (can invite/create other accounts).
    - Shouldn’t be used for workloads — keep it just for management/security.
2. **Member Accounts**
    - Accounts inside the org, created or invited.
    - They follow org-wide policies.
3. **Organizational Units (OUs)**
    - You can create and manage a hierarchy of accounts using **Organizational Units (OUs)**
4. **[[Service Control Policies (SCPs)]]**
    - Define and apply Policy at account or organizational level to restrict services and action.
    - SCPs do not grant permissions; instead, they define the maximum permissions available to an account, which helps enforce consistent security and compliance policies.

## 🚀 Key Features

- **Consolidated Billing** → All accounts share one bill, with combined discounts.
    
- **Account Creation** → Spin up new accounts programmatically with `CreateAccount`.
    
- **Centralized Control** → Apply SCPs to restrict services/regions.
    
- **Integration with AWS SSO/IAM Identity Center** → Central login across accounts.
    
- **Cross-Account Role Delegation** → Use one role across multiple accounts with trust.

## How to invite account under organization
Two ways to invite accounts into organization
	**1. Account creation**
		- You can directly create new account.
	**2. Invite existing AWS account**
		- You need to invite another account through there email.
		- You can send message through it to request join the organization.

	