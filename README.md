Circuito 2 LEDs dos Crias Mecatrônicos
---------------

Descrição Geral
---------------
Este projeto consiste em uma placa de circuito impresso (PCB) simples que acende dois LEDs (um vermelho e um verde) a partir de uma fonte de alimentação de 5V. O circuito utiliza dois resistores de 100 ohms para limitar a corrente dos LEDs e um plano de terra na camada inferior (B.Cu) para simplificar o roteamento e melhorar a integridade do sinal.

O projeto foi desenvolvido no KiCad 10.0 como um exercício de aprendizado do fluxo completo de design de PCBs: criação do esquemático, associação de footprints, layout da placa, verificação de regras elétricas e de design, geração de arquivos Gerber e visualização 3D.

Esquemático
-----------
O esquemático (arquivo .kicad_sch) contém os seguintes componentes:

- J1: Conector de dois pinos (Conn_01x02_Male) para a entrada de alimentação 5V. O pino 1 é conectado à rede +5V e o pino 2 ao GND.
- R1, R2: Resistores de 100 ohms, 1/4W, com encapsulamento axial (THT). Cada resistor tem uma extremidade ligada ao +5V e a outra ao ânodo do LED correspondente.
- D1: LED vermelho difuso de 5mm. Ânodo conectado a R1, cátodo ligado ao GND.
- D2: LED verde difuso de 5mm. Ânodo conectado a R2, cátodo ligado ao GND.

Símbolos globais de alimentação (+5V e GND) são utilizados para distribuir a energia de forma organizada. O terra é comum a todos os componentes, formando uma única rede GND.

Cálculo da corrente nos LEDs:
Considerando uma tensão direta típica de 2,0V para o LED vermelho e 2,2V para o verde, a corrente em cada LED é:
  LED vermelho: (5V - 2,0V) / 100Ω = 30mA
  LED verde:   (5V - 2,2V) / 100Ω = 28mA
Ambos os valores estão dentro da faixa segura para LEDs de 5mm (geralmente 20-30mA), garantindo luminosidade adequada sem risco de danos.

A verificação de regras elétricas (ERC) retornou zero erros e zero avisos, indicando que todas as conexões estão corretas.

Lista de Materiais (BOM)
-------------------------
- 1x LED vermelho 5mm (D1)
- 1x LED verde 5mm (D2)
- 2x Resistor 100Ω, 1/4W, THT (R1, R2)
- 1x Barra de pinos macho 1x2, passo 2,54mm (J1) — ou borne de parafusos compatível
- 1x Placa de circuito impresso (obtida a partir dos arquivos Gerber fornecidos)
- Fonte de alimentação 5V (ex.: carregador USB, bateria com regulador)

Design da PCB
--------------
O layout da placa (arquivo .kicad_pcb) foi desenvolvido no Pcbnew. A placa tem formato retangular de aproximadamente 40mm x 30mm, definido na camada Edge.Cuts.

Características principais do layout:

1. Plano de terra (zona de cobre) na camada inferior (B.Cu):
   - Foi criada uma zona de cobre preenchida em B.Cu, associada à rede GND.
   - Essa zona conecta automaticamente todos os pads pertencentes ao GND (catodo dos LEDs e pino 2 do conector), eliminando a necessidade de trilhas de terra adicionais.
   - A zona foi configurada com alívios térmicos (espaçamento de 0,5mm) para facilitar a soldagem.
   - Isolamento mínimo de 0,5mm entre a zona e outros elementos.

2. Roteamento:
   - A única trilha desenhada manualmente foi a de +5V, na camada superior (F.Cu), ligando o pino 1 do conector aos resistores R1 e R2.
   - Largura de trilha: 0,5mm, suficiente para as correntes envolvidas.

3. Posicionamento dos componentes:
   - Conector J1 na borda esquerda da placa.
   - Resistores no centro, ligando o +5V aos ânodos dos LEDs.
   - LEDs na borda direita, com os catodos voltados para baixo (conectados internamente ao plano de terra).
   - Serigrafia (F.Silkscreen) indica a polaridade do conector e identifica cada LED.

4. Verificações de design (DRC):
   - Antes de executar o DRC, a zona de cobre foi preenchida (tecla B).
   - O DRC retornou 0 violações, confirmando que o layout atende às regras de fabricação.

Alguns testes foram ignorados pelo DRC (ex.: "footprint não bate com o filtro da biblioteca"), o que é comum e não afeta o funcionamento.

Visualização 3D
----------------
O visualizador 3D do KiCad foi utilizado para inspecionar a placa virtualmente. Observações:
- Por padrão, ambos os LEDs aparecem na cor vermelha, pois o modelo 3D genérico (LED_D5.0mm) não distingue cores. Isso é apenas cosmético; os LEDs reais terão as cores conforme adquiridos.
- Para alterar a cor no modelo 3D, seria necessário substituir o arquivo STEP de um dos LEDs por uma versão colorida (ex.: LED_D5.0mm_Green.step), se disponível na biblioteca.
- O plano de terra em B.Cu é visível ao girar a placa e habilitar a camada B.Cu nas opções de exibição do visualizador 3D.

Arquivos de Fabricação (Gerber e Excellon)
------------------------------------------
Os arquivos para fabricação da PCB estão na pasta "Arquivo_Gerber/" e incluem:

Camadas Gerber (formato RS-274X, X2 estendido):
- Circuito_2_Leds_dos_crias_mecatronicos-F_Cu.gbr         -> Cobre superior
- Circuito_2_Leds_dos_crias_mecatronicos-B_Cu.gbr         -> Cobre inferior (plano de terra)
- Circuito_2_Leds_dos_crias_mecatronicos-F_Mask.gbr       -> Máscara de solda superior
- Circuito_2_Leds_dos_crias_mecatronicos-B_Mask.gbr       -> Máscara de solda inferior
- Circuito_2_Leds_dos_crias_mecatronicos-F_Silkscreen.gbr -> Serigrafia superior
- Circuito_2_Leds_dos_crias_mecatronicos-B_Silkscreen.gbr -> Serigrafia inferior (opcional)
- Circuito_2_Leds_dos_crias_mecatronicos-Edge_Cuts.gbr    -> Contorno da placa

Arquivo de furação (Excellon):
- Circuito_2_Leds_dos_crias_mecatronicos.drl              -> Coordenadas dos furos, unidades em mm, formato decimal

Para encomendar a placa, compacte todos os arquivos da pasta "Arquivo_Gerber/" em um arquivo .zip e envie ao fabricante de sua preferência (JLCPCB, PCBWay, etc.).

Montagem e Teste
-----------------
1. Solde os resistores R1 e R2.
2. Solde os LEDs D1 (vermelho) e D2 (verde), respeitando a polaridade: o terminal mais longo (ânodo) deve ser conectado ao resistor; o terminal mais curto (cátodo) ao plano de terra.
3. Solde o conector J1.
4. Conecte uma fonte de 5V, observando a polaridade indicada na serigrafia.
5. Ambos os LEDs devem acender imediatamente.

Se um LED não acender, verifique:
- Se a solda está firme e sem curto-circuito.
- Se o LED não foi invertido (polaridade trocada).
- Se a fonte está fornecendo 5V estáveis.

Possíveis Melhorias Futuras
----------------------------
- Adicionar um botão liga/desliga em série com a alimentação.
- Substituir o conector de pinos por um conector USB (ex.: micro-USB ou USB-C).
- Incluir um resistor de pull-down ou proteção contra inversão de polaridade.
- Criar uma versão com controle independente de cada LED via microcontrolador (ex.: ESP32, Arduino).

Estrutura do Repositório (Sugestão)
-------------------------------------
Circuito_2_Leds_dos_crias_mecatronicos/
├── README.txt (este arquivo)
├── Circuito_2_Leds_dos_crias_mecatronicos.kicad_pro
├── Circuito_2_Leds_dos_crias_mecatronicos.kicad_sch
├── Circuito_2_Leds_dos_crias_mecatronicos.kicad_pcb
├── .gitignore
├── Arquivo_Gerber/
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-F_Cu.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-B_Cu.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-F_Mask.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-B_Mask.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-F_Silkscreen.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-B_Silkscreen.gbr
│   ├── Circuito_2_Leds_dos_crias_mecatronicos-Edge_Cuts.gbr
│   └── Circuito_2_Leds_dos_crias_mecatronicos.drl
└── doc/ (opcional)
    ├── esquematico.pdf
    ├── pcb_frente.pdf
    ├── pcb_costas.pdf
    └── pcb_3d.png

Contato e Suporte
-------------------
Este projeto faz parte do aprendizado em engenharia mecatrônica e robótica. Se você tiver dúvidas, sugestões ou quiser trocar ideias sobre design de PCBs, fique à vontade para abrir uma issue no repositório do GitHub (link do repositório) ou entrar em contato diretamente.

Se você está usando este repositório como base para seus próprios estudos, recomendo os seguintes recursos:
- Documentação oficial do KiCad: https://docs.kicad.org
- Fórum da comunidade KiCad: https://forum.kicad.info
- Canais no YouTube sobre KiCad e eletrônica.

Agradecimento especial ao meu "chat dedicado de IA", que me auxiliou na elaboração desta documentação e na solução de dúvidas durante o desenvolvimento do projeto.
