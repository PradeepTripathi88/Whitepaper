Power Platform Governance & Architecture
1. Introduction
Microsoft Power Platform has become one of the fastest-growing low-code ecosystems across enterprises. It empowers organizations to automate business processes, build applications, analyze data, and design intelligent virtual agents with minimal technical effort. The suite includes Power Apps, Power Automate, Power BI, Power Pages, and Power Virtual Agents—all of which allow both technical and citizen developers to innovate at scale.
However, as adoption increases, enterprises face challenges in managing security, capacity, environments, licensing, and data governance. This expanded whitepaper explains the complete architectural and administrative model behind the Power Platform. It describes how tenants work, where environments sit, how licenses operate, how Dataverse capacity is allocated, and how Data Loss Prevention (DLP) policies secure data flows. Every section includes real-world examples and best practices that enterprises can follow to establish strong governance and operational excellence.
Understanding the architecture is crucial, especially for organizations with distributed teams, complex data boundaries, or strict compliance requirements. A properly governed tenant ensures that the organization can innovate rapidly while maintaining security, scalability, and control. This whitepaper provides a foundation for IT teams, architects, citizen developers, and administrators to build and operate Power Platform environments confidently and sustainably.
________________________________________
2. Microsoft 365 Tenant — Foundation of Power Platform
A Microsoft 365 tenant is the overarching security and administration boundary within Microsoft’s cloud infrastructure. When an organization purchases any Microsoft cloud product—Microsoft 365, Azure subscription, Dynamics 365, or Power Platform—a tenant is created automatically. This tenant becomes the home for all users, groups, domains, licenses, and Power Platform environments.
The tenant is powered by Microsoft Entra ID (formerly Azure Active Directory), which manages all identities, authentication, role assignments, and application access. All administrative configurations, such as user creation, license assignment, domain verification, and enterprise app registration, originate at the tenant level. Because the tenant acts as the root of trust, every service under the tenant ultimately inherits its security and compliance posture.
2.1 Characteristics of a Tenant
A tenant holds the identity directory, the purchased subscription information, and all administrative controls. It defines the organizational boundary for security, billing, compliance, and audit. For example, a Global Administrator in the tenant has full authority across all Power Platform environments, Azure AD configurations, and Microsoft 365 services.
2.2 Multiple Domains in One Tenant
Organizations often operate multiple domains for different subsidiaries, business units, or regions. Power Platform supports all these domains under one tenant. This allows users from different email extensions to collaborate, share applications, and be governed under one DLP policy model.
2.3 Multiple Tenants in One Organization
Enterprises may maintain separate tenants for mergers, geographic separation, or compliance needs. However, Power Platform environments cannot be shared across tenants. Solutions must be exported/imported manually, and user identities do not cross tenants.
________________________________________
3. Environments in Power Platform
Environments serve as containers for apps, flows, Dataverse tables, custom connectors, and DLP rules. They logically separate development, production, and departmental workloads. One tenant can have dozens or even hundreds of environments depending on governance strategy.
3.1 Types of Environments
•	Default Environment: Assigned to all users automatically. Suitable for personal productivity but not enterprise-grade apps.
•	Sandbox: Used for development and testing. Fully isolated from production environments.
•	Production: Intended for live business apps and flows. Requires strict governance.
•	Developer Environment: Personal Dataverse-enabled environments for makers.
•	Trial: Temporary environments for evaluation.
•	Teams Environment: Automatically created when Teams apps are built.
3.2 Environment Placement
All environments reside inside the tenant but can be located in different geographic regions. Enterprise architecture teams commonly define a multi-environment strategy—Dev, Test, UAT, Prod—to mimic software development lifecycle (SDLC) practices.
3.3 Assigning Users to Environments
Users are not automatically granted access to non-default environments. They must be explicitly added using the Power Platform Admin Center. Environment roles control access, independent of licenses. A user may have a premium license yet be unable to access Dataverse unless assigned a proper security role.
________________________________________
4. Dataverse Capacity Management
Dataverse is the cloud-scale database powering business applications, workflows, and virtual agents. All Dataverse capacity—Database, File, and Log—is managed at the tenant level.
4.1 Where Capacity Lives
Capacity is shared across all environments. It is not tied to a specific user or license. The tenant pool grows when licenses are purchased and decreases when data is stored.
4.2 Shared Capacity Model
Because capacity is pooled, one environment can consume more than others. If the tenant runs out of space, Dataverse blocks new records or creation of new Dataverse-enabled environments.
4.3 Capacity Increase from Licenses
Premium Power Apps and Power Automate licenses contribute additional Dataverse capacity. For instance, purchasing 100 premium licenses increases database storage significantly, allowing more enterprise-grade applications.
4.4 Purchasing Additional Capacity
Organizations can buy additional database, log, and file storage. The cost depends on region and contractual agreements. Enterprises often monitor usage through the Power Platform Admin Center to avoid service disruptions.
________________________________________
5. Licensing Model Explained
Licensing defines what features a user can access—not what environments they can access. A user with Power Automate Premium can use premium connectors, but access to environments still requires roles.
5.1 License Assignment Behavior
Licenses are assigned at the user account level via the Microsoft 365 Admin Center. Even if licenses are unassigned, the organization still pays for them as part of the subscription.
5.2 Example Scenario
If an organization purchases 3 Power Automate Premium licenses but assigns only 1, they still pay for all 3. Unassigned licenses simply remain available for future users.
5.3 License Impact on Dataverse
Premium licenses increase Dataverse capacity at the tenant level, enabling organizations to scale storage as automation needs grow.
________________________________________
6. Security Roles & User Permissions
Security roles define user access both at the tenant level (managed in Microsoft 365) and the environment/Dataverse level (managed in Power Platform Admin Center).
6.1 Microsoft 365 Directory Roles
Examples include: - Global Admin – highest privilege - Power Platform Admin – manages Power Platform resources - Dynamics 365 Admin – manages CRM/ERP components
These roles give administrative abilities but do not grant Dataverse table access.
6.2 Dataverse Environment Security Roles
Over 100 built-in roles manage entity-level access. These include: - Basic User - Environment Maker - System Administrator - System Customizer
Each grants a different level of access—from using apps to fully managing Dataverse.
6.3 Custom Security Roles
Many enterprises create custom roles matching business departments—e.g., Sales Manager Role, Audit Role, Production Analyst Role—to ensure least-privilege access.
________________________________________
7. Power Platform Governance Components
Governance ensures secure adoption. It covers environment strategy, DLP policies, licensing, user roles, and ALM processes.
An example governance model might include: - Prod, Dev, Test environments - Strict tenant-wide DLP - Automated monitoring using Center of Excellence (CoE) - Naming conventions, logging, and version control
Without governance, citizen developers may create unmanaged workflows that risk data leakage, performance bottlenecks, or compliance violations.
________________________________________
8. Data Loss Prevention (DLP) Policies
DLP is the core security mechanism that prevents unauthorized data movement between connectors. It ensures sensitive data does not leave secure systems.
8.1 Enforcement Mechanism
DLP policies are enforced before a flow or app runs. For example, if Dataverse is in the Business group and Gmail is in the Non-business group, a maker cannot build a flow that sends Dataverse data to Gmail.
8.2 Tenant-Level vs Environment-Level Policies
•	Tenant-level policies apply to all environments.
•	Environment-level policies override tenant-level restrictions but only where allowed.
8.3 Use Cases
Example 1: Block external APIs using the HTTP connector. Example 2: Allow relaxed connectors only in development environments. Example 3: Restrict social media connectors for government or finance clients.
________________________________________
9. End-to-End Scenario — Onboarding a New Employee
When a new employee joins, the organization follows this lifecycle: 1. IT creates the user in Microsoft 365. 2. A Power Automate Premium license is assigned. 3. The user gets automatic access to the Default environment. 4. Admins add the user to specific environments based on function. 5. Security roles such as Basic User or Environment Maker are assigned. 6. Tenant-level DLP policies automatically apply. 7. The user builds flows and apps according to the allowed connector rules.
This ensures secure onboarding while preventing data misuse.
________________________________________
10. Best Practice Governance Model
10.1 Environment Strategy
Maintain multiple environments—Prod, Dev, and Test—to ensure stability and reduce risk. Avoid building enterprise apps in the Default environment.
10.2 Licensing Strategy
Monitor unused licenses, track renewals, and ensure the right license SKU for each user. Use workload-based assignment rather than giving premium licenses to everyone.
10.3 DLP Strategy
Use strict tenant-level DLP policies to protect sensitive connectors. Use relaxed policies only in development or sandbox environments.
10.4 Security Strategy
Implement least privilege, use custom security roles, and assign System Administrator roles only to trained individuals.
________________________________________
11. Conclusion
Power Platform offers tremendous agility for building enterprise-grade applications, but without proper governance, organizations risk data loss, unmanageable environments, and regulatory challenges. By understanding tenants, environments, Dataverse capacity, licensing, security roles, and DLP policies, organizations can create secure, scalable, and well-managed Power Platform solutions. This expanded whitepaper serves as a blueprint for building a mature governance framework while empowering business teams to innovate safely.

