# IBM Planning Analytics Chatbot Architecture
```mermaid
graph TD
    A[Business Users] --> B[Chatbot Gateway]
    B --> C[AI & Logic Layer (AWS Bedrock)]
    C --> D[IBM Planning Analytics (TM1 on IBM Cloud)]
    D --> E[Governance, Monitoring, FinOps]
