# Teste Performance - BlazeDemo

Teste de performance para o site BlazeDemo utilizando JMeter + Maven.

## Cenario

- Compra de passagem aerea (Paris -> Buenos Aires)

## Criterio de Aceitacao

- 250 requisicoes por segundo
- Tempo de resposta P90 inferior a 2 segundos

## Resultado da Execucao

- Total de requisicoes: ~14.600
- Taxa de erro: 0%
- Throughput: ~230 req/s
- Tempo medio de resposta: 959ms

## Tecnologias

- JMeter 5.6.2
- Maven 3.9.x
- Java 17
- jmeter-maven-plugin 3.8.0

## Pre-requisitos

- Java JDK 17+
- Maven 3.9+

## Como executar
```bash
mvn verify
```