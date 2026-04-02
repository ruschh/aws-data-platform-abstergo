# Modelo de Dados – Abstergo Industries

## Visão Geral

O modelo segue o padrão dimensional (Kimball), com separação em:

- Tabelas fato (facts)

- Tabelas dimensão (dimensions)

Utilizado na camada **Gold do Data Lake (S3)**.

---

## Tabelas Fato

### fact_orders
Representa pedidos realizados pelas farmácias.

Campos principais:

- order_id

- customer_id

- product_id

- date_key

- quantity

- total_value

---

### fact_inventory

Controle de estoque.

Campos:

- product_id

- date_key

- stock_level

- warehouse_id

---

### fact_logistics

Dados de transporte e entrega.

Campos:
- shipment_id

- order_id

- delivery_time

- cost

- region

---


## Granularidade

fact_orders:

- nível: pedido individual

fact_inventory:

- nível: produto por dia

fact_logistics:

- nível: entrega

---

## Tabelas Dimensão

### dim_product
- product_id

- nome

- categoria

- shelf_life

---

### dim_customer

- customer_id

- tipo_cliente

- região

---

### dim_time

- date_key

- data

- mês

- ano

---

### dim_location

- location_id

- cidade

- estado

- região

---

## Relacionamentos

- fact_orders → dim_product

- fact_orders → dim_customer

- fact_orders → dim_time

- fact_logistics → fact_orders

- fact_inventory → dim_product

---

## KPIs Derivados

- Custo logístico médio

- Giro de estoque

- SLA de entrega

- Perdas por vencimento

---

## Observações Técnicas

- Armazenamento em formato Parquet

- Particionamento por data (date_key)

- Consultas via Athena

- Catálogo via Glue

---

## Benefícios

- Alto desempenho em consultas analíticas

- Baixo custo de armazenamento

- Facilidade de expansão

- Compatibilidade com BI e ML