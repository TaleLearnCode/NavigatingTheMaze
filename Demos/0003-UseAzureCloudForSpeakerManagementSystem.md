# Use Azure Cloud for Speaker Management System

- **Status:** Accepted
- **Date:** 2024-03-24
- **Work Item:** 5678-Select-Cloud-Provider

## Context and Problem

Our organization needs to select a cloud provider for our online speaker management system. The chosen provider must ensure data residency compliance across Europe while maintaining a strong presence in the United States for optimal performance and support.

## Decision Drivers

- **Data Residency Compliance:** Must comply with GDPR and other European data protection regulations.
- **Global Presence:** Needs strong infrastructure in both Europe and the United States.
- **Performance:** Ensures low latency and high availability.
- **Integration Capabilities:** Works seamlessly with our existing systems and tools.

## Considered Options

- Microsoft Azure
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)

## Decision Outcome

Chosen option: **Microsoft Azure**, because it offers robust data residency options, a strong presence in both Europe and the United States, and seamless integration with our current systems.

#### Consequences

- Good, because Azure provides extensive data residency options and compliance with European regulations.
- Good, because it ensures high availability and low latency due to its strong infrastructure.
- Bad, because there might be a slight learning curve for teams unfamiliar with Azure tools.

#### Implementation

1. Establish Azure accounts and configure necessary services.
2. Migrate existing data and applications to Azure.
3. Conduct thorough testing to ensure compliance and performance.
4. Provide training sessions for the team to get acquainted with Azure tools.

#### Confirmation

Confirm implementation by:

1. Conducting compliance audits for GDPR and other relevant regulations.
2. Performing latency and performance tests across different regions.
3. Ensuring seamless integration with existing systems.

#### Stakeholders

- IT Team
- Compliance Officers
- Data Protection Officers
- Development Team

## Pros and Cons of the Options

### Microsoft Azure

- Good, because it provides extensive data residency options and strong GDPR compliance.
- Good, because it offers high availability and low latency in both Europe and the United States.
- Neutral, because it integrates well with our existing Microsoft tools and services.
- Bad, because there might be a slight learning curve for teams unfamiliar with Azure tools.

### Amazon Web Services (AWS)

- Good, because it has a vast global presence and infrastructure.
- Good, because it provides robust data protection and compliance features.
- Neutral, because it integrates with a wide range of tools and services.
- Bad, because it might have higher costs compared to other options.

### Google Cloud Platform (GCP)

- Good, because it offers strong data analytics and machine learning capabilities.
- Good, because it has good infrastructure in both Europe and the United States.
- Neutral, because it integrates well with Google's suite of tools and services.
- Bad, because it may have fewer data residency options compared to Azure.

## More Information

No more information available.

## Follow-On Information

The decision will be reviewed bi-annually to ensure it continues to meet data residency and performance requirements. Updates or revisions will be documented as needed.

## Record History

* **Proposed**: 2024-20-18
* **Accepted**: 2024-03-24
* **Last Reviewed**: 2024-10-03
* **Deprecated**: [Date, if applicable]
* **Superseded by**: [Reference to the ADR that supersedes this one, if applicable]
* **Date Superseded**: [Date, if applicable]
* **Archived:** [Date, if applicable]