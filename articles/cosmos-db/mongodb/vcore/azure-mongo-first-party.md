---
title: Why Mission-Critical MongoDB Workloads Run on Azure First-Party Services
description: Learn why mission-critical workloads rely on first-party database services.
author: gahl-levy
ms.author: gahllevy
ms.service: azure-cosmos-db
ms.subservice: mongodb-vcore
ms.topic: product-comparison
ms.date: 06/03/2025
---

# Why mission-critical MongoDB workloads run on Azure first-party services

## Summary

For regulated industries, large enterprises, and mission-critical workloads, choosing the right cloud service matters. Azure developed, services—operated, secured, and supported by Microsoft—offer a fundamentally different level of control, compliance, and integration than third-party vendor-managed offerings and ISV integrations. This distinction is essential when evaluating managed MongoDB services on Azure. All first-party Azure services can be found on in the [Azure products page](https://azure.microsoft.com/products). 

## First-party vs. third-party ISV integration: What’s the difference?

Azure includes both **first-party** services (built and operated by Microsoft) and **third-party** services (published by ISVs such as MongoDB Inc.). These are fundamentally different in how they behave, integrate, and meet compliance expectations.

| Aspect                     | Azure Cosmos DB for MongoDB vCore             | MongoDB Atlas on Azure                         |
|---------------------------|-----------------------------------------------|------------------------------------------------|
| Developed By               | Microsoft                                     | MongoDB Inc. (third-party ISV integration)                 |
| Support                   | Microsoft Azure Support                       | MongoDB Inc. Support (separate contract)       |
| SLA Coverage              | End-to-end Microsoft-backed SLA                          | Vendor SLA excludes hardware, networking, and more.                           |
| Compliance Responsibility | Microsoft                                     | MongoDB Inc.                                   |
| Data Residency & Control  | Full Microsoft control plane + Azure policy   | Vendor-controlled environment                  |
| Network Integration       | Native Private Link, Entra ID (Management and Data), RBAC           | Limited/varies by vendor tier                  |

## Why this matters for mission-critical applications

### 1. **Security and compliance**

Mission-critical workloads demand full control over data and infrastructure. First-party services such as **Cosmos DB for MongoDB vCore** are built for [Microsoft’s extensive compliance portfolio](/azure/compliance/), including:

- UAE DESC
- FedRAMP
- ISO 27001, 27017, 27018
- HIPAA, PCI DSS, SOC 1/2/3

With third-party services such as MongoDB Atlas, **Microsoft is not responsible for the service’s compliance posture**- the vendor is.

### 2. **Support and escalation**

When running a native service:

- Azure Support covers everything from infrastructure to service behavior.
- No need to escalate across companies or manage vendor SLAs.
- Microsoft support teams engage directly, with full telemetry and control.

### 3. **Identity and access integration**

Cosmos DB for MongoDB vCore integrates natively with:

- Entra ID (formerly Azure AD) to **access your data** and **manage resources**. 
- Role-Based Access Control (RBAC)
- Azure policies and Private Link

This ensures centralized governance of who accesses what and how.

### 4. **Cost, billing, and SLA simplicity**

- Full-stack SLA covering the entire product
- No data transfer fees
- No charges for Backups
- No hidden support tiers doubling your cost

## Cosmos DB for MongoDB vCore: enterprise-ready, Microsoft-operated

Azure Cosmos DB for MongoDB vCore is a first-party service delivering:

- **Nearly 100% MongoDB [wire protocol compatibility](./managed-service-compatibility.md)**
- **Truly (MIT) open source, multi-cloud engine. Without [server-side public license](https://en.wikipedia.org/wiki/Server_Side_Public_License) limitations**.
- **AI-first capabilities such as vector search**
- **Global scalability, autoscale, and hybrid identity**
- **Full stack SLA** covering the database, compute, storage, and networking

## Conclusion

When uptime, compliance, support, and control matter, **only a first-party Azure service provides the trust and guarantees needed**. Cosmos DB for MongoDB vCore is purpose-built by Microsoft for enterprise-grade, mission-critical workloads.

## Next steps

> [!div class="nextstepaction"]
> [Get started with Azure Cosmos DB for MongoDB vCore](./quickstart-portal.md)
