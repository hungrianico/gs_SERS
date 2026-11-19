# Consumo de Energia dos Componentes

## 1. Componentes

- **Microcontrolador ESP-WROOM-32:** processador Xtensa Dual-Core de 32 bits, com clock ajustável entre 80 MHz e 240 MHz; memória RAM estática de 520 KB; memória Flash de 4 MB; Wi-Fi integrado.
- **Sensor capacitivo de umidade do solo V1.2:** sensor de saída analógica específico para medição de umidade.
- **Sensor ultrassônico AJ-SR04M:** sensor à prova d'água, usado para medir o nível de água disponível.
- **Alimentação solar (proposta):** painel solar Ztroon ZTP-010MI (10 W, monocristalino), controlador de carga MPPT CN3791 (versão 12 V) e baterias de íon-lítio 18650. Este conjunto não consome energia do sistema: ele a fornece (ver seção 7).

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

Para o dimensionamento da alimentação solar (seção 7):

```
E_ger = P_painel × HSP × RD
```

em que E_ger é a energia gerada por dia (Wh/dia), P_painel é a potência de pico do painel (W), HSP são as horas de sol pleno do local (h/dia) e RD é o rendimento global do conjunto de geração (adimensional). Como as perdas não são consideradas, adota-se **RD = 1**.

```
P_painel,mín = E_dia / (HSP × RD)
C_bat (Wh) = (E_dia × N) / DoD
C_bat (Ah) = C_bat (Wh) / V_bat
```

em que E_dia é o consumo diário (Wh/dia), N é o número de dias de autonomia, DoD é a profundidade de descarga permitida e V_bat é a tensão nominal da bateria (V).

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

## 7. Alimentação solar

Painel de **10 W** (Ztroon ZTP-010MI). Não consideramos perdas (RD = 1), então a geração é o valor ideal.

**HSP (horas de sol pleno):** valor simulado. Adotamos HSP = 4 h/dia como premissa e um cenário mais pessimista de HSP = 3 h/dia.

```
E_ger = P_painel × HSP
HSP = 4 h: 10 × 4 = 40 Wh/dia
HSP = 3 h: 10 × 3 = 30 Wh/dia
```

| HSP | Geração (Wh/dia) | Consumo (Wh/dia) | Geração / consumo |
|:---:|:---:|:---:|:---:|
| 4 h | 40 | 11,196 | 3,57 |
| 3 h | 30 | 11,196 | 2,68 |

**Potência mínima do painel:**

```
HSP = 4 h: 11,196 / 4 = 2,8 W
HSP = 3 h: 11,196 / 3 = 3,7 W
```

**Bateria** (2 dias de autonomia, DoD = 0,8, bateria 18650 de 3,7 V e 2500 mAh):

```
C = (11,196 × 2) / 0,8 = 27,99 Wh
C = 27,99 / 3,7 = 7,57 Ah
7,57 / 2,5 = 3,03 → 4 baterias em paralelo
```

Como 3,03 é maior que 3, três baterias não seriam suficientes, por isso o resultado foi arredondado para 4.

**Observação sobre as tensões:** a bateria tem tensão nominal de 3,7 V, enquanto o ESP-WROOM-32 opera em 3,3 V e os sensores em 4,5 V. Por isso, o sistema precisa de conversores de tensão (regulador e/ou boost), cujas perdas não foram consideradas nesta etapa.

## 8. Texto para o relatório

### Análise do consumo energético

O sistema de irrigação proposto para hortas ou jardins comunitários é composto por 3 componentes principais:

1. O ESP-WROOM-32, que faz o processamento e foi escolhido pelo baixo custo.
2. O sensor capacitivo de umidade do solo V1.2, que mede a umidade do solo e permite calcular o percentual de umidade.
3. O sensor ultrassônico AJ-SR04M, escolhido por ser à prova d'água, que vai medir a quantidade de água disponível para a irrigação.

**Premissas adotadas.** Para a estimativa, consideramos:

1. Os componentes operam 24 horas por dia.
2. Utilizamos a corrente de consumo típica informada pelos fabricantes, sem considerar picos de corrente, que por exemplo ocorrem durante a transmissão Wi-Fi do ESP32.
3. Adotamos tensões dentro das faixas de alimentação especificadas pelos fabricantes de cada componente.
4. Não consideramos perdas de fonte, de conversão de tensão nem do sistema solar (RD = 1).
5. Para a geração solar, usamos um valor simulado de 4 horas de sol pleno por dia (HSP), e 3 horas no cenário pessimista.
6. O escopo desta análise se limita ao microcontrolador, aos dois sensores e à alimentação solar descritos acima.

### Análise

O consumo do sistema é baixo, de 0,336 kWh por mês (cerca de 11,2 Wh por dia), o que torna o projeto viável para bairros e pequenas comunidades.

Por ser tão baixo, dá para alimentar tudo com energia solar. Um painel de 10 W gera cerca de 40 Wh por dia com 4 horas de sol pleno (valor simulado), mais de 3 vezes o que o sistema consome, e 4 baterias 18650 garantem 2 dias de autonomia sem sol. Assim, nas premissas adotadas (HSP simulado e sem perdas), 100% da energia usada pelo sistema vem de fonte renovável.
