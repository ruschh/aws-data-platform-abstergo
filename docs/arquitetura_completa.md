# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

Data: 02/04/2026

Empresa: Abstergo Industries 

Responsável: Flavio R. Rusch

## Introdução
Este relatório apresenta o processo de implementação de ferramentas na empresa Abstergo Industries, realizado por Flavio R. Rusch. O objetivo do projeto é elencar, no mínimo 3 serviços AWS, com a finalidade de realizar diminuição de custos imediatos, aumento de escalabilidade e melhoria da segurança da infraestrutura por meio da adoção de arquitetura em nuvem baseada em VPC.

## Descrição do Projeto
O projeto de implementação de ferramentas foi dividido em 3 etapas, cada uma com seus objetivos específicos. A seguir, serão descritas as etapas do projeto:

**Etapa 1**: Camada operacional

- **Nome da ferramenta 1**: Route 53

- **Foco da ferramenta 1**: Resolução de DNS e roteamento de requisições.

- **Descrição de caso de uso**: O Route 53 é responsável por receber as requisições externas provenientes de farmácias, filiais e parceiros, realizando a resolução de domínio e encaminhando o tráfego para o Application Load Balancer.

---

- **Nome da ferramenta 2**: ELB (Elastic Load Balancing)

- **Foco da ferramenta 2**: Distribuição de tráfego entre instâncias EC2.

- **Descrição de caso de uso**: O Application Load Balancer (ALB) recebe as requisições externas e distribui o tráfego entre múltiplas instâncias EC2. Esse componente está localizado em subnets públicas dentro de uma VPC e atua como ponto de entrada seguro para a aplicação.

---

- **Nome da ferramenta 3**: instâncias EC2 (Elastic Compute Cloud)

- **Foco da ferramenta 3**: Execução da camada de aplicação.

- **Descrição de caso de uso**: As instâncias EC2 hospedam os sistemas da Abstergo (ERP, APIs, processamento de pedidos). Elas são implantadas em subnets privadas, sem acesso direto à internet, sendo acessadas exclusivamente via Load Balancer. Essa abordagem melhora a segurança e permite escalabilidade horizontal.

---

- **Nome da ferramenta 4**: RDS / Aurora

- **Foco da ferramenta 4**: Armazenamento de dados transacionais.

- **Descrição de caso de uso**: O Amazon RDS armazena os dados operacionais da empresa, incluindo pedidos, clientes e informações logísticas. O banco é provisionado em subnets privadas com configuração Multi-AZ, garantindo alta disponibilidade, resiliência e isolamento da camada de dados.

---

**Etapa 2**: Camada de dados

- **Nome da ferramenta 1**: Amazon S3

- **Foco da ferramenta 1**: Armazenamento de dados em formato de data lake.

- **Descrição de caso de uso**: O Amazon S3 é utilizado como repositório central de dados, organizado em três camadas:

        - bronze: dados brutos provenientes do RDS e sistemas externos

        - silver: dados tratados e padronizados

        - gold: dados analíticos estruturados (facts e dimensions)

Além disso, o S3 armazena logs do ALB, logs de aplicação e backups, sendo acessado de forma segura por meio de políticas IAM e controle de acesso refinado.

---

**Etapa 3**: ETL e consultas analíticas

- **Nome da ferramenta 1**: AWS Glue

- **Foco da ferramenta 1**: Processamento e transformação de dados.

- **Descrição de caso de uso**: O AWS Glue realiza o processo ETL, extraindo dados do RDS, transformando-os (limpeza, padronização e enriquecimento) e carregando-os no S3. Também gerencia o catálogo de dados, permitindo que os datasets sejam organizados e consultados.

---

- **Nome da ferramenta 2**: Athena

- **Foco da ferramenta 2**: Consulta analítica de dados.

- **Descrição de caso de uso**: O Amazon Athena permite executar consultas SQL diretamente sobre os dados armazenados no S3, possibilitando análises de negócio, dashboards e validação de dados sem necessidade de infraestrutura dedicada.

---

**Etapa 4**: Governança e Segurança

- **Nome da ferramenta 1**: VPC (Virtual Private Cloud)

- **Foco da ferramenta 1**: Isolamento de rede.

- **Descrição de caso de uso**: A VPC define a rede virtual onde todos os recursos são provisionados, permitindo segmentação entre subnets públicas (ALB) e privadas (EC2 e RDS), aumentando a segurança da arquitetura.

---

- **Nome da ferramenta 2**: Security Groups

- **Foco da ferramenta 2**: Controle de tráfego de rede.

- **Descrição de caso de uso**: Os Security Groups atuam como firewalls virtuais, permitindo controlar quais serviços podem se comunicar entre si (ex: ALB → EC2 → RDS).

---

- **Nome da ferramenta 3**: IAM

- **Foco da ferramenta 3**: Controle de acesso.

- **Descrição de caso de uso**: O IAM gerencia permissões de usuários e serviços, garantindo acesso seguro aos recursos AWS, incluindo S3, Glue e Athena.

---

- **Nome da ferramenta 4**: CloudWatch e CloudTrail

- **Foco da ferramenta 4**: Monitoramento e auditoria.

- **Descrição de caso de uso**: O CloudWatch monitora métricas e logs da aplicação, enquanto o CloudTrail registra ações realizadas na conta AWS, garantindo rastreabilidade e conformidade.

---

- **Nome da ferramenta 5**: Lake Formation

- **Foco da ferramenta 5**: Governança de dados.

- **Descrição de caso de uso**: O Lake Formation permite gerenciar permissões e acesso aos dados armazenados no S3, garantindo governança sobre o data lake.

---

## Fluxo de dados


```mermaid
                Usuários / Farmácias  
                        ↓   
                     Route 53  
                        ↓  
           Application Load Balancer (ALB)  
                        ↓  
           Instâncias EC2 (subnets privadas)  
                        ↓  
           RDS / Aurora (dados transacionais)  
                        ↓  
                 AWS Glue (ETL)  
                        ↓  
   Amazon S3 (bronze → silver → gold + logs + backups)  
                        ↓  
             Athena (consultas SQL)  
                        ↓  
         Dashboards / BI / Machine Learning  
```
---

## Conclusões

A arquitetura proposta para a Abstergo Industries estabelece uma infraestrutura moderna baseada em cloud computing, com separação clara entre camadas operacionais, analíticas e de governança.

A utilização de VPC, subnets privadas e controles de acesso garante maior segurança, enquanto o uso de serviços gerenciados como S3, Glue e Athena reduz custos operacionais e aumenta a escalabilidade.

Essa abordagem permite à empresa evoluir para soluções avançadas de analytics e machine learning, mantendo eficiência, governança e alta disponibilidade.