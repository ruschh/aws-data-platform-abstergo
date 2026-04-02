# Arquitetura AWS – Abstergo Industries

## Visão Geral

Esta arquitetura representa uma plataforma moderna de dados em AWS para uma empresa farmacêutica com operações logísticas distribuídas. A solução separa claramente:

- Camada operacional (OLTP)

- Camada de dados (Data Lake)

- Camada analítica (OLAP)

- Governança e segurança

---

## Diagrama de Arquitetura

```mermaid
flowchart TB

    A[Usuários / Filiais / Farmácias] --> B[Route 53 / DNS]
    B --> C[Application Load Balancer (ALB)]

    subgraph VPC["AWS VPC"]
        subgraph PUB["Public Subnet"]
            C
        end

        subgraph PRIVAPP["Private Subnet - Aplicação"]
            D1[EC2 - App Server 1]
            D2[EC2 - App Server 2]
        end

        subgraph PRIVDB["Private Subnet - Banco"]
            E[RDS / Aurora]
        end
    end

    C --> D1
    C --> D2
    D1 --> E
    D2 --> E

    subgraph DATALAKE["Data Lake (S3)"]
        F[Bronze]
        G[Silver]
        H[Gold]
    end

    subgraph PROCESSING["ETL"]
        I[AWS Glue]
    end

    subgraph ANALYTICS["Analytics"]
        J[Athena]
        K[Dashboards / ML]
    end

    E --> I
    I --> F
    F --> G
    G --> H

    H --> J
    J --> K
    ```

## Componentes

### Camada Operacional

- Route 53: DNS e roteamento

- ALB: balanceamento de carga

- EC2: aplicação (ERP, APIs)

- RDS: banco transacional (OLTP)

### Camada de Dados
- Amazon S3:
    * Bronze: dados brutos

    * Silver: dados tratados

    * Gold: dados analíticos

### Processamento
- AWS Glue:

    * ETL

    * Data Catalog

### Analytics

- Athena:
    * consultas SQL serverless

- Dashboards / ML:
    * Streamlit, notebooks, modelos

### Segurança

- VPC com subnets públicas e privadas

- IAM

- Security Groups

- CloudWatch / CloudTrail

- Lake Formation

### Princípios da Arquitetura

- Separação OLTP vs OLAP

- Processamento serverless

- Escalabilidade horizontal

- Segurança por isolamento de rede

- Governança de dados centralizada

### Benefícios

- Redução de custos (pay-as-you-go)

- Alta disponibilidade

- Escalabilidade

- Flexibilidade analítica

- Base para machine learning

