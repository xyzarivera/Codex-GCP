# API Gateways for Cloud Functions

This is a comparison of GCP services to create an API Gateway for Cloud Functions. 

## Context

Improving the Solutions Architecture Design for creating Web Applications.

Compared to previous design, the team has decided to utilize an API Gateway to improve the following:

- Developer Experience
    - easy for app developers to consume your services.
- Application Decoupling
    - enables backend service implementation changes without affecting the public API
- Advantage of the scaling, monitoring, and security features built into the Google Cloud Platform

There are several ways to implement an API Gateway in GCP. Currently, there are three possible ways. I suggest choosing an implementation based on the use case. 

### Solutions Architecture with API Gateway


## API Gateway

**API Gateway** enables you to provide secure access to your services through a well-defined REST API that is consistent across all of your services, regardless of service implementation.


[About API Gateway | API Gateway Documentation | Google Cloud](https://cloud.google.com/api-gateway/docs/about-api-gateway)

### How to deploy

[Quickstart: Deploy an API on API Gateway using the Cloud Console](https://cloud.google.com/api-gateway/docs/quickstart-console)

[Pricing](https://www.notion.so/0c20d656a9cc4e83891b1be2a2a567fd)

[Pricing | API Gateway Documentation | Google Cloud](https://cloud.google.com/api-gateway/docs/pricing)

---

## Cloud Endpoints

**Cloud Endpoints** is a distributed API management system. It provides an API console, hosting, logging, monitoring, and other features to help you create, share, maintain, and secure your APIs.

[About Cloud Endpoints | Cloud Endpoints with OpenAPI | Google Cloud](https://cloud.google.com/endpoints/docs/openapi/about-cloud-endpoints)

### How to deploy

[Getting Started with Endpoints for Cloud Functions with ESPv2](https://cloud.google.com/endpoints/docs/openapi/get-started-cloud-functions)

### Request Rate Limit

A rate limit of **10,000,000 quota units per 100 seconds per service producer project** is enforced by default.

**Note:** Both ESP and Cloud Endpoints Frameworks employ efficient caching algorithms so they don't call Service Control every time your API is called. So while the default limit is 10,000,000 per 100 seconds, your API can support a much higher volume.

[Pricing](https://www.notion.so/37fe785363644e2986695d1fa56aefe0)

**Ingress**  - always free

**Egress**  - The API Gateway uses Premium Internet Egress (**per GB per month**)

[Egress](https://www.notion.so/4f119c4fee584e4cb22e54da36ec187c)

[Pricing and quotas | Cloud Endpoints | Google Cloud](https://cloud.google.com/endpoints/pricing-and-quotas)

---

## Apigee Edge

**Apigee Edge** is a platform for developing and managing APIs. By fronting services with a proxy layer, Edge provides an abstraction or facade for your backend service APIs and provides security, rate limiting, quotas, analytics, and more.

**Apigee Edge** consists of API runtime, monitoring and analytics, and developer services that together provide a comprehensive infrastructure for API creation, security, management, and operations.

[What is Apigee Edge? | Apigee Docs](https://docs.apigee.com/api-platform/get-started/what-apigee-edge)

### How to deploy

[Google Cloud Functions Extension | Apigee Docs](https://docs.apigee.com/api-platform/reference/extensions/google-cloud-functions/google-cloud-functions-extension-105)

[Using the Cloud Functions Extension securely](https://community.apigee.com/articles/69821/using-the-cloud-functions-extension-securely.html)

### **Pricing**

- Tier pricing

[Pricing | Apigee | Google Cloud](https://cloud.google.com/apigee/pricing?utm_referrer=https%3A%2F%2Fdocs.apigee.com%2F)