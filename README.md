# Langflow Kubernetes Helm Charts

<div class="column" align="middle">
  <img alt="GitHub License" src="https://img.shields.io/github/license/langflow-ai/langflow-helm-charts">
  <img alt="GitHub Release" src="https://img.shields.io/github/v/release/langflow-ai/langflow-helm-charts?filter=langflow-ide-*">
  <img alt="GitHub Release" src="https://img.shields.io/github/v/release/langflow-ai/langflow-helm-charts?filter=langflow-runtime-*">
</div>


## Charts
- [LangFlow IDE](./charts/langflow-ide/): Full experience of Langflow, optimized for prototyping and testing new flows. 
- [LangFlow Runtime](./charts/langflow-runtime/): Productionize Langflow flows as standalone services.


## Langflow IDE vs Runtime

Langflow offers two distinct Kubernetes charts for deployment: one for the Integrated Development Environment (IDE) and another for the Runtime environment. 
This separation is designed to enhance security, optimize resource allocation, and streamline management. 
Understanding the rationale behind these deployment options will help you make informed decisions about how to best deploy and manage your applications.

The `ide` chart is designed to provide a complete environment for developers to create, test, and debug their flows. It includes both the API and the UI.

The `runtime` chart is tailored for deploying applications in a production environment. It is focused on stability, performance, isolation and security to ensure that applications run reliably and efficiently.

### Why is important to have separate deployments?
- Security
  - Isolation: by separating the development and production environments, we can better isolate different phases of the application lifecycle. This isolation minimizes the risk of development-related issues impacting the production environment.
  - Access Control: different security policies and access controls can be applied to each environment. Developers may require broader access in the IDE for testing and debugging, whereas the runtime environment can be locked down with stricter security measures.
  - Reduced Attack Surface: the runtime environment is configured only include essential components, reducing the attack surface and potential vulnerabilities.

- Resource Allocation
  - Optimized Resource Usage and cost efficiency: by separating the two, we can allocate resources more effectively. Additionally, each flow can be deployed independenly, providing fine-grained resource control.
  - Scalability: the runtime environment can be scaled independently based on application load and performance requirements, without affecting the development environment.
