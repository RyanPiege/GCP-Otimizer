# Otimização de Custo · Banco Corporativo GCP (BigQuery)

Refatoração de consultas e padronização de boas práticas para reduzir processamento e custo em tabelas de BigData.

**Status:** Encerrado · **Responsável:** [preencher] · **Período:** [preencher]

## Resultados

| Indicador | Resultado |
|---|---|
| Volume de dados processado | **−60%** |
| Custo mensal BigQuery (jul/25 → ago/25 previsto) | R$ 8.227,85 → R$ 3.718,09 |
| **Economia mensal** | **R$ 4.509,76 (−54,81%)** |
| Tempo de resposta | [preencher] |

> Agosto/2025 é parcial: realizado de 1 a 11/ago (R$ 1.663,25) + previsão do Cloud Billing. Atualizar após o fechamento do mês.

## Problema

Tabelas de **28 a 48 colunas e mais de 500 mil linhas** eram consultadas com `SELECT *`. No BigQuery o custo é proporcional aos bytes lidos nas colunas referenciadas, e `LIMIT` não reduz o faturamento. Resultado: processamento e custo pagos por colunas que ninguém usava.

## Solução

Substituir `SELECT *` pela lista das colunas realmente necessárias em cada consulta.

```sql
-- Antes: lê todas as colunas (28 a 48)
SELECT * FROM `projeto.dataset.tabela`

-- Depois: lê só o necessário
SELECT coluna_a, coluna_b, coluna_c FROM `projeto.dataset.tabela`
```
## Estrutura

```text
.
├── README.md
├── docs/          # apresentação (pptx/pdf)
├── sql/
│   ├── antes/     # consultas originais
│   └── depois/    # consultas refatoradas
└── evidencias/    # prints do Cloud Billing
```
## Padrões para novos projetos

- Não usar `SELECT *` em tabelas de produção.
- Rodar *dry run* antes de consultas novas em tabelas grandes.
- Definir `maximum_bytes_billed` em consultas recorrentes.
- [Incluir outros padrões aplicados, se houver]

## Próximos passos

Replicar o padrão em novos projetos · acompanhar o consumo mensal · registrar lições aprendidas.
