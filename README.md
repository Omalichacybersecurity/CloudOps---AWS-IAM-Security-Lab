# CloudOps---AWS-IAM-Security-Lab
# Securing AWS Accounts and Resources with IAM

# Repository Description

This repository documents my hands-on learning experience from an AWS Security Lab, where I explored the features of AWS Identity and Access Management (IAM) and related services.

The goal of this lab was to strengthen AWS account security by:

Managing user identities and roles with IAM

Applying multi-factor authentication (MFA)

Exploring IAM Identity Center (formerly AWS SSO)

Using IAM Access Analyzer to detect and remediate unintended access

Managing accounts at scale with AWS Organizations

This project demonstrates how I apply best practices in cloud identity and access management, a critical component of cloud security engineering.

# Scenario

As a Cloud Security Engineer, I was tasked with protecting an AWS environment by:

Enforcing least privilege access for users and services

Adding extra layers of authentication with MFA

Detecting public and cross-account permissions

Centrally managing multiple accounts

The lab provided a guided environment to practice securing AWS resources against unauthorized access.

# Step 1: IAM User & Group Management

Created IAM users for team members.

Organized users into groups (e.g., Admins, Developers, Auditors).

Attached IAM policies granting least-privilege permissions.

Example Policy (Read-Only Access to S3):

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:Get*", "s3:List*"],
      "Resource": "*"
    }
  ]
}


✔ Why: This ensures users have only the permissions they need — reducing risk of accidental or malicious misuse.

# Step 2: Multi-Factor Authentication (MFA)

Enabled MFA for the root user (best practice).

Required IAM users to configure virtual MFA devices (e.g., Google Authenticator).

✔ Why: MFA adds a second layer of protection, preventing account compromise if passwords are stolen.

# Step 3: IAM Identity Center (AWS SSO)

Configured AWS IAM Identity Center for centralized sign-in.

Assigned users single sign-on (SSO) access to multiple AWS accounts.

Mapped groups to IAM roles with tailored permissions.

✔ Why: Identity Center simplifies user management and ensures consistent, centralized access control across accounts.

# Step 4: IAM Access Analyzer

Ran IAM Access Analyzer to identify resources with public or cross-account access.

Found overly permissive S3 bucket policies and refined them.

Documented findings and applied least-privilege remediation.

✔ Why: Access Analyzer helps detect unintended exposure, protecting sensitive data from external threats.

# Step 5: AWS Organizations

Created an AWS Organization to manage multiple accounts.

Applied Service Control Policies (SCPs) to enforce security guardrails.

Example: Prevent disabling of CloudTrail logs across accounts.

Example SCP (Deny CloudTrail Deletion):

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyCloudTrailDeletion",
      "Effect": "Deny",
      "Action": [
        "cloudtrail:DeleteTrail",
        "cloudtrail:StopLogging"
      ],
      "Resource": "*"
    }
  ]
}


✔ Why: AWS Organizations ensures consistent governance and prevents risky security configurations.

# Step 6: Validation & Testing

Verified MFA enforcement by logging in as users without MFA → Access denied.

Tested SCPs by attempting restricted actions → Confirmed blocked.

Reviewed Access Analyzer findings to confirm no public S3 buckets remained.
s (Azure AD, Okta).
