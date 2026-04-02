# Pipeline ETL – AWS Glue

## Visão Geral

O pipeline ETL é responsável por mover dados da camada operacional (RDS) para o Data Lake (S3), transformando-os em dados analíticos prontos para consumo.

---

## Arquitetura do Pipeline

```text
RDS → Glue → S3 (Bronze → Silver → Gold) → Athena
```

## Etapas do Pipeline

1. Extração

	Fonte:
		- RDS (PostgreSQL / MySQL)

		- APIs externas

		- Arquivos CSV

	Processo:

		- Leitura incremental (por timestamp)

		- Conexão via JDBC

2. Transformação

	Operações:

		- Limpeza de dados

		- Tratamento de nulos

		- Padronização de tipos

		- Enriquecimento (KPIs)

	Exemplos:

	- cálculo de custo por pedido

	- normalização de categorias

	- agregações por região

3. Carga

	Destino: Amazon S3

	Estrutura:

		s3://abstergo-data/
 		 ├── bronze/
 		 ├── silver/
 		 └── gold/

	Formato:
		- Parquet

		- Particionado por data

## Estratégia de Carga

- Incremental (CDC ou timestamp)

- Evita reprocessamento completo

## Tratamento de Erros

- retries automáticos

- logs no CloudWatch

## Catálogo de Dados

- AWS Glue Data Catalog

- Registro automático de tabelas

- Integração com Athena

## Orquestração

- Jobs Glue agendados

- Execução diária ou near real-time

## Monitoramento

- CloudWatch Logs

- Métricas de execução

- Alertas de falha

## Boas Práticas

- Idempotência no ETL

- Versionamento de dados

- Particionamento eficiente

- Controle de schema

## Benefícios

- Pipeline serverless

- Escalabilidade automática

- Redução de custo operacional

- Integração nativa com AWS Analytics

## Evoluções Futuras

- Streaming (Kinesis)

- Feature Store para ML

- Data Quality (Great Expectations)