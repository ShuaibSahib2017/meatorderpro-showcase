# Shuaib Sahib

## Cloud and Full-Stack Systems Builder

I design and operate practical software that connects customer ordering, factory workflows, dispatch, delivery, invoicing, printing, and workforce operations.

My focus is turning real operational constraints into reliable systems: clear service boundaries, event-driven workflows, secure access, observable production services, and tools that work for both office and factory teams.

## Featured Project: MeatOrderPro

MeatOrderPro is a private production platform built for an Australian meat processing and distribution business. It coordinates wholesale and retail orders from checkout through fulfilment, dispatch, delivery, invoicing, and reporting.

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

## Engineering Scope

- Event-driven services for order processing, fulfilment, dispatch, notifications, and reporting
- Fresh-product rules covering lead times, cutoffs, fulfilment dates, blackout dates, and capacity
- Role-based web applications for administrators, factory staff, drivers, and managers
- On-premises integration for thermal labels, business documents, and attendance devices
- Payment, invoice, statement, and variable-weight order workflows
- Monitoring, audit trails, retry handling, and operational recovery tooling
- AI-assisted order intake and workflow suggestions with human review controls

## Technology

AWS Lambda, AppSync, API Gateway, Step Functions, DynamoDB, S3, CloudFront, EventBridge, SQS, SES, Cognito, CloudWatch, React, Node.js, Python, and PowerShell.

## Design Priorities

- Keep production data and infrastructure details private
- Validate business rules on the server, not only in the interface
- Make failures observable and recoverable
- Design factory-facing tools for quick, repeated use
- Use managed cloud services where they reduce operational overhead
- Keep human approval available for financially or operationally sensitive decisions

## Repository Access

This is a portfolio overview of a proprietary production system. Source code and live environments are not publicly accessible.