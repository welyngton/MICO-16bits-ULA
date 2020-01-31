# Projeto de ULA de 16bits em VERILOG

## Criado por:
Rafael Rotelok
Welyngton Jose Vinicius Dal Pra

### Operações e funcionalidades

### Extensão sinal
Módulo que estende a entrada do dip Imm5 de 5bits para uma saída de 16 bits Imm16. A extensão é realizada copiando-se o bit número 4 (sinal) aos bits da extensão para manter o sinal do número.

### Registradores
Esse módulo possui 12 registradores interiormente, um Demux que selecionado pelo sinal de LoadReg, grava no registrador destino (RegDst) a entrada R. As entradas RegA e RegB selecionam em dois multiplexadores as saídas DataOutBusA e DataOutBusB entre os registradores - essas saídas serão operandas na ULA.

### ULA
Bloco que contém os módulos das 6 funções (ADD, SUB, OR, AND, NOT, IDENTIDADE) possui 6 wire merges que aglutinam os fios de status (zero, negativo, positivo, overflow) de cada módulo, em fios de 4 bits para a saída S que entra no módulo regstat, também possui uma saída R saída dos módulos. A saída R e S são escolhidas pelo dip switch ctrlULA que define as operações.

### REGSTAT
Módulo que guarda um registrador que armazena o status do número de saída (zero, negativo, positivo, overflow).

### ADD
Esse módulo foi feito com base na concepção de 4 somas de 4 bits para gerar um resultado de 16 bits e dois níveis de geração de carry antecipado (CLA) os 'carrys gerados' são enviados antecipadamente ao módulo seguinte de soma em 4 bits evitando-se a espera pela geração de carry que atrasa muito circuitos com grande quantidade de bits.

### SUB
O módulo é praticamente igual ao ADD, as diferenças são: a entrada B é negada e o primeiro carry é definido como 1. Assim pode-se manter a idéia de subtração com complemento de dois - em que uma entrada é somada a outra na forma complementada (negando esta e somando-se 1 a ela).

### OR
As entradas A e B passam por uma porta OR também é gerado o status.

### AND
Nesse módulo as entradas A e B passam por uma porta AND e é realizada a operação.

### NOT
Esse módulo só pussui uma porta inversora para negar os 16 bits de entrada e o status de saída.

### IDENTIDADE
Esse módulo passa diretamente a entrada A para a saída, utiliza dois wire no começo porque o tkgate não permite ligar uma entrada a uma saída diretamente. Também gera os bits de status.
