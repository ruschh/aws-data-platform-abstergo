# AWS Data Platform – Abstergo Industries

## Problema de Negócio

Distribuição farmacêutica exige:

- controle de estoque

- otimização logística

- análise de custos

## Solução

Arquitetura AWS baseada em:

- Data Lake (S3)

- ETL (Glue)

- Analytics (Athena)

## Resultados esperados

- redução de custo logístico

- melhoria no SLA

- governança de dados

## Descrição

Arquitetura de data platform em AWS para empresa farmacêutica, incluindo:

	- Data Lake (S3)

	- ETL (Glue)

	- Analytics (Athena)

	- Infraestrutura segura (VPC, subnets privadas, IAM)

---
 
## Diagrama

```mermaid
flowchart TB

    A[Usuários / Filiais / Farmácias] --> B[Route 53 / DNS]
    B --> C[Application Load Balancer (ALB / ELB)]

    subgraph VPC["AWS VPC"]
        subgraph PUB["Public Subnet"]
            C
        end

        subgraph PRIVAPP["Private Subnet - Aplicação"]
            D1[EC2 - App Server 1<br/>ERP / API / Portal / Order Processing]
            D2[EC2 - App Server 2<br/>ERP / API / Portal / Order Processing]
        end

        subgraph PRIVDB["Private Subnet - Banco"]
            E[RDS / Aurora<br/>Dados Transacionais]
        end
    end

    C --> D1
    C --> D2
    D1 --> E
    D2 --> E

    subgraph DATALAKE["Camada de Dados"]
        F[Amazon S3<br/>bronze / silver / gold<br/>logs / backups]
    end

    subgraph ETL["ETL e Consultas Analíticas"]
        G[AWS Glue<br/>catálogo + ETL]
        H[Amazon Athena<br/>SQL sobre dados no S3]
    end

    subgraph ANALYTICS["Consumo Analítico"]
        I[BI / Dashboards / DS / ML<br/>Streamlit / notebooks / modelos preditivos]
    end

    E --> G
    G --> F
    F --> H
    H --> I

    subgraph GOV["Governança / Operação / Segurança"]
        J[IAM<br/>acessos]
        K[Security Groups<br/>firewall / rede]
        L[CloudWatch<br/>métricas / logs]
        M[CloudTrail<br/>auditoria]
        N[Lake Formation<br/>governança S3]
    end

    J -.-> D1
    J -.-> D2
    J -.-> F
    K -.-> C
    K -.-> D1
    K -.-> D2
    K -.-> E
    L -.-> C
    L -.-> D1
    L -.-> D2
    L -.-> E
    M -.-> C
    M -.-> E
    N -.-> F
```

## Link para documentação completa

[Veja o relatório completo](./docs)