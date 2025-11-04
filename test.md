```mermaid
graph TD
    %% High-Level Architecture for IBM Planning Analytics Chatbot (AWS + IBM Cloud)

    subgraph Users
        A1[Business Users: Finance, HR, Ops]
        A2[Analysts and Admins]
    end

    subgraph Access_Layer
        B1[Web or Teams or Slack Interface]
        B2[Chatbot Gateway API (AWS API Gateway)]
        B3[SSO Authentication (Cognito or Okta)]
    end

    subgraph AI_and_Logic_Layer_AWS
        C1[Intent Recognition and Orchestration (Lambda + Bedrock)]
        C2[RAG Pipeline (LangChain or Knowledge Base)]
        C3[Prompt Engineering and Response Formatter]
        C4[Human-in-the-Loop Validation Portal]
    end

    subgraph Integration_Layer
        D1[Secure API Tunnel (AWS PrivateLink)]
        D2[IBM Planning Analytics TM1 REST API on IBM Cloud]
        D3[Data Access Policy Layer: Row/Column Security]
    end

    subgraph Data_and_Governance_Layer
        E1[Metadata Catalog (AWS Glue + Alation)]
        E2[Data Quality and Masking Rules]
        E3[Audit and Lineage Logs (CloudTrail)]
        E4[Access Control Policies (IAM)]
    end

    subgraph Monitoring_and_FinOps
        F1[Cost Tracking Dashboard (Cost Explorer + QuickSight)]
        F2[Model Monitoring and Drift Detection (SageMaker)]
        F3[Performance Metrics (CloudWatch)]
    end

    subgraph Continuous_Learning
        G1[Feedback Store (DynamoDB or S3)]
        G2[Retraining Pipeline (SageMaker Pipelines)]
        G3[Prompt and Policy Refinement Loop]
    end

    %% Connections
    A1 --> B1 --> B2 --> B3 --> C1
    C1 --> C2 --> D1 --> D2 --> D3 --> C3 --> B1 --> A1
    A2 --> C4 --> C3
    C2 --> E1 --> E3
    D3 --> E2
    E3 --> F3
    F1 --> A2
    F2 --> G1 --> G2 --> G3 --> C2
