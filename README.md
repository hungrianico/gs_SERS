# gs_SERS


[]Diagrama conceitual de funcionamento;  
[]Código ou componentes desenvolvidos para integração ao dashboard;  
[]O diagrama conceitual da solução;  


# Diagnóstico do problema
## Espaço escolhido: Jardim ou horta comunitária
Escolhemos esse espaço porque conseguimos levantar uma solução energética sustentavel com base em uma arquitetura já elaborada para a entrega de **Arquitetura e Organização de Computadores** que consiste em sensores capacitivos que fazem uma leitura elétrica do solo, permitindo um calculo percentual da umidade volumétrica do plantio. 

## Público beneficiado:
O projeto beneficiaria membros de uma comunidade ou bairro com uma horta com irrigação inteligente e energéticamente eficiente e sustentavel.

## Condições de funcionamento da solução:
Para o funcionamento da solução precisamos de  
  1. Um microcontrolador ESP-WROOM-32
  2. Um sensor ultrassônico AJ-SR04M
  3. Sensor capacitivo de umidade do solo V1.2
  4. Painel solar Ztroon ZTP-010MI
Além disso, nós não consideramos perdas de fonte nem de conversão de tensão, e usamos um valor simulado de 4 horas de sol pleno por dia, com um cenário de 3 horas para uma análise conservadora.

## Benefícios esperados para a comunidade
Os moradores do local teriam acesso a horta comunitária onde podem realizar seu plantio e compartilhar recursos um com os outros de forma acessivel, já que a irrigação é adequada a cada tipo de planta e sustentável, já que a irrigação inteligente previne o desperdicio de água

# Análise do consumo energético
Estimamos o consumo do sistema com a fórmula E = (P × t) / 1000, considerando funcionamento contínuo de 24 h por dia, a corrente típica informada pelos fabricantes de cada componente e sem perdas de fonte, de conversão de tensão ou do sistema solar. O ESP-WROOM-32, o sensor capacitivo de umidade do solo V1.2 e o sensor ultrassônico AJ-SR04M somam 0,4665 W, o que dá cerca de 11,2 Wh por dia, ou 0,336 kWh por mês. Para a alimentação, dimensionamos um painel solar de 10 W (Ztroon ZTP-010MI), que gera de 30 a 40 Wh por dia com 3 a 4 horas de sol pleno (valor simulado), e 4 baterias 18650 em paralelo, que garantem 2 dias de autonomia sem sol.

Para os cálculos completos, as premissas e o dimensionamento solar, veja o arquivo original: [consumo_energetico.md](consumo_energetico.md).

# Comparação de alternativas
Comparamos duas alternativas para a mesma necessidade energética (0,336 kWh/mês, período de referência de 30 dias): energia solar e rede elétrica. Como hortas comunitárias geralmente não têm ponto de energia, a rede exigiria uma nova ligação, com custo de implantação estimado entre R$ 1.855,86 e R$ 3.055,86 e custo de disponibilidade de cerca de R$ 36,30 por mês. A energia solar tem custo inicial estimado de R$ 250,17 e praticamente nenhum custo de operação, além de funcionar sem tomada, manter o sistema ativo em quedas de energia e estar alinhada ao objetivo de sustentabilidade. Por isso, a solar foi a alternativa escolhida.

Para a tabela completa de critérios e a análise detalhada, veja o arquivo original: [comparacao.md](comparacao.md).

# Diagramação da solução
[A equipe deverá apresentar um diagrama de blocos que represente conceitualmente o
funcionamento da solução proposta. O diagrama deverá relacionar, conforme o projeto:
• Fonte de energia;
• Equipamentos consumidores;
• Sensores ou dados de consumo;
• Lógica de monitoramento ou automação;
• Processamento das informações;
• Indicadores apresentados no dashboard.
O objetivo é demonstrar como os componentes se relacionam, sem exigir a construção de circuitos
eletrônicos ou equipamentos físicos.]
# Indicadores de eficiência e sustentabilidade

# Integração ao Neighborhood Action Dashboard
A contribuição da disciplina deverá ser incorporada ao projeto integrador. O dashboard deverá
permitir visualizar os indicadores energéticos definidos pela equipe, utilizando dados reais,
estimados ou simulados.
A implementação poderá incluir gráficos, tabelas, comparações entre alternativas e informações
sobre os benefícios ambientais e comunitários.
GLOBAL SOLUTION 2026.2 | SERS | CIÊNCIA DA COMPUTAÇÃO 4
Não basta apresentar um dashboard genérico: os indicadores deverão corresponder à análise
energética efetivamente desenvolvida


fontes:  
- https://www.bitmaker.com.br/esp32-wifi-e-bluetooth-esp-wroom-32.html
- https://www.smartkits.com.br/sensor-capacitivo-de-umidade-do-solo?parceiro=9390
- https://www.fornell.com.br/produtos/sensor-ultrassonico-aj-sr04m-a-prova-de-agua/
- https://www.mercadolivre.com.br/painel-solar-10w-ztroon-monocristalino-ztp-010mi-azul-escuro-1000v-2472v/p/MLB74596095?pdp_filters=item_id%3AMLB7674420940&from=gshop&matt_tool=34755848&matt_word=&matt_source=google&matt_campaign_id=22090354298&matt_ad_group_id=173090578756&matt_match_type=&matt_network=g&matt_device=c&matt_creative=727882731306&matt_keyword=&matt_ad_position=&matt_ad_type=pla&matt_merchant_id=735128188&matt_product_id=MLB74596095-product&matt_product_partition_id=2494755919328&matt_target_id=pla-2494755919328&cq_src=google_ads&cq_cmp=22090354298&cq_net=g&cq_plt=gp&cq_med=pla
- https://m.magazineluiza.com.br/busca/modulo+lm2596/
- https://www.magazineluiza.com.br/busca/fonte+12v+2amp/
- https://monitordomercado.com.br/noticias/410146-quanto-custa-trocar-o-padrao-de-entrada-de-energia-para-suportar-os-novos-aparelhos-da-casa/
