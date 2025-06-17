# Estrutura e Regras do Exame

- **Formato:** Perguntas de resposta aberta.
- **Consulta:** É permitida uma **única folha A4, manuscrita** (frente e verso).
- **Restrições:** A folha de consulta **não pode conter código Dart nem excertos JSON**, apenas texto e diagramas.

### Pontuação
- **Parte 1:** Formato JSON (2 valores)
- **Parte 2:** Programação com Callbacks (2 valores)
- **Parte 3:** Conceitos e Programação Flutter (4 valores)
- **Parte 4:** Conceitos de Computação Móvel (12 valores)

---

## Parte 1: Transformação de XML para JSON

O objetivo é converter uma estrutura de dados de XML para um formato JSON equivalente. A lógica de mapeamento segue regras consistentes.

- **Regra 1: Tags Aninhadas → Objetos Aninhados**
  - Uma tag XML que contém outras tags dentro dela (ex: `<response>...</body></response>`) torna-se um objeto JSON (`{}`). A tag externa vira a chave do objeto.

- **Regra 2: Tags com Conteúdo de Texto → Pares Chave-Valor**
  - Uma tag que contém apenas texto (ex: `<code>Success</code>`) torna-se um par chave-valor (`"code": "Success"`). A tag é a chave, o conteúdo é o valor.

- **Regra 3: Atributos de Tag → Pares Chave-Valor**
  - Atributos dentro de uma tag XML (ex: `<movie name="Gladiador" year="2000">`) tornam-se pares chave-valor dentro do objeto JSON correspondente (`"name": "Gladiador", "year": 2000`).

- **Regra 4: Múltiplas Tags com o Mesmo Nome → Lista de Objetos**
  - Quando uma tag pai contém várias tags filhas com o mesmo nome (ex: dois `<actor>` dentro de `<movie>`), estas são agrupadas numa lista (array `[]`) de objetos JSON. O nome da tag repetida torna-se o nome da lista (ex: `"actors": [...]`).

- **Tipagem de Dados:** Valores numéricos ou booleanos no XML devem ser convertidos para os tipos correspondentes em JSON, não strings (ex: `year="2000"` vira `"year": 2000`).

---

## Parte 2: Lógica de Callbacks

A chave é seguir o fluxo de execução e perceber que o estado é mantido num objeto central, enquanto outros objetos apenas invocam as funções (callbacks) que alteram esse estado.

- **Fluxo Conceptual:**
  1.  **Objeto de Estado (`Callbacks`):** Existe um objeto central que contém as variáveis de estado (ex: `_x`, `_y`) e os métodos que as manipulam (ex: `onX`, `onY`).
  2.  **Objetos "Gatilho" (`Contadores`):** Outros objetos são inicializados recebendo referências para os métodos do objeto de estado. Eles não sabem o que os métodos fazem, apenas que devem executá-los.
  3.  **Invocação Indireta:** Quando se altera uma propriedade num objeto "gatilho" (ex: `contadores1.a = 3`), o seu `setter` interno invoca a função que lhe foi passada no construtor.
  4.  **Mutação do Estado Central:** A função invocada (ex: `callbacks.onX(3)`) executa e altera o estado no objeto original (`_x` passa a ser `3`).
  5.  **Sequência é Crucial:** O resultado de uma operação depende do estado deixado pela operação anterior. Se `contadores1.b = 4` invoca `onY` que usa `_x`, o valor de `_x` será o que foi modificado pelo passo anterior.
  6.  **Lambdas/Funções Anónimas:** Um "gatilho" pode ser configurado com uma função definida no local (lambda). Essa função é independente do objeto de estado e executa a sua própria lógica (ex: `print(valor)`).

---

## Parte 3: Conceitos Fundamentais de Flutter

### A) Respostas Curtas

- **StatelessWidget vs. StatefulWidget:**
  - **Stateless:** Para UI que **não muda** após ser desenhada (ex: ícones, texto fixo). É imutável, leve e apenas tem um método `build`.
  - **Stateful:** Para UI **dinâmica** que precisa de ser redesenhada quando os dados internos mudam. É composto por duas classes: o Widget (imutável) e o `State` (mutável e persistente). A mudança é despoletada por uma chamada a `setState()`, que agenda a reconstrução do widget.

- **Injeção de Dependências (DI):**
  - **O Quê:** É uma técnica que consiste em **fornecer as dependências** a uma classe (os objetos de que ela precisa) a partir do exterior, em vez de a classe as criar internamente.
  - **Porquê:** Para **desacoplar** o código. A classe depende de um "contrato" (classe abstrata) e não de uma implementação concreta. O principal benefício é a **testabilidade**, pois permite substituir dependências reais por `mocks` (objetos falsos) nos testes.

- **Pedidos Assíncronos (`async`/`await`):**
  - **O Quê:** Mecanismo para executar operações demoradas (rede, ficheiros) **sem bloquear a UI**.
  - **Como:** Uma função marcada como `async` pode usar a palavra `await` para pausar a sua própria execução até que um `Future` (a promessa de um resultado futuro) seja concluído. Enquanto a função está em `await`, o *event loop* de Dart (UI Thread) fica livre para continuar a responder a interações do utilizador.

- **Testes de Widget vs. Testes de Integração:**
  - **Teste de Widget:** Testa **um único widget** de forma isolada do resto da app. Verifica a sua UI, estado e interações. É **rápido** e **não precisa de emulador**.
  - **Teste de Integração:** Testa um **fluxo completo da app** ou a app inteira, simulando um utilizador real. Valida a integração entre múltiplos widgets, ecrãs e serviços. É **lento** e **precisa de um emulador/dispositivo real**.

### B) Lógica de Programação (Widget de Contador)

1.  **Tipo de Widget (`StatefulWidget`):** O widget precisa de ser `StatefulWidget` porque o seu conteúdo (o número do contador) muda com a interação do utilizador.
2.  **Declaração de Variável (`title;`):** Sintaxe padrão de Dart para completar a declaração de uma variável de instância numa classe.
3.  **Função de Mutação (`setState`):** É a função essencial num objeto `State`. Qualquer alteração a uma variável que deva ser refletida na UI tem de ser feita dentro do callback de `setState`. Isto notifica o Flutter para chamar o método `build` novamente.
4.  **Mostrar o Valor (`'$_counter'`):** Interpolação de strings em Dart. O `$` permite inserir o valor de uma variável diretamente numa string.
5.  **Referência de Função (`_incrementCounter`):** Propriedades como `onPressed` esperam uma **referência** a uma função, não a sua invocação. Passa-se o nome da função sem parênteses.

---

## Parte 4: Mega-Resumo de Computação Móvel

### Arquiteturas de Desenvolvimento

- **Nativa Pura:** **Máximo desempenho e acesso a APIs**. Custo mais elevado devido a bases de código separadas (Swift/Kotlin).
- **Híbrida-Nativa (Flutter):** **Melhor compromisso**. Base de código única (Dart). Compila para código nativo ARM, atingindo **excelente desempenho**. Usa o seu próprio motor de renderização (Skia) para desenhar a UI, garantindo consistência visual total.
- **Híbrida-Nativa (React Native):** Base de código única (JavaScript). Usa uma **ponte (JS Bridge)** para comunicar com os componentes de UI nativos do SO. A ponte pode ser um **gargalo de desempenho**. Permite atualizações "over-the-air" com Code Push.
- **Híbrida-Web (Cordova/Ionic):** Essencialmente um **site dentro de uma `WebView`**. Desempenho mais fraco, acesso limitado a APIs nativas. Barato, mas a experiência de utilizador é inferior.
- **PWA (Progressive Web App):** Um site moderno que se "comporta" como uma app (manifest, **service worker para offline**). Não passa pelas app stores, sendo "instalado" a partir do browser. Adoção limitada por falta de suporte total no iOS.

### Modelos de Navegação e Estado
- **Passagem de Dados:** É comum passar dados simples (como IDs) para o ecrã de detalhe. Para cenários mais complexos, como saber a *origem* da navegação, pode-se passar um argumento extra no construtor do novo ecrã ou através do sistema de rotas (ex: `GoRouter`).
- **Estado Persistente:** Para guardar preferências do utilizador (ex: "não mostrar novamente") que devem sobreviver entre sessões da app, usa-se uma solução de armazenamento local como `shared_preferences`. Esta informação é depois lida pelo repositório ou ViewModel para alterar a lógica de apresentação dos dados.
- **Layouts Complexos:** A criação de UIs específicas (como dashboards) requer uma combinação de widgets de layout (`Row`, `Column`, `Stack`), widgets de espaçamento (`Padding`, `SizedBox`) e `Expanded` para gerir o espaço. A estilização individual (cores, fontes) é aplicada diretamente nos widgets.

### Usabilidade e Interação

- **Thumb Zone (Zona do Polegar):** As ações primárias e a navegação devem estar na **parte inferior do ecrã**, facilmente alcançáveis com uma mão.
- **Problema do "Dedo Gordo":** Os alvos de toque (botões, ícones) devem ter no mínimo **48dp** (cerca de 9mm) de área clicável para serem fáceis de usar. A área clicável pode ser maior que o ícone visível.
- **Ponto de Atenção:** A UI deve reagir a interações de forma clara, como com uma `SnackBar` ou `Toast`, para dar feedback de ações (ex: clique num marcador de mapa) sem interromper o fluxo principal.

### Conectividade e Dados

- **Padrão Repositório:** **Essencial.** Cria uma camada de abstração entre a UI e as fontes de dados. A UI pede dados ao repositório, que decide se os vai buscar a uma **API remota** ou a uma **cache local**. Desacopla o código e é a chave para a testabilidade e para implementar lógica offline.
- **Offline-First:** A app deve ser funcional **sem internet**. A UI carrega dados da cache local primeiro e só depois (ou em background) tenta sincronizar com a rede.
- **Ponto de Atenção (Lógica de Negócio):** O repositório é o local ideal para centralizar a lógica de negócio. Isto inclui **fundir dados de múltiplas fontes** (ex: combinar uma lista de uma API com dados de lotação de outra API) e **filtrar** a lista final com base em regras (ex: remover itens que não cumprem uma condição) antes de a entregar à UI.

### Autonomia (Gestão de Bateria)

- **Otimizar a Rede:** O rádio de rede é um grande consumidor. A melhor estratégia é **agrupar (`batching`) vários pedidos pequenos num único pedido maior**. Isto permite que o rádio "durma" por mais tempo.
- **Otimizar GPS:** Pedir sempre a **menor precisão (`LocationAccuracy`)** aceitável para a tarefa. Desligar o sensor (`stream.cancel()`) assim que a localização for obtida.
- **Processamento em Background:** É **fortemente restringido pelo SO**. Para tarefas periódicas, usar um agendador (`workmanager`). A app **pede ao SO** para executar a tarefa no futuro, e o SO decide o melhor momento para o fazer (e.g., durante o **Modo Doze**).

### Sensores e Contexto

- **Geolocalização:** Requer **permissão explícita** do utilizador. O fluxo correto é sempre: **Verificar Permissão -> Pedir Permissão -> Gerir Negação Permanente**. A app nunca deve assumir que tem permissão.
- **Tipos de Sensores:** Físicos (Acelerómetro), Lógicos/Virtuais (Detetor de passos, que combina dados de sensores físicos), e Biométricos (Ritmo cardíaco).

### Serviços Externos e APIs

- **REST:** Um estilo de arquitetura para APIs que usa verbos HTTP (`GET` para ler, `POST` para escrever) em **Endpoints** (URLs). Comunica tipicamente com **JSON**.
- **Tokens:**
    - **API Token:** Autentica a **aplicação** cliente junto da API.
    - **Access Token (Bearer):** Autentica o **utilizador** final, provando que ele fez login e tem permissão para aceder aos seus dados. É enviado no `Header` de cada pedido.

### Modelos de Negócio

- **Custos:** Publicar na **App Store custa $99/ano**; na **Google Play custa $25 (pagamento único)**. Ambas ficam com uma comissão de **15-30%** sobre as vendas.
- **Modelos:**
    - **Anúncios:** Requer muitos utilizadores e/ou muito tempo de uso.
    - **Paga:** Difícil de vender sem uma reputação forte.
    - **Freemium:** Grátis para usar, pagar por extras. O mais comum.
    - **Subscrição:** Exige **valor contínuo** para justificar o pagamento recorrente. Gera receita previsível.

---

## Anexo: Cábula Rápida Kotlin -> Dart

| Conceito | Kotlin | Dart | Notas |
|:---|:---|:---|:---|
| **Variáveis Imutáveis** | `val x = 10` | `final int x = 10;` | `const` em Dart é para valores conhecidos em tempo de compilação. |
| **Nulabilidade** | `String? nome` | `String? nome;` | Declaração similar. |
| **Safe Call** | `nome?.length` | `nome?.length;` | Idêntico. |
| **Elvis Operator** | `nome ?: "Default"` | `nome ?? "Default"` | `?:` em Kotlin é `??` em Dart. |
| **Função (Lambda)** | `(Int a, Int b) -> a + b` | `(int a, int b) => a + b;` | Usa `=>` para funções de uma linha. |
| **Callbacks em Setters** | `set(v) { field=v; f(v) }` | `set a(v) { _a=v; f(v); }` | A sintaxe de `setters` é diferente. |
| **Listas** | `listOf(1, 2)`