# Quiz #8 - Conectividade - Solução

### Pergunta 1

As redes sem fios assentam sobre duas tecnologias de transmissão de dados. A mais utilizada é, de longe **RF** (sigla em maiúsculas). A outra **IR** é menos utilizada pois está limitada a comunicações de:
- [x] Curta distância
- [ ] Média distância
- [ ] Longa distância

De facto, o alcance da tecnologia é um factor importante de decisão. Algumas tecnologias são de curta distância, isto é, podem transmitir até:
- [ ] alguns cms
- [ ] 1 metro
- [x] alguns metros

Outras são de média distância ([**Wi-Fi**]):
- [ ] 1-10 metros
- [x] 30-300 metros
- [ ] 200-500 metros

...e finalmente as de **longa** distância podem atingir muitos kms.

Mas não é o único factor. Por exemplo, a maior vantagem do IR relativamente ao RF é:
- [ ] ter maior largura de banda
- [ ] não ser afectada por obstáculos
- [ ] ter uma transmissão mais rápida
- [ ] funcionar dentro de casa
- [x] ter comunicação direccional

Outro exemplo é o do NFC que é melhor do que o RFID por:
- [ ] ter maior largura de banda
- [ ] não ser afectado por obstáculos
- [x] ser mais seguro
- [ ] ter maior alcance

A principal vantagem do Bluetooth relativamente às outras tecnologias de curta-distância é:
- [ ] ser direccional
- [x] funcionar em todos os smartphones
- [ ] o baixo custo
- [ ] o tempo de inicialização

É impossível falar de conectividade sem falar da problemática de se ficar offline. Para isso, as aplicações têm que **interrogar** o estado da rede quando o utilizador quer fazer uma acção que exija dados do servidor e **observar** o estado da rede para saber quando enviar dados pendentes ao servidor.

A primeira opção é maioritariamente associada a:
- [x] leituras
- [ ] escritas

...enquanto a segunda a:
- [ ] leituras
- [x] escritas

...de informação do/no servidor.

Para garantir que a aplicação trabalha minimamente em modo offline, é normalmente necessário usar:
- [ ] replicação
- [x] cache
- [ ] repositório

...que pode operar de forma **permanente** ou temporária. O segundo caso é também denominado de **cache**.

Quando alteramos a réplica num dispositivo, essa informação tem que ser propagada para os restantes dispositivos através de dois modos: o modelo **pull** implica interrogar periodicamente o servidor enquanto no modelo **push** é o servidor a transmitir essa informação diretamente para cada dispositivo. A primeira opção é a que:
- [x] funciona melhor para dispositivos offline
- [ ] atualiza mais rapidamente a informação

Por exemplo, o Git usa o modelo **pull**. 