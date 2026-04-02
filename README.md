# AWS Data Platform – Abstergo Industries

## Problema de Negócio

A distribuição farmacêutica exige controle rigoroso de estoque, otimização logística e análise contínua de custos operacionais. Em um cenário com múltiplas filiais, farmácias e fornecedores, a empresa precisa de uma arquitetura que combine alta disponibilidade, segurança, governança e capacidade analítica.

## Solução

Este projeto propõe uma arquitetura de data platform em AWS para uma empresa farmacêutica, combinando:

- Data Lake em Amazon S3
- ETL com AWS Glue
- Analytics serverless com Amazon Athena
- Camada operacional com EC2, RDS e Load Balancer
- Infraestrutura segura com VPC, subnets privadas, IAM e controles de rede

## Resultados Esperados

- redução de custo logístico  
- melhoria no SLA de entrega  
- maior governança de dados  
- separação entre sistemas transacionais e analíticos  
- base escalável para analytics e machine learning  

## Descrição

A arquitetura foi desenhada para separar claramente:

- **Camada operacional (OLTP)**: Route 53, ALB, EC2 e RDS/Aurora  
- **Camada de dados**: Amazon S3 com bronze, silver e gold  
- **Processamento**: AWS Glue para ETL e catálogo  
- **Consumo analítico**: Athena, dashboards e modelos  
- **Governança e segurança**: VPC, IAM, Security Groups, CloudWatch, CloudTrail e Lake Formation  

## Tecnologias

- AWS Route 53  
- AWS Application Load Balancer (ALB)  
- Amazon EC2  
- Amazon RDS / Aurora  
- Amazon S3  
- AWS Glue  
- Amazon Athena  
- AWS VPC  
- IAM  
- Security Groups  
- CloudWatch  
- CloudTrail  
- Lake Formation  

---

## Diagrama

```mermaid
flowchart TB

    A["Usuários / Filiais / Farmácias"] --> B["Route 53 / DNS"]

    subgraph VPC["AWS VPC"]
        subgraph PUB["Public Subnet"]
            C["Application Load Balancer"]
        end

        subgraph PRIVAPP["Private Subnet - Aplicação"]
            D1["EC2 - App Server 1"]
            D2["EC2 - App Server 2"]
        end

        subgraph PRIVDB["Private Subnet - Banco"]
            E["RDS / Aurora"]
        end
    end

    B --> C
    C --> D1
    C --> D2
    D1 --> E
    D2 --> E

    subgraph DATALAKE["Camada de Dados"]
        F["Amazon S3 (bronze / silver / gold)"]
    end

    subgraph ETL["ETL"]
        G["AWS Glue"]
    end

    subgraph ANALYTICS["Analytics"]
        H["Amazon Athena"]
        I["BI / Dashboards / ML"]
    end

    E --> G
    G --> F
    F --> H
    H --> I

    subgraph GOV["Governança e Segurança"]
        J["IAM"]
        K["Security Groups"]
        L["CloudWatch"]
        M["CloudTrail"]
        N["Lake Formation"]
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

## Estrutura do repositório

aws-data-platform-abstergo/
├── README.md
├── diagrams/
│   └── architecture.md
├── data-model/
│   └── facts_dims.md
├── etl/
│   └── glue_pipeline.md
└── docs/
    └── arquitetura_completa.md

## Link para documentação completa

[Veja o relatório completo](./docs)