# Migrate-AppAccessPolicies

Script that creates RBAC management role assignments to match existing application access policies in Exchange Online

## Description
The high-level overview of what this script does is the following:

1. Gets a list of Application roles in Exchange Online
2. Gets a list of Graph API permissions that match the Exchange roles
3. Gets a list of Application Access Policies in Exchange Online
4. Loops through each of the policies and does the following:
    * Gets the application from Entra ID
    * Gets the SPN for the application in Entra ID
    * Checks for SPN in Exchange Online and creates one if needed
    * Checks for management scope in Exchange Online for the group used by policy and creates one if needed
    * Loops through each of the permissions in the Entra app and does the following:
        * Checks if the permission matches an Exchange Online role
        * Checks for a management role assignement using the SPN and role, create one if needed


## Requirements
1. The script requires an application registration in Entra ID that has the Graph API permission Application.Read.All
2. A connection to Exchange Online remote PowerShell with Exchange admin role

## Usage
Move an item from the Inbox to the Deleted Items folder using impersonation:
```powershell
.\Migrate-AppAccessPolicies.ps1 -PermissionType Application -OAuthClientId 1d5cdea4-32e6-1234-a35a-cc443d697cab -OAuthTenantId 9101fc97-5be5-4438-a1d7-83e051e52057 -OAuthCertificate 67DCA626D48EE1626623FF26E6C8D856262D1DDC -CertificateStore CurrentUser
```

## Parameters
**AzureEnvironment** - The AzureEnvironment parameter specifies the environment for the tenant (default is Global).

**PermissionType** - The PermissionType parameter specifies whether the app registrations uses delegated or application permissions

**OAuthClientId** - The OAuthClientId parameter specifies the app ID for the OAuth token request.

**OAuthTenantId** - The OAuthTenantId parameter specifies the the tenant ID for the OAuth token request.

**OAuthRedirectUri** - The OAuthRedirectUri specifies the redirect Uri of the Azure registered application.

**OAuthClientSecret** - The OAuthSecretKey parameter is the the secret for the registered application.

**OAuthCertificate** - The OAuthCertificate parameter is the certificate for the registered application.

**CertificateStore** - The CertificateStore parameter specifies the certificate store where the certificate is loaded.

**Scope** - The Scope parameter specifies the scope for the OAuth token request.