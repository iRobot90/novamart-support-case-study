# NovaMart support agent: implementation case study

A multi-agent customer-support project covering order questions, return eligibility and policy retrieval.

## Implementation work

The project uses a coordinator to route requests to inventory, policy, refund and communication agents. My completed implementation adds:

- Order lookups using both the customer and order identifiers, customer-tier lookup, and paginated order queries.
- Return checks for ownership, delivery status, a supplied reason, valid order dates and tier-based eligibility windows.
- Agent instructions that separate factual lookup from eligibility decisions and avoid claiming money has already been refunded.
- Knowledge-base retrieval tracing, readable policy labels and prevention of duplicate nested trace segments.
- Local execution output that includes a request summary and final response.

The original project uses Python, Strands Agents, Amazon Bedrock, DynamoDB and AWS tracing services.

## Engineering decisions

The order lookup uses the full composite key rather than an order identifier alone. Refund validation is also checked by the tool implementation, instead of relying only on model instructions. Retrieval tracing groups work by policy type so the request path is easier to inspect.

The exercise uses the order date as the eligibility reference because a separate delivery date is not stored. A production implementation would need an explicit policy for the correct date and additional review of authorization, concurrency and failure recovery.

## Current status

This repository is a case study, not a runnable standalone application. The original implementation depends on AWS resources and course-provided components, which are not bundled here. No live cloud deployment is claimed by this repository.

The source was reviewed locally, but the full AWS-dependent test suite was not run. Three checks in the supplied local test file report success without checking the corresponding service, so they are not used as evidence that memory, logging or tracing is configured correctly.

## Background

This work was completed through hands-on AWS/Udacity coursework. This case study describes implementation work without redistributing the course starter code, diagrams, infrastructure or private account details.
