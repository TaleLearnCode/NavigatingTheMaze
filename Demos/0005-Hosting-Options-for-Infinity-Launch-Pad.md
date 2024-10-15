# Hosting Options for Infinity Launch Pad

- **Status:** Accepted
- **Date:** 2024-09-03
- **Work Item:** [8559 - Takeaway: Determine where to deploy updated Launch Pad and what training is needed](https://dev.azure.com)

## Context and Problem

The Infinity Launch Pad application is currently an ASP.NET MVC application using .NET Framework 4.8, hosted on-premises. The application is functioning well, but there is a new requirement to make the site multilingual. Given the effort required to implement this feature, we are evaluating whether it makes sense to host the updated application in Azure or keep it on-premises.

#### Multilingual Requirement

The new requirement ([8286 - Ability to Translate the Infinity Launch Pad](https://dev.azure.com) involves supporting English and Spanish for the Infinity Launch Pad application. This includes:

- Translating all static content (e.g., labels, messages, and navigation links) into multiple languages.
- Implementing language selection functionality, allowing users to switch languages seamlessly.
- Maintaining a consistent user experience across all supported languages.

#### Technical Challenges of Multilingual Support

- **Resource Management**: Managing resource files for each language, ensuring they are up-to-date and correctly referenced in the application.
- **User Interface Adjustments**: Adapting the UI to accommodate different text lengths and reading directions (e.g., right-to-left languages - which is currently out of scope).
- **Performance Considerations**: Ensuring that the addition of multilingual support does not negatively impact the application's performance.
- **Testing and Quality Assurance**: Thoroughly testing the application in all supported languages to ensure accuracy and usability.

#### Performance Considerations

- **Load Times**: Ensuring that the application loads quickly and efficiently.
- **Caching**: Possibly implementing effective caching strategies to reduce server load and improve response times for frequently accessed content.
- **Scalability**: Choosing a hosting option that can scale to handle increased traffic and data load as more languages are added.
- **Monitoring and Optimization**: Continuously monitoring performance metrics and optimizing the application to maintain a high level of performance.

## Decision Drivers

- Needed for multilingual support.
- Effort required for redevelopment or migration.
- Cost implications of hosting options.
- Scalability and future-proofing.
- Management and maintenance overhead.

## Considered Options

- Host the Infinity Launch Pad app as is (ASP.NET MVC on .NET Framework 4.8) on Azure App Service.
- Host the Infinity Launch Pad app as an ASP.NET MVC on Azure Container Apps (requires dockerizing the application).
- Convert the Infinity Launch Pad app to a Blazor WASM application and host on Azure Static Web Apps.
- Convert the Infinity Launch Pad app to a static website and host on Azure Static Web Apps.
- Convert to Blazor WASM and host on Azure App Service.
- Convert to Blazor WASM and host on Azure Container Apps.
- Leave the application hosted on-premises.

## Decision Outcome

Chosen option: Convert the Infinity Launch Pad app to a static website and host on Azure Static Web Apps, because it is the simplest and most cost-effective option, offering easy global distribution with integrated CDN and minimal management overhead.

#### Consequences

- **Good**: Simplest and most cost-effective option, easy global distribution with integrated CDN, minimal management overhead.
- **Bad**: Limited to static content (the current site is only static content)

#### Implementation

1. Convert the existing ASP.NET MVC application to a static website.
2. Host the static website on Azure Static Web Apps.
3. Implement multilingual support.
4. Adapt the UI to accommodate different text lengths and ensure a consistent user experience.
5. Thoroughly test the application in all supported languages to ensure accuracy and usability.

#### Confirmation

- Regular performance monitoring and optimization.
- User feedback and testing to ensure multilingual support is functioning correctly.

#### Stakeholders

- Architecture Team
- Development Team
- Product Owners (Dev02 and MFG)
- Software Development Management

## Pros and Cons of the Options

### Host the Infinity Launch Pad app as is (ASP.NET MVC .NET Framework 4.8) on Azure App Service

- **Projected Monthly Cost**: $73.00; assuming S1 Windows App Service (1 Core, 1.75-GB RAM, 50-Gb storage) in the Azure North Central US region.
- Good, because minimal changes to the existing application.
- Good, because easy deployment and management.
- Good, because supports server-side rendering and complex backend logic.
- Bad, because potentially higher costs compared to static hosting options.
- Bad, because requires ongoing management of the app service environment.

### Convert the Infinity Launch Pad app to a Blazor WASM application and host on Azure Static Web Apps

- **Projected Cost**: Free (includes up to 100-Gb of bandwidth per subscription and 0.5-Gb of storage per app). If more than 100-Gb required, need to go to the Standard tier which is $9/per app/month and then $0.20 per GB over 100-Gb.
- Good, because modern, client-side framework,
- Good, because potentially lower costs and global scalability.
- Good, because integrated API support via Azure Functions.
- Bad, because significant redevelopment effort to convert the application to Blazor WASM.
- Bad, because limited to client-side logic, which may not suit all use cases.
- Bad, because daily download delays for users on thin clients connecting to virtual machines that are rebuilt every evening.

### Convert the Infinity Launch Pad app to a static website and host on Azure Static Web Apps

- **Projected Cost**: Free (includes up to 100-Gb of bandwidth per subscription and 0.5-Gb of storage per app). If more than 100-Gb required, need to go to the Standard tier which is $9/per app/month and then $0.20 per GB over 100-Gb.
- Good, because simplest and most cost-effective option.
- Good, because easy global distribution with integrated CDN.
- Good, because minimal management overhead.
- Bad, because limited to static content.
- Bad, because may not support all current functionalities if server-side logic is needed.

### Convert to Blazor WASM and host on Azure App Service

- **Projected Monthly Cost**: $73.00; assuming S1 Windows App Service (1 Core, 1.75-GB RAM, 50-Gb storage) in the Azure North Central US region.
- Good, because combines the benefits of Blazor WASM with the flexibility of App Service.
- Good, because supports server-side APIs and complex backend logic.
- Good, because easy integration with other Azure services.
- Bad, because requires redevelopment effort to convert to Blazor WASM.
- Bad, because higher costs compared to static hosting options.
- Bad, because daily download delays for users on thin clients connecting to virtual machines that are rebuilt every evening.

### Convert to Blazor WASM and host on Azure Container Apps

- **Projected Monthly Cost**: $1.60; assuming 600,000 requests (5 requests/day/user) with and average 5 seconds per request. *Unsure if the included allotment is per subscription or per application.*
- Good, because combines the benefits of Blazor WASM with the flexibility of containerization.
- Good, because serverless infrastructure management.
- Good, because scalability and isolation of application dependencies.
- Bad, because requires redevelopment effort to convert to Blazor WASM.
- Bad, because requires effort to containerize the application.
- Bad, because daily download delays for users on thin clients connecting to virtual machines that are rebuilt every evening.

### Leave the application hosted on-premises

- **Projected Cost**: Existing infrastructure costs; but usage will go up and new infrastructure might be required.
- Good, because no changes required to the current setup.
- Good, because full control over the hosting environment.
- Good, because no additional cloud hosting costs.
- Bad, because limited scalability compared to cloud options.
- Bad, because potentially higher maintenance and infrastructure costs.
- Bad, because lack of cloud-native features and integrations.

## More Information

No more information available"

## Follow-On Information

No follow-on information.

## Record History

* **Proposed**: 2024-09-03
* **Accepted**: 2024-09-03
* **Last Reviewed**: [Date, if appliable]
* **Deprecated**: [Date, if applicable]
* **Superseded by**: [Reference to the ADR that supersedes this one, if applicable]
* **Date Superseded**: [Date, if applicable]
* **Archived:** [Date, if applicable]