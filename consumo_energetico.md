# Consumo de Energia dos Componentes

## 1. Componentes

- **Microcontrolador ESP-WROOM-32:** processador Xtensa Dual-Core de 32 bits, com clock ajustável entre 80 MHz e 240 MHz; memória RAM estática de 520 KB; memória Flash de 4 MB; Wi-Fi integrado.
- **Sensor capacitivo de umidade do solo V1.2:** sensor de saída analógica específico para medição de umidade.
- **Sensor ultrassônico AJ-SR04M.**

## 2. Fórmulas utilizadas

```
P = V × I
```

em que P é a potência (W), V é a tensão (V) e I é a corrente (A).

```
E = (P × t) / 1000
```

em que E é a energia consumida (kWh), P é a potência (W) e t é o tempo de funcionamento (h).

**Tempo de funcionamento considerado:** t = 24 h (funcionamento contínuo por um dia).

## 3. ESP-WROOM-32

- **Corrente de consumo típica:** 80 mA
- **Tensão de alimentação:** 2,7 V a 3,6 V (será utilizada 3,3 V)

### Conversão da corrente

```
80 / 1000 = 0,08 A
```

### Potência

```
P = V × I
P = 3,3 × 0,08 = 0,264 W
```

### Energia consumida em 24 h

```
E = (P × t) / 1000
E = (0,264 × 24) / 1000 = 0,006336 kWh
```

## 4. Sensor Capacitivo de Umidade do Solo V1.2

- **Corrente de consumo típica:** 5 mA
- **Tensão de alimentação:** 3,3 V a 5,5 V (será utilizada 4,5 V)

### Conversão da corrente

```
5 / 1000 = 0,005 A
```

### Potência

```
P = V × I
P = 4,5 × 0,005 = 0,0225 W
```

### Energia consumida em 24 h

```
E = (P × t) / 1000
E = (0,0225 × 24) / 1000 = 0,00054 kWh
```

## 5. Sensor Ultrassônico AJ-SR04M

- **Corrente de consumo:** 40 mA
- **Tensão de alimentação:** 3,5 V a 5 V (será utilizada 4,5 V)

### Conversão da corrente

```
40 / 1000 = 0,04 A
```

### Potência

```
P = V × I
P = 4,5 × 0,04 = 0,18 W
```

### Energia consumida em 24 h

```
E = (P × t) / 1000
E = (0,18 × 24) / 1000 = 0,00432 kWh
```

## 6. Resumo do consumo
 
| Componente | Tensão (V) | Potência (W) | Energia em 24 h (kWh/dia) | Energia em 30 dias (kWh/mês) |
|---|:---:|:---:|:---:|:---:|
| ESP-WROOM-32 | 3,3 | 0,264 | 0,006336 | 0,19008 |
| Sensor de umidade do solo V1.2 | 4,5 | 0,0225 | 0,00054 | 0,0162 |
| Sensor ultrassônico AJ-SR04M | 4,5 | 0,18 | 0,00432 | 0,1296 |
| **Total** | - | **0,4665** | **0,011196** | **0,33588** |
 
O consumo mensal foi obtido multiplicando a energia diária por 30 dias: `E_mês = E_dia × 30`.
 
---

### Análise do consumo energético

Os componentes do sistema de irrigação proposto para hortas ou jardins comunitários é composto por 3 componentes principais
  1. O ESP-WROOM-32 para processamento, que foi escolhido pelo seu baixo custo
  2. Os sensores capacitivos de medição de umidade v1.2, usado para medir a umidade do solo, pondendo ser usado para calcular o percentual de umidade do solo
  3. O sensor ultrassônico AJ-SR04M, escolhido justamente por ser a prova d'agua, cumprira o papel de gerenciar a quantidade de água disponível para irrigação

**Premissas adotadas.**  
Para a estimativa, foram consideradas as seguintes premissas:

  1. Os componentes operam 24 horas por dia
  2. Utilizamos a corrente de consumo típica informadas pelos fabricantes, sem considerar picos de corrente que por exemplo ocorrem durante transmissão de Wi-Fi do ESP32
  3. Adotamos valores intermediarios dentro das faixas de alimentação especificadas pelos fabricantes para cada componente
  4. Não consideramos perdas de fonte ou de conversão de tensão.

**Interpretação.**

O consumo do sistema de irrigação é baixo, sendo de 0,33588/kWh por mês, tornando o projeto viável no caso de atendimento para bairros e pequenas comunidades
[sla dps volto aqui para elaborar mais nisso]
