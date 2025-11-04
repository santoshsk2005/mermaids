```mermaid
graph TD
    %% High-Level Architecture Diagram for IBM Planning Analytics Chatbot (AWS + IBM Cloud)

    subgraph Users
        A1[Business Users (Finance, HR, Ops)]
        A2[Analysts & Admins]
    end

    subgraph Access Layer
        B1[Web / Teams / Slack Interface]
        B2[Chatbot Gateway API (AWS API Gateway)]
        B3[SSO Authentication (AWS Cognito / Okta)]
    end

    subgraph AI & Logic Layer (AWS)
        C1[Intent Recognition & Orchestration (Lambda + Bedrock Agent)]
        C2[RAG Pipeline (LangChain / Bedrock Knowledge Base)]
        C3[Prompt Engineering & Response Formatter]
        C4[Human-in-the-Loop Validation Portal]
    end

    subgraph Integration Layer
        D1[Secure API Tunnel (AWS PrivateLink)]
        D2[IBM Planning Analytics (TM1 REST API on IBM Cloud)]
        D3[Data Access Policy Layer (Row/Column Security)]
    end

    subgraph Data & Governance Layer
        E1[Metadata Catalog (AWS Glue + Alation Integration)]
        E2[Data Quality & Masking Rules]
        E3[Audit & Lineage Logs (AWS CloudTrail / CloudWatch)]
        E4[Access Control Policies (IAM + ABAC)]
    end

    subgraph Monitoring & FinOps
        F1[Cost Tracking Dashboard (AWS Cost Explorer + QuickSight)]
        F2[Model Monitoring & Drift Detection (SageMaker Model Monitor)]
        F3[Performance Metrics (CloudWatch + Prometheus)]
    end

    subgraph Continuous Learning
        G1[Feedback Store (DynamoDB / S3)]
        G2[Retraining Pipeline (SageMaker Pipelines)]
        G3[Prompt & Policy Refinement Loop]
    end

    %% Connections
    A1 -->|Natural Language Query| B1 --> B2 --> B3 --> C1
    C1 --> C2 -->|Query Context| D1 --> D2
    D2 -->|Filtered TM1 Data| D3 --> C3 -->|Response| B1 --> A1
    A2 -->|Review / Approve| C4 --> C3

    %% Governance & Monitoring
    C2 --> E1
    D3 --> E2
    E1 --> E3
    E3 --> F3
    F1 -->|Cost Alerts| A2
    F2 --> G1 --> G2 --> G3 --> C2

    %% Notes Section
    classDef header fill:#005EB8,stroke:#fff,color:#fff;
    classDef tech fill:#E5F3FF,stroke:#005EB8,color:#000;
    classDef control fill:#FDF5E6,stroke:#E3A008,color:#000;

    class B1,B2,B3 tech;
    class C1,C2,C3,C4 tech;
    class D1,D2,D3 tech;
    class E1,E2,E3,E4 control;
    class F1,F2,F3,G1,G2,G3 control;

    %% Business Value Summary
    %% - Democratizes access to TM1 data through conversational interface
    %% - Maintains strict data governance and PII protection
    %% - Enables real-time insight generation with human oversight
    %% - Reduces time to decision, lowers manual workload
    %% - Delivers transparent cost visibility and scalable AI operations
