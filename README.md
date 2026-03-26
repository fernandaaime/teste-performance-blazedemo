# Teste Performance - BlazeDemo

Testes de performance para o site BlazeDemo utilizando JMeter + Maven.

## Cenario

Compra de passagem aerea completa:
1. Acessar a home
2. Selecionar voo (Paris -> Buenos Aires)
3. Preencher dados e confirmar compra

## Tipos de Teste

### Teste de Carga (blazedemo-load-test.jmx)
Simula o uso normal e sustentado do sistema.
- 250 usuarios simultaneos
- Ramp-up de 10 segundos
- Duracao de 60 segundos

### Teste de Pico (blazedemo-spike-test.jmx)
Simula um pico repentino de acessos acima do normal.
- 500 usuarios simultaneos
- Ramp-up de 5 segundos (subida rapida para simular o pico)
- Duracao de 30 segundos

## Criterio de Aceitacao

- 250 requisicoes por segundo
- Tempo de resposta 90th percentil inferior a 2 segundos

## Resultado da Execucao

### Teste de Carga
| Metrica           | Resultado | Criterio     | Status |
|-------------------|-----------|--------------|--------|
| Throughput        | ~230 req/s| 250 req/s    | ⚠️     |
| Tempo medio       | 959ms     | P90 < 2000ms | ✅     |
| Taxa de erro      | 0%        | < 10%        | ✅     |
| Total requisicoes | ~14.600   | -            | ✅     |

### Teste de Pico
| Metrica           | Resultado | Criterio     | Status |
|-------------------|-----------|--------------|--------|
| Throughput        | ~230 req/s| 250 req/s    | ⚠️     |
| Tempo medio       | ~1200ms   | P90 < 2000ms | ✅     |
| Taxa de erro      | 0%        | < 10%        | ✅     |

## Analise do Criterio de Aceitacao

O sistema atingiu aproximadamente 230 req/s, ligeiramente abaixo do criterio de 250 req/s.

**Conclusao:** O criterio de aceitacao foi PARCIALMENTE satisfeito.

**Pontos positivos:**
- Taxa de erro zerada em ambos os testes, demonstrando estabilidade
- Tempo de resposta medio abaixo de 2 segundos mesmo sob pico de 500 usuarios
- O sistema se comportou de forma consistente sob carga sustentada e pico

**Pontos de atencao:**
- O throughput ficou ~8% abaixo do criterio de 250 req/s
- Esse gap pode ser causado por limitacoes da infraestrutura do blazedemo.com
- Em um ambiente real, recomendaria investigar gargalos no servidor (CPU, memoria, banco de dados) antes de aprovar o deploy

## Tecnologias

- JMeter 5.6.2
- Maven 3.9.x
- Java 17
- jmeter-maven-plugin 3.8.0

## Pre-requisitos

- Java JDK 17+
- Maven 3.9+

## Como executar

### Teste de carga
```bash
mvn clean verify
```

### Apenas um teste especifico
```bash
mvn jmeter:configure jmeter:jmeter -Djmeter.test=blazedemo-load-test
mvn jmeter:configure jmeter:jmeter -Djmeter.test=blazedemo-spike-test
```