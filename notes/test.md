
```mermaid
  User[Customers (Web/Mobile)] --> CF[CloudFront + WAF + AWS Shield]
  CF --> ALB[Application Load Balancer]

  subgraph App[Application Layer]
    ALB --> FE[Frontend ECS Fargate (Apache)]
    ALB --> BE[Backend ECS Fargate (.Net Core)]
    BE --> RDS[(Aurora Database)]
    BE --> Cache[(ElastiCache)]
  end

  FE --> S3[S3 Product Images]
  S3 --> CF

  subgraph AI[AI/ML Services]
    Forecast[Amazon Forecast]
    Personalize[Amazon Personalize]
    Forecast --> BE
    Personalize --> BE
  end

  subgraph Sec[Security & Governance]
    WAF[AWS WAF/Shield]
    Guard[GuardDuty/Security Hub]
    Config[AWS Config + CloudTrail]
    KMS[KMS Key Mgmt]
  end

  subgraph Ops[Operations]
    CW[CloudWatch + X-Ray]
    SSM[AWS Systems Manager]
    Backup[AWS Backup]
  end

  App --- Sec
  App --- Ops
```