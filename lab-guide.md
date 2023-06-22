# PRISMA CLOUD CODE TO CLOUD LAB EXERCISE

![image](https://github.com/PaloAltoNetworks/c2c_summit_lab/assets/137418261/b2b58e4a-6672-4141-a112-2b1ff3025c4c)

### Lab Introduction

Thank you for joining today's Code to Cloud hands on lab with Prisma Cloud. The lab will focus on the ways
that Prisma Cloud can help you secure applications from code to cloud.

Before we begin the lab let's start with a brief overview of the scenario to help frame the
context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to finish a new mobile banking app for their customers by the end of their fiscal quarter. Up against unrealistic goals the development and infrastructure teams are working around the clock to get their app built, tested, and released to hit their deadlines.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle adopting security from code to cloud. Once in production Exampli Corps operations and security teams continue to leverage Prisma Cloud to monitor and protect runtime resources, reduce the attack surface, and enforce least privilege.

Will the Exampli Corp team take the time to build a secure app? Or will the stress of completing the Bank of Anthos app in time for deadlines lead to mistakes?

### Lab Overview

The lab is broken down into three sections :

##### Gain Visibility and Control of Cloud Assets

In this first section you will learn how to use Prisma Cloud to quickly identify Risky Assets in Exampli’s cloud footprint, automatically inform the relevant stakeholders, and remediate misconfigurations that lead to cloud breaches. 

##### Protect Critical Applications

The second section covers detecting and protecting containerized workloads powering Exampli Corp’s critical Bank of Anthos application using Prisma Cloud Defenders. 

##### Prevent Risk 

The final section includes shifting security left to help prevent vulnerable cloud infrastructure and applications from hitting runtime.

### Architecture 
The lab primarily focuses on Exampli Corp’s Banking Application known as the Bank of Anthos. The Bank of Anthos application is an example application purpose built for Google Kubernetes Engine, you can find the repo here as well as in the Resources section.

If you are unfamiliar with Kubernetes or container orchestration do not worry below you can find a HLD of the applications architecture. Additionally, in the Resources section there are provided links to learn more about Kubernetes and container orchestration. 

Prisma Cloud is integrated with mock company Exampli Corp in the following ways : 

1. Cloud Accounts are onboarded with Prisma Cloud allowing visibility into Exampli’s resources as well as their associated behavior and configuration states.

2. Critical applications in Exampli Corp’s cloud footprint are protected by Prisma Cloud defenders.

3. Code Repositories, Image Registries, and CI Tools are on-boarded into Prisma Cloud allowing for detection and remediation of misconfigurations and vulnerabilities earlier on in the development process.

### Resources

Vulnerable IaC :

In this lab we leverage some intentionally vulnerable IaC. To learn more about the projects and
its contributors visit the link below:

##### Sample Git Repositories

- [TerraGoat - Vulnerable by design Terraform Infrastructure](https://github.com/bridgecrewio/terragoat)

- [Cfngoat - Vulnerable by design Cloudformation Template](https://github.com/bridgecrewio/cfngoat)

- [CdkGoat - Vulnerable by design AWS CDK Infrastructure](https://github.com/bridgecrewio/cdkgoat)

- [BicepGoat - Vulnerable by design Bicep and ARM Infrastructure](https://github.com/bridgecrewio/bicepgoat)

- [KubernetesGoat-Vulnerable by design KubernetesCluster](https://github.com/bridgecrewio/kubernetes-goattest)

- [KustomizeGoat - Vulnerable by design Kustomize deployment](https://github.com/bridgecrewio/kustomizegoat)

- [SupplyGoat- Vulnerable by design SCA](https://github.com/bridgecrewio/supplygoat)

Bank of Anthos Application :

In this lab there is a mock banking application that is used as the application the Exampli Corp
development team is building. To learn more about the project and its contributors visit the link
below :

- https://github.com/GoogleCloudPlatform/bank-of-anthos

### Exercise

#### Gain Visibility and Control of Cloud Assets

Let's begin the lab by exploring Exampli Corp's existing assets to see if any alerts or vulnerabilities have been detected by Prisma Cloud.

1. Login to [Prisma Cloud](https://app3.prismacloud.io/legacy/signin).

2. Use the credentials provided by your Instructor to authenticate.

3. Use the navigation pane on the left hand and click the **blue arrow** on the lower left
side of the UI to open up the navigation pane and move between the different
modules within Prisma Cloud.

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-3.png "Optional title")

4. Next, use the navigation pane to select the **Inventory** module and then select
**Assets.**

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/7ad86954-db4e-4281-9444-a0155902926c)

5. Once in the Asset Inventory view, click on the **High Risk Assets** tab. Scroll towards the bottom and take a look at the **Google Compute Engine** service. Exampli Corps uses deployed these hosts using Googles Kubernetes service called GKE to orchestrate their container workloads that run the banking applications Exampli's customers use everyday.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/35f99789-924b-4500-8c35-f53a8f43791a)

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/85efb5a4-0537-4002-8af6-d35f8c484195)

Note the two columns **Assets with Alerts** and **Assets with Vulnerabilities**. 

6. Click on one of the hyperlinked numbers in the **Assets with Alerts** column.

7. Now we have a view of the assets in question along with other useful metadata.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/5f63dee7-ac3f-4033-836f-9c8d9c2df0a6)

8. Click on the first Asset Name to open a detailed side window view.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/503ec353-8a72-40a1-ab71-28d279ad834c)

9. From the side window view, we can explore the Alerts and Vulnerabilities associated with the asset in question. Note in the **Alerts** tab we can see the 4 High severity alerts associated with the asset. Note the different **Policy Name** categories.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/fce4df02-3b6e-43f1-895f-da4d106664ca)

We can see a couple issues right away that are a high risk such as **GCP VM instance that is internet reachable with unrestricted access (0.0.0.0/0) to Admin ports** and **GCP VM instance with data destruction permissions**.

Addtionally in the **Findings** tab we can see a long list of CVE's that need to be addressed such as CVE-2023-24538, which allows code injection via Javascript.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/0ffb521a-6205-443c-8c5e-a109c1663ce0)

Please feel free to explore the other alerts and CVE's for more insight. Use the filters to find the worst CVEs impacting these hosts. 

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/ac2f322d-2440-4cfd-80b7-e3ebb1937596)

Well done, you helped identify alerts and vulnerabilities present in Exampli's GKE cluster. Fortunately, Exampli Corps has integrated Prisma Cloud with the organization's Jira instance. With this integration configured the appropriate system and application owners have been notified and Jira Issues have been created to track their remediation automatically.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/31839fdf-c46e-4849-b6b3-ef206752073f)

Prisma Cloud has many out of the box integrations as well as supports the use of Web Hooks to operationalize security outcomes using other third-party tools.

To learn more view our public documenation for more info :

https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin/configure-external-integrations-on-prisma-cloud

Now that we have learned about some vulnerabilties and misconfigurations on Exampli's GKE cluster let's learn a little bit more information about the containerized applications running on them!

### Protect Critical Applications

#### Visualize Applications and Establish Context

The first step to protecting applications is to gain and maintain comprehensive visibility of your applications and all their associated resources. If Exampli Corp does not have oversight of their cloud environment it is impossible for them to stop emerging threats, respond to incidents, or reduce vulnerabilities. In a modern multi-cloud and hybrid world, applications are broken into different environments across the clouds like VMs, containers, serverless compute architecture types. Maintaining visibility is essential to protecting applications at runtime.

Prisma Cloud supports a massive amount of compute types, to review the supported systems check out our public documentation. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/install/system_requirements)

Let's help Exampli Corp get a clear picture of the application running on the vulnerable GKE cluster from the previous section. Start by taking a look at the microservices running the Bank of Anthos application using Prisma Cloud’s Radar feature.

1. The Radar feature lets you gain a bird’s eye view to monitor and understand your cloud applications. It helps you visualize the connectivity between microservices and search for vulnerabilities. Navigate to **Compute -> Radar -> Containers** and select the cluster **bank-of-anthos**.

![Alt text for image](/screenshots/maintaining-visibility-1.png "Optional title")

2. Once you have selected the correct cluster your screen should look similar the the screenshot below:

![Alt text for image](/screenshots/maintaining-visibility-2.png "Optional title")

3. Radar provides a visual depiction of the connections between containers, apps, and cluster services across your environment. Take some time to play around with the Radar feature and think through the following questions:

**What type of information can you learn by clicking on the nodes?
How does this visibility help you protect your applications?**

4. Let’s dive deeper into the **frontend:v0.5.5** microservice. Click on the associated container. Your screen should look similar to the screenshot below:

![Alt text for image](/screenshots/preventing-attacks-3.png "Optional title")

5. Take some time to review the **Vulnerabilities** page.

![Alt text for image](/screenshots/preventing-attacks-4.png "Optional title")

6. Of the identified OS vulnerabilities, which one has the highest CVE? Do all the identified vulnerabilities contain a fix?

7. Take a look at the **Layers** tab to view the dockerfile that built this image and find where vulnerabilities were introduced.

![Alt text for image](/screenshots/preventing-attacks-6.png "Optional title")

8. Find the file that added the most severe vulnerabilities and open it up by clicking on it to learn more about specifically what CVEs were added. Your screen should look similar to the screen capture below :

![openssl-1](https://github.com/c-haisten/c2c_summit/assets/98335592/7d522d07-18c8-4ce0-afe2-4d12cb44d370)

**We can see that this particular file introduced a ton of vulnerabilities including the usage of openssl version 1.1 which is susceptable to a number of malicious exploits.** 

9. Now that we have established some understanding of this container and have found some CVE's lets expand our knowledge by observing this workload's behavior using Prisma Cloud's foresnic modeling capabilities. Click the back arrow at the top right hand side of the UI and arrive back at the container summary view. Your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/preventing-attacks-3.png "Optional title")

#### Modeleing Application Behavior

Prisma Cloud observes and logs behavior such as running processes, network behavior, and even binary executions. Prisma Cloud then takes this data and builds a model for each workload giving administrators an understanding of what is the normal working conditions of their applications. Armed with this information administrators both understand the behavior of their workloads and can prevent malicious actions from taking place.

1. Begin by clicking on the forensic microscope underneath the **Runtime** tab.

![forensic-model](https://github.com/c-haisten/c2c_summit/assets/98335592/39476dcb-54cc-418e-bca4-cfeeb42cac71)

2. Here you can see all the events displayed. Let’s take a deeper look at these events to get some details and see what has been happening with our bank-of-anthos-frontend.

![Alt text for image](/screenshots/investigate-incidents-at-runtime-5.png "Optional title")

3. To learn more please find the following documentation covering more details around runtime protection.(https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)

4. Now let's take a look at a summary view of some of the suscipious behaviors taking place on this workload. Please click the close button at the bottom left of the UI. You should be back at the summary page and your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/preventing-attacks-3.png "Optional title")

5. Next, click on **Runtime** tab on the summary view. Here we can view highlights from the container's behavior and see if there are any security concerns with what the container is doing.

![runtime-events](https://github.com/c-haisten/c2c_summit/assets/98335592/92d8f7c6-a14f-4a7a-8420-07afcedd0125)

6. On this screen you will find a summarized list of findings from the defender including behavior that is not in the container's model. Your screen should look similar to the screen capture below :

![runtime-summary](https://github.com/c-haisten/c2c_summit/assets/98335592/d751a357-11a1-437a-a0c3-95e30404752d)

7. Find the audit finding of a foriegn binary execution of tcpdump and click on it. If you have trouble finding it you can type tcpdump in the search bar at the top of the UI.

![runtime-summary-1](https://github.com/c-haisten/c2c_summit/assets/98335592/24adb5ff-5f69-43af-b388-8ab63ae9929b)

![runtime-summary-filter](https://github.com/c-haisten/c2c_summit/assets/98335592/d955e32c-eee3-45c2-8e80-3c9dd9d65d77)

8. This view provides an expanded understanding of the finding. We can see that Prisma Cloud alerted on this finding due to the default rule to alert on suspicious behavior. Administrators can configure their own rules alert on or block malicious activity.

9. Creating rules to defend applications is easy in Prisma Cloud. Use the navigation bar on the left hand side of the UI and select **Compute -> Defend -> Runtime**.

![runtime-rules](https://github.com/c-haisten/c2c_summit/assets/98335592/1332f7ea-c45f-4004-8eba-2d30a98b9cfc)

10. On this page administrators can configure rules that make sense for their applications. There is a great deal of granularity given to Prisma Cloud administrators to configure allowed process, networking, and file system actitivies. Prisma Cloud defenders are also integrated with Palo Alto Network's WildFire anti-malware service allowing for the blocking of malware found on the application.

![runtime-rules-blocking](https://github.com/c-haisten/c2c_summit/assets/98335592/3b0f5dcb-7e1f-4668-bf90-40d41964bf41)

**Feel free to explore the different pages, because this is a lab you will have limited permissions and are not able to edit or create rules.**

For more information about runtime rules and protection from Prisma Cloud check out our public documentation here. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)

In addition to providing visibility, context, and protection for applications Prisma Cloud also helps operationalize security outcomes by automatically mapping events to the Mitre ATT&CK Matrix. In the next steps you will learn how Prisma Cloud helps enable Exampli Corps find indicators of compromise and help secure their footprint.

#### Mitre ATT&CK Matrix

Exampli Corp has adopted Prisma Cloud and maintained consistent visibility on their applications. But seeing your resources does not make them immune to incidents during runtime. By using the Mirtre ATT&CK Matrix the Exampli Corp Security team gets analysis of potential threats to their applications mapped against the Mitre standard.

1. Let's begin by navigating to **Monitor -> Monitor -> ATT&CK**. On this screen we can see an interactive view of the attack framework organizing the different observed findings with associated attack methods.

![mitre-selection](https://github.com/c-haisten/c2c_summit/assets/98335592/0595d572-4268-4b6c-beb2-fe87cf2a8d99)

2. Start by clearing out the time filter to get a better view of different types of findings. By default the view is set to 7 days. You can clear it by clicking on the 'X' found on the filter. 

![mitre-time](https://github.com/c-haisten/c2c_summit/assets/98335592/6ece5937-1a37-4248-816f-368af1f3884c)

3. Take a look at the **Account Manipulation** category underneath the **Persistence** column and click on it. You screen should look similar to the capture below :

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/75a2de99-2361-4d93-a805-71c4c8bd7bf6)

4. Prisma Cloud provides a summary of findings associated with Account Manipulation and organizes for administrators to use for investigations and remediation efforts. For this particular attack method we can view the description of Account Manipulation according to Mitre.  

**Adversaries may manipulate accounts to maintain access to victim systems. Account manipulation can consist of any action that preserves adversary access to a compromised environment, such as modifying or adding credentials to an account or changing permissions. In Kubernetes environments, adversaries can persist access by creating RoleBindings and ClusterRoleBindings that grant access to an adversary-controlled service account, user, or group.**

5. Click on a recent finding to learn more, your screen should look similar to the capture below :

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/43faa08c-17ae-48e9-aef8-c6c7eacd13ab)

6. Scroll to the bottom of the page to learn more information about the container and audit details. Here we can see that this alert is related to the GKE hosts and Bank of Anthos application from the information provided in the container summary. It appears an attacker is trying to create a backdoor into the application. Fortunately because Prisma Cloud is integrated with JIRA and issues have been created, work is underway to quaratine the cluster. 

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/c99fd419-5d7b-4abd-8d0e-9373d8c3e1ec)

7. Are you able to discover additional findings associated with Exampli's GKE hosts? Feel free to exploe other attack methods and findings.

There are many capabilities that Prisma Cloud can deliver when protecting applications that are not covered in this lab including but not limitied to Wep App and API Security. To learn more about how Primsa Cloud can protect application APIsvisit this page. (https://www.paloaltonetworks.com/prisma/cloud/web-application-API-security)

The final section of the lab will cover concepts of reducing risk at runtime by finding and fixing insecure infrastructure code and identifying insecure software packages early in the development lifecycle. In this section you will investigate insecure infrastructure code as well as investigate Exampli Corps code supply chain.

#### Prevent Future Risk 

Let's begin this next exercise by exploring the power of shifting security left with Infrastructure as code
scanning. As infrastructure is being defined as code, security must be integrated with the
tools developers use.

The first place we will begin is with investigating Exampli Corp's infrastructure code in the company's GitHub repositories. 

Follow the steps below :

1. Use the navigation pane to select the **Code Security** module and then select **Projects.**

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-3.png "Optional title")

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-4.png "Optional title")

2. At the top of the UI select the **Exampli** view.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/fe7d38fc-8dc2-4c7e-ab4d-8a9e96949317)

3. Once you have selected the correct view, begin by using the filters and ensure you select the **Code Category IaC Misconfiguration**

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/ed8d5f7e-7689-4891-b732-8a4954baee9a)

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/2247402e-3d58-4fa6-992b-4308de8098e6)

4. Here we can see a summary of various findings in Exampli's code repositories. Feel free to use the filters to investigate different findings and see if you can find any high severity issues.

5. When you are finished use the search bar at the top of the UI and search for the big_data.tf script that Exampli's infrastructure team has been developing for a new analytics project at Exampli Corps.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/de61f6d5-6817-41b8-817c-8e03d3fb21c3)

7. Now that we have filtered by severity, explore the different misconfigurations and
identify the one that says **_GCP SQL database is publicly accessible._**

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-7.png "Optional title")

8. Click the Policy details button ![Alt text for image](/screenshots/policy-details-button.png "Optional title") to view guidelines on how to resolve the
misconfiguration. Below is an example of how the policy box will look and the type of information you will see.

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-8.png "Optional title")

9. Reviewing the guidelines we can see the description of this misconfiguration, its potential risk, and how to remediate at build time and runtime.

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-9.png "Optional title")

10. Now navigate back to the Prisma Cloud platform. Click on the associated SQL database resource and view the helpful information about the misconfiguration such as its history, errors, details, and traceability. It also will give you an option to view the resource in its VCS.

![Alt text for image](/screenshots/find-and-fix-insecure-infrastructure-code-10.png "Optional title")

11. This misconfiguration makes the application vulnerable to attacks that could reveal sensitive data such as user credentials and financial information. This error could lead to big problems for the Bank of Anthos. By using Prisma Cloud code security, the Exampli Corp security team can avoid costly mistakes and protect the integrity of the application.

**There are many other examples to explore in the Exampli repo, feel free to use the filters and search bar to explore additional resources and findings.**

#### Generating Pull Requests

1. Depending on the nature of a misconfiguration, Prisma Cloud can provide single click remediation. This capability creates a pull request that is sent to the version control system where the IaC template is stored.

Looking at the same **big_data.tf** template, there is another HIGH severity misconfiguration for lack of SSL on SQL database connections.

![Alt text for image](/screenshots/generating-pull-requests-1.png "Optional title")

2. This resource is a fully managed relational database service for MySQL, PostgreSQL and SQL Server. It is recommended to enable SSL but we can see it is not configured in this resource.

**The Suppress and Fix capability requires increased RBAC capabilities and is not available to read-only users**

3. Pull requests have been created previously for various findings. To access the VCS associated with this IaC resource click the git link. We can also see the developer who committed the last change associated with this IaC resource.

![Alt text for image](/screenshots/generating-pull-requests-3.png "Optional title")

4. After clicking the git link we see the last commit associated with the **big_data.tf** IaC template. Highlighted is the **ip_configuration** parameterwhich does not include the SSL enablement.

![Alt text for image](/screenshots/generating-pull-requests-4.png "Optional title")

5. To view the fix generated by Prisma Cloud let’s take a look at the pull requests tab at the top of the github UI.

![Alt text for image](/screenshots/generating-pull-requests-5.png "Optional title")

6. Once on the Pull Requests view take a look at [PR #34](https://github.com/umman-manda/Exampli/pull/34) and its associated [commit](https://github.com/umman-manda/Exampli/pull/34/commits/d1360871240084945b5d7d09d087e195241b9e22). Examining the changes, the ‘require_ssl = true’ setting has been added to the big_data.tf template.

![Alt text for image](/screenshots/generating-pull-requests-6.png "Optional title")

#### Identify Exposed Secrets

Prisma Cloud also gives administrators the ability to detect exposed secrets. This is a powerful
tool that can be utilized from the Project page.

1. Clear out all of your filters and select **“Secrets”** under **Category**. Now you can view any exposed secrets in your repository. 

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/40acdfec-0876-4ed9-af46-2e94e6c7ad1c)

2. Find the secrets in the on **/terraform/aws** you will see that there are several misconfigurations that expose secrets. Take a closer look at the **providers.tf** template. Note that you may have to search for the file if the filters don’t work due to concurrent users within the lab. Here we can see a variety of issues with this terraform template. The first being hard coded plain text secrets.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/146e03d9-170b-435f-8c1d-b3d3995f820d)

3. When accessing AWS programmatically users can select to use an access key to verify their identity, and the identity of their applications. An access key consists of an access key ID and a secret access key. Anyone with an access key has the same level of access to AWS resources.

![Alt text for image](/screenshots/identify-exposed-secrets-3.png "Optional title")

**According to the [2022 Verizon Data Breach Report](https://www.verizon.com/business/resources/T14f/reports/dbir/2022-data-breach-investigations-report-dbir.pdf), stolen access credentials are used in 80% of successful data breaches.**

Fortunately, Prisma Cloud makes it easy for anyone to quickly determine how the exposed secret can harm your organization and what steps must be taken. These exposed AWS access credentials could let an unauthorized attacker access the Exampli Corp AWS account. In this section we have looked at infrastructure in Exampli's repository but what about application code and OSS? 

### Software Composition Analysis:

1. Ensure that you select the **Exampli** view.

![Alt text for image](/screenshots/software-composition-analysis-5.png "Optional title")

2. Use the filters and select **Code Category Vulnerability**.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/bd200c35-25b1-49a1-8fbd-34b011b04812)

3. Let’s check to see if there are any serious vulnerabilities by filtering  **Category -> Vulnerabilities** and **Severity -> Critical.**

5. Next, find the CVE ID CVE-2022-23305 and click on it. This is the CVE associated with the infamous log4shell attacks. This view provides critical information that Exampli's teams can use to investigate the vulnerability and determine what next steps to take. 

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/ec507f49-ce05-4399-85d0-f6b6affbfc5b)

Administrators can click suppress, or fix. The suppress button allows you to dismiss all incidents that fall under that specific policy violation. The fix button will allow you to remediate the vulnerability via a bump fix. Here we can see that the vulnerability can be fixed by bumping to 2.0.

**Suppress and Fix requires increased RBAC that is not available in this lab**

8. You can also click the “Details” or “Errors” tab on the right side of the page to get some more information on the dangers of the specific vulnerability.

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/c35609ce-cc60-43ee-95df-c7842bc7340a)

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/4b4f6d10-2873-42c8-86f8-572c99c98e92)

9. This CVE has a CVSS score of 9.8! Its possible Exampli's applications could be vulnerable to a remote code execution attack.

On this page Exampli Corp developers can gain context on the CVE and click on the link to NIST providing them with all the details and documentation regarding the vulnerability. Feel free to explore other interesting findings in Exampli's repositories. Can you find anythig more dangerous CVE-2022-23305? 

10. In Prisma Cloud licenses are scanned in parallel to vulnerability scanning. This means that Exampli Corp developers can make sure they are remaining compliant when working with open source packages. Adjust your filter to **Category -> Licenses** and
let's see if there are any licensing issues in the Bank of Anthos Repo. Remember to clear the severity filter!

![image](https://github.com/c-haisten/c2c_summit/assets/98335592/720b13b9-5b30-43f9-8e69-c92b9bcbd5f3)

11. Now, let's scroll down and look at some of the licensing issues identified by Prisma Cloud.

![Alt text for image](/screenshots/software-composition-analysis-11.png "Optional title")

12. By Clicking on the license type Prisma Cloud provides developers with critical information and identifies each policy violation as a single error.

![Alt text for image](/screenshots/software-composition-analysis-12.png "Optional title")

Now that we have found some vulnerabilities and licensing violations in our Application code, let's take a look at how Prisma Cloud can give us visibility to the package manager files that comprise applications by taking a look at the supply chain and software composition analysis (SCA).

### Supply Chain Security

1. Use the navigation pane on the left hand and click the **blue arrow** on the lower left side of the UI to open up the navigation pane and move between the different modules within Prisma Cloud.

![Alt text for image](/screenshots/supply-chain-security-1.png "Optional title")

2. Next, use the navigation pane to select the Code Security module and select Supply Chain.

![Alt text for image](/screenshots/supply-chain-security-2a.png "Optional title")

![Alt text for image](/screenshots/supply-chain-security-2b.png "Optional title")

3. Use the Supply Chain Graph to view the relationships between different IaC templates and the types of infrastructure and services they provision. Be sure to select the bank-of-anthos repository from the drop-down window in the filters at the top.

![Alt text for image](/screenshots/supply-chain-security-3.png "Optional title")

4. Next, take a deeper look at the **requirements.txt** file. Feel free to test the filters on the left side of the UI and search bar at the top to quickly locate templates.

![Alt text for image](/screenshots/supply-chain-security-4.png "Optional title")

5. Once you have found the **requirements.txt** file click on the first package that is unpacked, **cryptography: 38.0.1**. Notice on the right side of the UI there is additional information about this resource.

Here we can quickly identify valuable information like the package version, license type and privileges.

6. Your screen should look similar to the screenshot below.

![Alt text for image](/screenshots/supply-chain-security-6.png "Optional title")

7. Next, click on the **Errors** tab to investigate policy violations and vulnerabilities.

![Alt text for image](/screenshots/supply-chain-security-7.png "Optional title")

8. How many Vulnerabilities are associated with the **cryptography: 38.0.1** package? Read the **Details** section to discover more about the CVE and confirm the **Fix Version**. Are there other packages with a higher CVSS score?

That concludes the exercise.

## Summary \ Resources

The Prisma Cloud team here at Palo Alto sincerely hopes you enjoyed this workshop. Today, organizations need a growing set of capabilities to secure modern cloud applications. Implementing AppSec into your development and security workflows with Prisma Cloud can provide the increased speed and agility your organization needs to implement zero trust throughout the entire development lifecycle. Check out the resources below for more information!

[Live Workshops](https://bridgecrew.io/resource/workshops/)

[DevSecTalks Podcast](https://www.paloaltonetworks.com/devsectalks/)

[Supply Chain Security](https://bridgecrew.io/software-supply-chain-security/)

[Cloud DevSecOps](https://bridgecrew.io/cloud-devsecops/)

[Learn More](https://www.paloaltonetworks.com/prisma/cloud)
