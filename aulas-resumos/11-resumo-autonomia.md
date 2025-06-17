# Resumo Aprofundado: Aula 11 - Autonomia e Gestão de Energia

A autonomia é um dos maiores constrangimentos da computação móvel. Como a capacidade das baterias (medida em **mAh**) evolui muito mais lentamente do que a dos CPUs, a responsabilidade de gerir o consumo recai sobre o Sistema Operativo e, crucialmente, sobre as aplicações.

## 1. Os Grandes Consumidores de Energia

O consumo de um dispositivo varia com o seu estado: **Ativo** (ecrã ligado, app a correr), **Idle** (ecrã ligado, sem apps ativas) e **Suspenso** (ecrã desligado). Os componentes que mais consomem são:

1.  **Ecrã:** O maior consumidor em estado ativo. O brilho é um fator direto.
2.  **Rádio de Rede (Wi-Fi/Dados Móveis):** Manter a ligação de rede ativa é extremamente custoso. É o maior consumidor no estado **suspenso**.
3.  **CPU:** Processamento intensivo de dados.
4.  **GPS:** O sensor de localização é um dos maiores "vilões" de consumo.

## 2. Estratégias de Otimização pela Aplicação (O Papel do Developer)

O objetivo é minimizar o tempo em que estes componentes estão ativos, adiando, agrupando ou evitando trabalho.

### A) Otimização do Ecrã
- **Dark Mode em Ecrãs OLED:** Esta é a otimização mais impactante. Em ecrãs OLED/AMOLED, píxeis pretos estão **efetivamente desligados** e não consomem energia. Usar um tema escuro resulta numa poupança muito significativa. Em ecrãs LCD, o efeito é nulo.
- **Brilho Adaptativo:** Deixar o sistema ajustar o brilho com base na luz ambiente.

### B) Otimização da Rede (A Estratégia Mais Importante)
O rádio de rede tem vários estados de energia. "Acordá-lo" para o estado de alta performance tem um custo fixo elevado. A estratégia fundamental é **minimizar o número de vezes que o rádio é ativado**.

- **Batching (Agrupamento):** É o conceito-chave. Em vez de fazer muitos pedidos de rede pequenos e frequentes (ex: enviar cada foto de uma galeria individualmente), deve-se **agrupar as operações de rede** num único pedido, maior e menos frequente (ex: enviar um ZIP com todas as fotos). Isto permite que o rádio volte ao estado de baixo consumo por mais tempo.
- **Caching:** A forma mais eficaz de poupar rede é não a usar. Armazenar dados localmente para evitar fazer pedidos para obter informação que não mudou.
- **Verificar Conectividade:** Antes de tentar uma operação de rede, verificar se existe ligação para evitar falhas e novas tentativas que consomem energia.
- **Push vs. Pull:** Usar notificações Push para informar a app de novos dados é mais eficiente do que a app verificar (Pull/Polling) o servidor a cada X minutos.

### C) Otimização do GPS e Sensores
- **Precisão Adequada:** Pedir sempre o nível de precisão estritamente necessário. O `geolocator` em Flutter permite configurar a `LocationAccuracy`:
    - `LocationAccuracy.high` ou `best`: Usa o GPS, consome muita bateria. Necessário para navegação passo-a-passo.
    - `LocationAccuracy.low` ou `medium`: Usa Wi-Fi e triangulação de antenas (A-GPS), muito mais económico. Suficiente para obter a cidade ou bairro.
- **Não Manter Ativo:** Desligar o stream de localização (`positionStream.cancel()`) assim que a informação não for mais necessária.
- **Escolher o Sensor Certo:** Outros sensores como o acelerómetro têm um consumo de energia muito inferior ao GPS.

### D) Offloading de Processamento
- Mover tarefas computacionalmente intensivas (ex: aplicar filtros a um vídeo, treinar um modelo de ML) para um **servidor na cloud**, que não tem restrições de bateria. A app apenas envia os dados brutos e recebe o resultado final.

---

## 3. Processamento em Background e o Sistema Operativo

Para poupar bateria, os SOs modernos (iOS e Android) são muito restritivos com o que as apps podem fazer em segundo plano. Uma app que sai do foco do utilizador é rapidamente "suspensa" ou terminada.

- **O Problema:** Como executar tarefas importantes mesmo com a app fechada (ex: sincronizar dados periodicamente, fazer backup de fotos)?
- **A Solução (Scheduling):** A app não executa a tarefa diretamente. Em vez disso, **pede ao Sistema Operativo para a executar** no futuro, quando for mais oportuno. O SO (`WorkManager` em Android, `BGAppRefreshTask` em iOS) gere a fila de tarefas de todas as apps e executa-as de forma otimizada para o sistema.
    - **Modo Doze (Android):** Quando o telemóvel está parado, com ecrã desligado e sem carregar, o SO entra num modo de "hibernação" profunda, onde o acesso à rede e CPU é bloqueado, exceto durante curtas "janelas de manutenção".

- **Solução em Flutter (`workmanager`):** O plugin `workmanager` oferece uma API unificada que abstrai a complexidade de ambos os sistemas.

#### Como funciona o `workmanager`:
1.  **Definir um Callback:** Criar uma função global/estática que contém o código a correr em background.
2.  **Inicializar e Registar:** No `main()` da app, inicializar o `Workmanager` e registar o callback.
3.  **Agendar a Tarefa:** Registar a tarefa, especificando uma frequência **mínima** e **restrições** (ex: "só executar com Wi-Fi" ou "só quando a carregar").

```dart
// Agendar uma tarefa para correr APROXIMADAMENTE a cada hora.
Workmanager().registerPeriodicTask(
  "idUnicoDaTarefa", 
  "nomeDaTarefa", // Nome simples para debugging
  frequency: Duration(hours: 1),
  constraints: Constraints(
    networkType: NetworkType.unmetered, // Só em Wi-Fi
    requiresCharging: true,
  ),
);
```
- **Importante:** A execução **não é garantida** no tempo exato. O SO tem a palavra final e "fará o seu melhor" para executar a tarefa por volta da frequência pedida, otimizando sempre pelo bem da bateria do dispositivo. 