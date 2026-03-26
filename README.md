# Teste Técnico de Performance - BlazeDemo

Este repositório contém uma automação de testes de performance para o fluxo de **compra de passagem aérea** no site [BlazeDemo](https://www.blazedemo.com), utilizando **Apache JMeter**.

## Objetivo

Validar o cenário:

- Compra de passagem aérea
- Resultado esperado: **Passagem comprada com sucesso**

## Critério de aceitação

- **250 requisições por segundo**
- **Tempo de resposta no percentil 90 inferior a 2 segundos**

## Estratégia adotada

Foram criados dois cenários:

### 1. Teste de carga
Objetivo: validar comportamento sustentado próximo ao critério de aceitação.

### 2. Teste de pico
Objetivo: validar comportamento do sistema sob subida rápida de carga, atingindo e ultrapassando momentaneamente a meta.

## Estrutura do projeto

```text
blazedemo-jmeter-performance/
├── README.md
├── data/
│   └── passengers.csv
├── docs/
│   └── execution-report-template.md
├── jmeter/
│   ├── blazedemo_load_test.jmx
│   └── blazedemo_spike_test.jmx
└── results/
```

## Pré-requisitos

- Java 8+
- Apache JMeter 5.6+

## Como executar

### Teste de carga

```bash
jmeter -n -t jmeter/blazedemo_load_test.jmx -l results/load_results.jtl -e -o results/load_report
```

### Teste de pico

```bash
jmeter -n -t jmeter/blazedemo_spike_test.jmx -l results/spike_results.jtl -e -o results/spike_report
```

## O que validar no relatório

Após a execução, analisar principalmente:

- **Throughput**
- **90th percentile**
- **Error %**
- **Response Times Over Time**
- **Transactions per Second**

## Conclusão esperada

A conclusão deve ser registrada após a execução real. Use o template em `docs/execution-report-template.md`.

Modelo de avaliação:

- **Critério atendido**: quando o throughput alcançar pelo menos 250 req/s e o percentil 90 ficar abaixo de 2 segundos.
- **Critério não atendido**: quando um ou ambos os indicadores ficarem fora da meta.

## Observações técnicas

- O fluxo navega pelas páginas principais do BlazeDemo até a confirmação da compra.
- Foram adicionados headers, cookie manager, cache manager e assertions básicas de resposta.
- O teste usa dados parametrizados para compra.
- Como o BlazeDemo é um site público de demonstração, resultados podem variar conforme disponibilidade e latência externa.

## Sugestão de nome para o repositório

`blazedemo-jmeter-performance-test`

## Sugestão de descrição do repositório

Teste técnico de performance com Apache JMeter para o fluxo de compra de passagem aérea no BlazeDemo, incluindo testes de carga, pico, relatório e análise de critério de aceitação.

## Como subir para o GitHub

```bash
git init
git add .
git commit -m "feat: add JMeter performance test for BlazeDemo flight purchase flow"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/blazedemo-jmeter-performance-test.git
git push -u origin main
```

## Resultado da execução - Teste de carga

- Throughput médio: 243.99 req/s
- p90: 1434.90 ms
- Taxa de erro: 0.00%
- Tempo médio: 646.72 ms

## Conclusão

O sistema apresentou estabilidade durante a execução, com 0% de erros e p90 abaixo de 2 segundos. No entanto, o throughput médio consolidado ficou ligeiramente abaixo da meta de 250 req/s. Dessa forma, o critério de aceitação foi parcialmente atendido: o requisito de latência foi cumprido, mas a vazão mínima não foi sustentada de forma consistente ao longo de toda a execução.
