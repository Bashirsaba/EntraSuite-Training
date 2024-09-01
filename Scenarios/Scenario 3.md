## Microsoft Entra Suite � Scenario 3

## Govern internet access based on business needs (Secure and governed access to all applications and resources)

## Introduction
In this guide, we describe how to configure Microsoft Entra Suite products for a scenario in which the fictional organization, Contoso has strict default internet access policies and wants to control internet access according to business requirements.

In an example scenario for which we describe how to configure its solution in this guide, a Marketing department user requires access to social networking sites that Contoso prohibits for all users. Users can request access in [My Access](https://learn.microsoft.com/en-us/entra/id-governance/my-access-portal-overview). Upon approval, they become a member of a group that grants them access to social networking sites.

In another example scenario and corresponding solution, a SOC analyst needs to access a group of high-risk internet destinations for a specific time to investigate an incident. The SOC analyst can make that request in My Access. Upon approval, they become a member of a group that grants them access to high-risk internet destinations. 

You can replicate these high-level steps for the Contoso solution as described in this guide.
1.	Sign up for Microsoft Entra Suite. Enable and configure Microsoft Entra Internet Access for desired network and security settings.
2.	Deploy [Microsoft Global Secure Access clients](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-clients) on users� devices. Enable Microsoft Entra Internet Access.
3.	Create a security profile and web content filtering policies with a restrictive baseline policy that blocks specific web categories and web destinations for all users.
4.	Create a security profile and web content filtering policies that allows access to social networking sites.
5.	Create a security profile that enables the Hacking web category. 
6.	Use [Microsoft Entra ID Governance](https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-overview) to allow users requesting access to access packages such as: 
    * Marketing department users can request access to social networking sites with a quarterly access review. 
    * SOC team members can request access to high-risk internet destinations with a time limit of eight hours.
7.	Create and link two [Conditional Access policies](https://learn.microsoft.com/en-us/entra/identity/conditional-access/plan-conditional-access) using the Global Secure Access security profile session control. Scope the policy to groups of users for enforcement.
8.	Confirm that traffic is appropriately granted with traffic logs in Global Secure Access. Ensure that Marketing department users can access the access package in the My Access portal.
These are the benefits of using these solutions together:
    * **Least privilege access to internet destinations**. Reduce internet resource access to only what the user requires for their job role through the joiner/mover/leaver cycle. This approach reduces end user and device compromise risk.
    * **Simplified and unified management**. Manage network and security functions from a single cloud-based console, reducing complexity and cost of maintaining multiple solutions and appliances.
    * **Enhanced security and visibility**. Enforce granular and adaptive access policies based on user and device identity and context, as well as app and data sensitivity and location. Enriched logs and analytics provide gain insights into network and security posture to more quickly detect and respond to threats. 
    * **Improved user experience and productivity**. Provide fast and seamless access to necessary apps and resources without compromising security or performance

## Requirements
This section defines the requirements for the scenario solution.

### Permissions

Administrators who interact with Global Secure Access preview features require the Global Secure Access Administrator and Application Administrator roles.

Conditional Access (CA) policy configuration requires the Conditional Access Administrator or Security Administrator role. Some features may require additional roles.

Identity Governance configuration requires at least the Identity Governance Administrator role.

### Licenses
To implement all the steps in this scenario, you need Microsoft Entra ID P1 for Global Secure Access (while the product is in Public Preview) and Microsoft Entra Governance licenses. You can [purchase licenses or obtain trial licenses](https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing).

### Users and devices prerequisites
To successfully deploy and test this scenario, configure for these prerequisites:

1.	Microsoft Entra tenant with Microsoft Entra ID P1 license. Configure Microsoft Entra ID P2 to test Identity Protection. Purchase licenses or obtain trial licenses.
    * One user with at least Global Secure Access Administrator and Application Administrator roles to configure Microsoft's Security Service Edge
    * At least one user as client test user in your tenant
2.	One Windows client device with this configuration:
    * Windows 10/11 64-bit version
    * Microsoft Entra joined or hybrid joined
    * Internet connected
3.	Download and install Global Secure Access Client on client device. The [Global Secure Access Client for Windows](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client) article describes prerequisites and installation.

## Configure Global Secure Access
In this section, we activate Global Secure Access through the Microsoft Entra admin center. We then set up the required initial configurations for the scenario.

1.	Sign in to the Microsoft Entra admin center with at least a Global Administrator role.
2.	Go to **Global Secure Access > Get started > Activate Global Secure Access in your tenant**. Select **Activate** to enable SSE features.
    ![imagen 1](../images/IA-01.png)
3.	Go to **Global Secure Access > Connect > Traffic forwarding **. Toggle on Private access profile. Traffic forwarding enables you to configure the type of network traffic to tunnel through Microsoft�s Security Service Edge Solution services. Set up [traffic forwarding profiles](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-traffic-forwarding) to manage traffic types. 
    * The **Microsoft 365 access profile** is for Microsoft Entra Internet Access for Microsoft 365. 
    * The **Private access profile** is for Microsoft Entra Private Access. 
    * The **Internet access profile** is for Microsoft Entra Internet Access. Microsoft's Security Service Edge solution only captures traffic on client devices with Global Secure Access Client installation.
    ![imagen 1](../images/IA-02.png)


