# Guia de Estudo para o Exame de Computação Móvel

**Foco:** Conceitos, justificações e padrões. Otimizado para folha A4 manuscrita (frente e verso).
**Regra de Ouro:** Sem código Dart ou JSON. Apenas texto, conceitos e diagramas simples.

---

## Parte 1: Formato JSON (2 valores)

**Objetivo:** Compreender a lógica de conversão de estruturas de dados (como XML) para JSON.

**Regras de Mapeamento (XML para JSON):**

*   **Tags Aninhadas:** Uma tag dentro de outra em XML corresponde a um objeto JSON (`{ }`) como valor de uma chave no objeto pai. A tag raiz do XML torna-se o objeto raiz do JSON.
*   **Conteúdo da Tag:** O texto dentro de uma tag (ex: `<code>Success</code>`) torna-se um valor de uma propriedade JSON (ex: `"code": "Success"`).
*   **Atributos de Tags:** Atributos de uma tag XML (ex: `<movie name="Gladiador">`) tornam-se propriedades `chave: valor` dentro do objeto JSON correspondente (ex: `"name": "Gladiador"`).
*   **Tags Irmãs com o Mesmo Nome:** Quando várias tags com o mesmo nome aparecem sob o mesmo pai (ex: duas tags `<actor>`), elas são agrupadas numa **lista (array `[ ]`)** em JSON. O nome da chave JSON será o nome da tag no plural (ex: `"actors": [ ... ]`).

---

## Parte 2: Programação com Callbacks (2 valores)

**Objetivo:** Seguir o fluxo de execução de código que passa funções como parâmetros (callbacks) para entender como o estado de um objeto muda ao longo do tempo.

**Lógica do Fluxo de Execução:**

Imagine um objeto `CentralState` que guarda dois números, `x` e `y`. O seu estado inicial é `x = 0` e `y = 0`.
Temos também dois objetos `Controller`, C1 e C2. Cada um pode modificar `x` e `y` no `CentralState` através de callbacks.

1.  **C1 é configurado para:**
    *   Ao executar a sua **ação A**, chamar uma função que *soma* ao `x` do `CentralState`.
    *   Ao executar a sua **ação B**, chamar uma função que atualiza o `y` do `CentralState` com base no valor *atual* de `x`.

2.  **C2 é configurado para:**
    *   Ao executar a sua **ação A**, também chamar a função que *soma* ao `x` do `CentralState`.
    *   Ao executar a sua **ação B**, simplesmente imprimir um valor na consola, sem afetar o `CentralState`.

**Execução passo a passo:**
1.  `C1.actionA(3)` é chamado -> `CentralState.x` torna-se `0 + 3 = 3`.
2.  `C1.actionB(4)` é chamado -> `CentralState.y` torna-se `(valor atual de x) + 4`, ou seja, `3 + 4 = 7`.
3.  `C2.actionA(10)` é chamado -> `CentralState.x` torna-se `3 + 10 = 13`.
4.  `C2.actionB(5)` é chamado -> Imprime `5` na consola. O `CentralState` não é alterado.

**Estado Final:** Após a execução, o objeto `CentralState` contém `x = 13` e `y = 7`.

---

## Parte 3: Conceitos Fundamentais de Flutter (4 valores)

*   **Stateless vs. StatefulWidget:**
    *   **StatelessWidget:** Usado para partes da UI que são **estáticas e imutáveis**. Não dependem de interação do utilizador para mudar a sua aparência (ex: um ícone, um título fixo). São eficientes e têm apenas um método `build`.
    *   **StatefulWidget:** Usado para UI **dinâmica** que muda com base em interação ou dados. A sua lógica é dividida em duas classes: o Widget (imutável) e o seu State (mutável). A função `setState()` é chamada dentro da classe State para notificar o Flutter que o estado mudou e que a UI precisa ser reconstruída.

*   **Injeção de Dependências (DI):**
    *   **O quê?** É um padrão que consiste em **fornecer as dependências** (objetos que uma classe precisa para funcionar, como um serviço de API) de fora, geralmente através do construtor.
    *   **Porquê?** Para **desacoplar** o código. A classe não cria as suas próprias dependências, o que a torna mais flexível e, crucialmente, **fácil de testar**. Em testes, podemos "injetar" versões falsas (`mocks`) das dependências para isolar o comportamento que queremos testar.

*   **Programação Assíncrona (`async`/`await`):**
    *   **O quê?** Uma forma de lidar com operações demoradas (ex: pedidos de rede, acesso a ficheiros) **sem bloquear a interface do utilizador**.
    *   **Como funciona?** A palavra-chave `async` marca uma função como assíncrona. Dentro dela, `await` pausa a execução *dessa função específica* até que a operação (um `Future`) termine, mas **liberta o thread principal da UI**, mantendo a app responsiva.

*   **Testes de Widget vs. Testes de Integração:**
    *   **Teste de Widget:** Foca-se em **testar um único widget isoladamente**. Verifica a sua UI, interações e se responde corretamente a mudanças de estado. São rápidos e não precisam de um emulador.
    *   **Teste de Integração:** Testa a **app completa ou um fluxo de utilizador inteiro** (end-to-end). Valida a integração entre vários widgets, serviços, e a performance geral. São mais lentos e requerem um emulador ou dispositivo real para correr.

---

## Parte 4: Conceitos Essenciais de Computação Móvel (12 valores)

### Arquiteturas de Desenvolvimento: Prós e Contras

*   **Nativa Pura (Kotlin/Swift):**
    *   **Prós:** Máximo desempenho, acesso total e imediato a todas as APIs nativas do SO.
    *   **Contras:** Custo de desenvolvimento muito elevado (duas bases de código, duas equipas), lento a desenvolver.
*   **Híbrida-Nativa (Flutter):**
    *   **Prós:** Base de código única (Dart), excelente desempenho (compilado para código nativo), UI consistente entre plataformas. Acesso a APIs nativas via plugins (bridges).
    *   **Contras:** A app é ligeiramente maior. Dependência de plugins de terceiros. **É o melhor compromisso geral (custo/performance).**
*   **Híbrida-Web (Ionic/Cordova):**
    *   **Prós:** Base de código web (HTML, CSS, JS), mais barato e rápido para projetos simples.
    *   **Contras:** A app corre numa `WebView`, o que resulta num desempenho inferior e numa experiência de utilizador (UX) menos fluida. Acesso limitado a funcionalidades nativas.
*   **PWA (Progressive Web App):**
    *   **Prós:** Não requer instalação via store. Usa tecnologias web e pode funcionar offline (com service workers).
    *   **Contras:** Funcionalidades muito mais limitadas no iOS. Não é uma "app real", mas sim um site melhorado.

### Usabilidade e Interação (UX)

*   **Thumb Zone (Zona do Polegar):** As ações primárias e a navegação devem estar na **parte inferior do ecrã**, onde são facilmente alcançáveis com o polegar numa utilização com uma só mão.
*   **Fat Finger Problem (Problema do Dedo Gordo):** Os alvos de toque (botões, links, ícones) devem ter uma área de toque mínima de **48x48 dp** (aproximadamente 9mm), mesmo que o ícone visual seja mais pequeno. Isto reduz erros de interação.

### Dados e Conectividade

*   **Padrão Repositório (Repository Pattern):** **CRUCIAL.** É uma camada de abstração que fica entre a lógica de negócio/UI e as fontes de dados.
    *   **Como funciona:** A UI pede dados ao Repositório. O Repositório decide de onde os obtém: de uma **API remota** (se houver rede) ou de uma **cache local** (Base de Dados, SharedPreferences).
    *   **Vantagens:** Desacopla a UI da origem dos dados, facilita a implementação de **lógica offline-first**, e simplifica os testes (podemos substituir o repositório por um `mock`).
*   **Offline-First:** A arquitetura onde a app é desenhada para funcionar primariamente com dados locais (cache). A UI carrega instantaneamente a partir da cache e a sincronização com a rede é feita em segundo plano ou quando estritamente necessário.

### Autonomia (Gestão de Bateria)

*   **Otimização de Rede:** O rádio do telemóvel é um dos maiores consumidores de bateria. A melhor prática é **agrupar (`batching`) vários pedidos de rede pequenos num único pedido maior**. Isto permite que o rádio seja ativado menos vezes e "durma" por mais tempo.
*   **Otimização de GPS:** A geolocalização é muito dispendiosa. Deve-se **pedir sempre a menor precisão (`LocationAccuracy`)** que seja suficiente para a funcionalidade e **parar de ouvir a localização (`stream.cancel()`)** assim que a informação necessária for obtida.
*   **Tarefas em Background:** São **fortemente restringidas** pelos SOs modernos (iOS, Android > 6.0) para poupar bateria. Para tarefas não urgentes e deferíveis (ex: sincronizar dados a cada poucas horas), deve-se usar ferramentas como o `workmanager`. Ele agenda a tarefa e o SO decide o melhor momento para a executar (ex: quando o telemóvel está a carregar e com Wi-Fi), respeitando o **Modo Doze**.

### Sensores, APIs e Segurança

*   **Permissões:** O acesso a sensores (GPS, câmara, microfone) e dados do utilizador requer **permissão explícita**, que deve ser pedida e gerida em tempo de execução.
*   **API REST:** Um estilo de arquitetura para serviços web. Usa os verbos HTTP (`GET`, `POST`, `PUT`, `DELETE`) para manipular recursos identificados por URLs (endpoints). É o padrão de facto para comunicação cliente-servidor.
*   **Tokens de Acesso (JWT):** Para proteger endpoints, a app primeiro faz login para obter um `Access Token`. Este token é então enviado no `Header` de cada pedido subsequente à API para provar que o utilizador está autenticado e autorizado. 