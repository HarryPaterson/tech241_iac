<h1 style="text-align: center;">Terraform</h1>

### Contents
* What is Terraform?
* Why use Terraform?
* Who is using Terraform?
* Terraform installation
  
### What is Terraform?
Terraform is an open-source infrastructure as code (IaC) tool developed by HashiCorp. It allows users to define, manage, and provision infrastructure resources across multiple cloud providers and on-premises environments using declarative configuration files.

### Why use Terraform?
1. **Infrastructure as Code (IaC):** Terraform enables the concept of Infrastructure as Code, allowing you to define and version your infrastructure in a human-readable, text-based format. This brings several benefits, such as version control, collaboration, and reproducibility.

2. **Multi-Cloud Provisioning:** Terraform supports various cloud providers, including AWS, Azure, Google Cloud, and others. This gives users the flexibility to manage resources across different clouds without vendor lock-in.

3. **Resource Graph and Dependency Management:** Terraform builds a resource graph based on the configuration, allowing it to understand dependencies and relationships between resources. It ensures that resources are provisioned in the correct order, reducing errors and ensuring consistency.

4. **Idempotent Execution:** Terraform follows an idempotent approach, which means that applying the same configuration multiple times will result in the same outcome. This allows for safe and predictable infrastructure management.

5. **Change Management and Planning:** Terraform's "plan" command lets you preview the changes before applying them. This helps you understand what will happen when you make adjustments to your infrastructure and avoid unexpected side effects.

### Benefits of Terraform:
- **Automation:** Terraform automates the provisioning and management of infrastructure, reducing manual intervention and human error.

- **Scalability:** It is well-suited for managing large-scale infrastructures and complex deployments.

- **Consistency:** Terraform ensures that your infrastructure is consistent across environments, making it easier to maintain and troubleshoot.

- **Collaboration:** The use of configuration files enables easy collaboration among team members, as the infrastructure's entire state is stored in code repositories.

- **Version Control:** Configuration files can be versioned using tools like Git, enabling easy tracking of changes and rollbacks.

### Who is using Terraform?

- **HashiCorp:** The company behind Terraform itself, HashiCorp, uses its own tool for managing infrastructure and provisioning resources across cloud platforms.

- **Microsoft:** Microsoft, one of the leading cloud service providers, utilizes Terraform to offer Infrastructure as Code solutions to its Azure customers.

- **Shopify:** Shopify, an e-commerce platform, uses Terraform to manage its infrastructure and ensure consistency and scalability.

- **Splunk:** Splunk, a popular data analytics and monitoring platform, employs Terraform for automating its infrastructure on cloud providers.

- **Pinterest:** Pinterest, the social media and image-sharing platform, leverages Terraform for its infrastructure automation needs.

- **Lyft:** Lyft, the ride-sharing company, uses Terraform to manage its extensive cloud infrastructure and deployments.

### Terraform installation
1. Download Terraform at https://developer.hashicorp.com/terraform/downloads
2. Extract folder to desired location
3. Add to PATH by editing system environment variables, edit PATH, new with Terraform location as shown below.
![](https://i.imgur.com/kSqc6jf.png)
![](https://i.imgur.com/wc1wOps.png)
![](https://i.imgur.com/HKEBXe7.png)
![](https://i.imgur.com/hg5qgiD.png)
4. Verify Installation in CLI with terraform --version
![](https://i.imgur.com/jPvbqBD.png)
