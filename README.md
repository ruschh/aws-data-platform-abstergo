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