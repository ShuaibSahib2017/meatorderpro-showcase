# Shuaib Sahib

## Cloud and Full-Stack Systems Builder

I design and operate practical software that connects customer ordering, factory workflows, dispatch, delivery, invoicing, printing, and workforce operations.

My focus is turning real operational constraints into reliable systems: clear service boundaries, event-driven workflows, secure access, observable production services, and tools that work for both office and factory teams.

## Featured Project: MeatOrderPro

MeatOrderPro is a private production platform built for an Australian meat processing and distribution business. It coordinates wholesale and retail orders from checkout through factory production, weight capture, packing, dispatch, delivery, invoicing, and reporting.

The source code, infrastructure identifiers, production endpoints, customer information, and operational runbooks are private. The diagrams below are intentionally high level.

### Platform Architecture

```mermaid
flowchart TB
    subgraph Channels[Order and Operations Channels]
        direction LR
        B2B[B2B Ordering]
        B2C[B2C Ordering]
        ADMIN[Admin Tools]
        FLOOR[Factory Smartboard]
        DRIVER[Driver Portal]
    end

    subgraph Access[Secure Access]
        direction LR
        EDGE[Secure Web Delivery]
        AUTH[Identity and Access]
        API[API and GraphQL Layer]
    end

    subgraph Platform[Cloud Platform]
        direction LR
        FLOW[Workflow Orchestration]
        EVENTS[Events and Queues]
        SERVICES[Domain Services]
    end

    subgraph Data[Data and Communications]
        direction LR
        DB[(Operational Data)]
        FILES[(Documents and Media)]
        NOTIFY[Email and Notifications]
    end

    subgraph Factory[Factory Integration]
        direction LR
        PRINT[Label and Document Printing]
        CLOCK[Time and Attendance]
    end

    B2B --> EDGE
    B2C --> EDGE
    ADMIN --> EDGE
    FLOOR --> EDGE
    DRIVER --> EDGE
    EDGE --> AUTH
    AUTH --> API
    API --> FLOW
    API --> SERVICES
    FLOW <--> EVENTS
    EVENTS <--> SERVICES
    SERVICES <--> DB
    SERVICES <--> FILES
    SERVICES --> NOTIFY
    EVENTS --> PRINT
    CLOCK --> API
```

### Order Lifecycle

```mermaid
flowchart TB
    subgraph Prepare[Plan and Prepare]
        direction LR
        ORDER[Order Received] --> VALIDATE[Policy and Capacity Validation]
        VALIDATE --> PLAN[Production Planning]
        PLAN --> PACK[Weight Capture and Packing]
    end

    subgraph Complete[Complete and Report]
        direction LR
        LABEL[Labels and Documents] --> DISPATCH[Dispatch and Driver Assignment]
        DISPATCH --> DELIVERY[Delivery Confirmation]
        DELIVERY --> FINANCE[Invoice and Reporting]
    end

    PACK --> LABEL

    VALIDATE -. exception .-> REVIEW[Human Review]
    PACK -. variance .-> REVIEW
    REVIEW --> PLAN
```

### AWS Services by Stage

| Stage | AWS services | Role in the platform |
|---|---|---|
| Web delivery and secure access | CloudFront, S3, Cognito, IAM | Deliver the web applications and enforce authenticated, role-based access |
| Order intake and APIs | AppSync, API Gateway, Lambda | Provide GraphQL and HTTP entry points for ordering and operational tools |
| Validation and operational data | Lambda, DynamoDB | Apply fresh-product rules and persist orders, capacity, inventory, and workflow state |
| Workflow orchestration and background processing | Step Functions, EventBridge, SQS, SNS | Coordinate workflows, schedule jobs, decouple services, and fan out events |
| Weight capture, packing, and factory output | Lambda, DynamoDB, SQS, S3 | Persist packed weights, queue print jobs, and store generated documents |
| Dispatch and driver delivery | AppSync, Lambda, DynamoDB, S3, EventBridge | Assign work, track delivery state, retain proof, and emit completion events |
| Invoicing, statements, and communication | Lambda, DynamoDB, S3, SES | Generate financial documents, archive them, and send customer communications |
| Time and attendance | API Gateway, Lambda, DynamoDB, S3, Cognito | Securely process punches, maintain live status, and generate timesheets |
| Monitoring and recovery | CloudWatch, X-Ray, CloudWatch Synthetics, SNS | Centralize logs, metrics, traces, health checks, and operational alerts |
| Voice and optional AI | Transcribe, Bedrock, Lambda | Support voice-assisted intake and optional generative operations alerts |

## Engineering Scope

- Event-driven services for order processing, fulfilment, dispatch, notifications, and reporting
- Fresh-product rules covering lead times, cutoffs, fulfilment dates, blackout dates, and capacity
- Cognito-backed, role-based web applications for administrators, factory staff, drivers, and managers
- Authorization-safe cache refresh for installed progressive web applications
- On-premises integration for thermal labels, business documents, and attendance devices
- Driver workflows for pickup, routing, location updates, proof of delivery, and completion
- Payment, invoice, statement, and variable-weight order workflows
- Monitoring, audit trails, retry handling, and operational recovery tooling
- Voice transcription and learning-assisted order intake, with optional generative operations alerts kept disabled

## Technology

**AWS:** Lambda, AppSync, API Gateway, Step Functions, DynamoDB, S3, CloudFront, EventBridge, SQS, SNS, SES, Cognito, IAM, CloudWatch, X-Ray, CloudWatch Synthetics, Bedrock, and Transcribe.

**Application tooling:** React, Node.js, Python, PowerShell, and Stripe.

## Design Priorities

- Keep production data and infrastructure details private
- Validate business rules on the server, not only in the interface
- Make failures observable and recoverable
- Design factory-facing tools for quick, repeated use
- Use managed cloud services where they reduce operational overhead
- Keep human approval available for financially or operationally sensitive decisions

## Repository Access

This is a portfolio overview of a proprietary production system. Source code and live environments are not publicly accessible.