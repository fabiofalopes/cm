# Guia de Estudo A4 para Exame de Computação Móvel (Cábula)

Este guia está otimizado para ser transcrito à mão numa única folha A4.

---

### **Parte 1: Guia Mental de Conversão XML -> JSON**

O objetivo é converter uma estrutura XML para JSON seguindo um processo lógico.

-   **Passo 1: Elemento Raiz.** A tag principal do XML torna-se a chave do objeto JSON de topo.
-   **Passo 2: Mapeamento de Tags para Chaves.** Cada tag filha no XML corresponde a uma nova chave no objeto JSON. O conteúdo de texto da tag torna-se o valor dessa chave.
-   **Passo 3: Mapeamento de Atributos.** Atributos de uma tag XML (`<tag atributo="valor">`) são mapeados como pares chave-valor dentro do objeto JSON correspondente a essa tag.
-   **Passo 4: Mapeamento de Listas/Arrays.** Quando uma tag XML se repete em sequência (ex: `<item>...</item><item>...</item>`), deve ser mapeada como um array (lista `[]`) de objetos em JSON.

**Exemplo Conceitual:** Uma lista de livros em XML, onde cada livro tem um título e um autor, seria convertida para um array JSON chamado "livros", onde cada elemento é um objeto com as chaves "titulo" e "autor".

---

### **Parte 2: Análise de Padrão e Fluxo de Callbacks**

**1. Análise do Padrão (O "Porquê"):**
O padrão de design utilizado é a **Injeção de Dependências** via construtor.
- **Propósito:** Uma classe "sujeito" (`Contadores`) recebe "callbacks" (funções) no seu construtor e chama-os quando o seu estado interno muda. Isto permite que a classe notifique o mundo exterior sobre as suas mudanças, sem conhecer os detalhes de quem está a "ouvir". Promove o **desacoplamento**: o `Contadores` não conhece o `Callbacks`, apenas a "promessa" de que as funções que recebeu podem ser executadas.

**2. Rastreamento de Estado (O "Como"):**
Seguindo o fluxo da função `main`, o estado das variáveis é o seguinte:

| Ação | Efeito | Estado `_x` | Estado `_y` | Output |
| :--- | :--- | :--- | :--- |:--- |
| **Início** | `callbacks` é criado. | 0 | 0 | - |
| `contadores1.a = 3` | O setter `a` chama `onX(3)`. | `0 + 3 = 3` | 0 | - |
| `contadores1.b = 4` | O setter `b` chama `onY(4)`. | 3 | `3 + 4 = 7` | - |
| `contadores2.a = 10` | O setter `a` chama `onX(10)`. | `3 + 10 = 13`| 7 | - |
| `contadores2.b = 5` | O setter `b` chama `print(5)`. | 13 | 7 | `5` |
| `print(callbacks._x)` | Imprime o valor final de `_x`. | 13 | 7 | `13` |
| `print(callbacks._y)` | Imprime o valor final de `_y`. | 13 | 7 | `7` |

**Resultado Final:** O output do programa será `5`, `13`, `7`.

---

### **Parte 3: Conceitos Fundamentais de Flutter**

- **`StatelessWidget` vs. `StatefulWidget`:**
    - `StatelessWidget`: Para UI estática e imutável (ex: ícones, texto fixo). Uma vez construído, não muda.
    - `StatefulWidget`: Para UI dinâmica que muda em resposta a dados ou interações. Usa o método `setState()` para notificar o framework para reconstruir o widget com o novo estado.
    - **Dica de Exame:** Se a UI precisa de ser redesenhada após uma interação, a resposta é `StatefulWidget`.

- **Injeção de Dependências (DI):**
    - É uma técnica que consiste em fornecer as dependências a um objeto (via construtor), em vez de ele as criar. Isto desacopla o código e facilita os testes, permitindo substituir dependências reais por `mocks`.
    - **Dica de Exame:** Se um problema menciona trocar implementações (e.g., usar uma API falsa para testes), a DI é a solução.

- **Programação Assíncrona (`async/await`):**
    - Garante que operações demoradas (rede, I/O) não bloqueiam a UI. O `await` pausa a função assíncrona até a operação terminar, mas liberta o *thread* principal, mantendo a app responsiva.
    - **Dica de Exame:** Qualquer menção a pedidos de rede, acesso a bases de dados ou ficheiros implica o uso de `async/await`.

- **Testes de Widget vs. Integração:**
    - **Widget:** Testa um único widget de forma isolada. Rápido e focado num componente.
    - **Integração:** Testa um fluxo completo da app (end-to-end). Lento, precisa de um emulador/dispositivo e valida a interação entre vários ecrãs e serviços.
    - **Dica de Exame:** "Testar um formulário" é um teste de widget. "Testar o login e a navegação" é um teste de integração.

- **Padrão Repositório:**
    - Um mediador entre a lógica de negócio e as fontes de dados (API, cache local). A UI pede dados ao Repositório, que decide de onde os obter.
    - **Dica de Exame:** Se a app precisa de obter dados de forma transparente (online ou offline), o Padrão Repositório é a resposta.

- **Gestão de Estado (`Provider`):**
    - Resolve o problema de partilhar e sincronizar o estado da aplicação entre diferentes ecrãs ou widgets.
    - **Dica de Exame:** Se a pergunta envolve partilhar dados entre ecrãs, a resposta envolve uma solução de gestão de estado.

---

### **Parte 4: Conceitos de Computação Móvel**

- **Arquiteturas de App (P/C = Prós/Contras):**
    - **Nativa:** (P) Performance máxima, acesso total a APIs. (C) Custo alto (bases de código separadas).
    - **Híbrida-Web:** (P) Barata, código único. (C) Performance fraca, UX inferior, acesso limitado a APIs (corre numa `WebView`).
    - **Híbrida-Nativa (Flutter):** (P) Código único, performance perto de nativa, UI consistente. (C) Acesso a APIs nativas requer "plugins". **Melhor compromisso geral.**
    - **[Diagrama] Híbrida-Nativa:** Desenhar [UI Nativa (Widgets)] <-> [Bridge (Ponte)] <-> [Lógica da App (Dart)]. Contrastar com Nativa, que não tem a "ponte".

- **Usabilidade e Interação:**
    - **Leis:** Fitts (alvos grandes e próximos são mais rápidos de acertar), Hick (mais escolhas = mais tempo de decisão).
    - **Thumb Zone:** Ações primárias na zona de alcance do polegar (base do ecrã).
    - **Alvos de Toque:** Mínimo de 48dp (9mm) para evitar o "problema do dedo gordo".

- **Conectividade:**
    - **Desafios:** Latência, perda de rede, bateria.
    - **Estratégia Offline-First:** A app deve ser funcional offline. A UI carrega dados da cache local primeiro, e só depois sincroniza com a rede.

- **Geolocalização:**
    - **Tecnologias:** GPS (preciso, gasta bateria) vs. Redes Móveis/Wi-Fi (menos preciso, mais eficiente).
    - **Implicações:** Requer permissão explícita do utilizador. Sempre pedir a menor precisão necessária para a tarefa.

- **Autonomia (Bateria):**
    - **Otimizações:**
        - **Rede:** Agrupar (`batching`) pedidos de rede para permitir que o rádio "durma".
        - **GPS:** Desligar o sensor assim que a localização for obtida.
        - **Processamento:** Usar `WorkManager` para agendar tarefas não urgentes, permitindo que o SO as execute em momentos oportunos (e.g., **Modo Doze**).

- **Sensores:**
    - **Tipos:** Físicos (acelerómetro), Lógicos (detetor de passos), Biométricos.
    - **Sensor Fusion:** Combinar dados de múltiplos sensores para obter uma leitura mais precisa e fiável.

- **Serviços Externos:**
    - **Padrão:** App -> HTTP Request -> API (REST/JSON) -> Servidor.
    - **REST:** Usa verbos HTTP (`GET`, `POST`) em `Endpoints` (URLs) para manipular recursos.
    - **Tokens (JWT):** Usados para autenticar pedidos a APIs. Obtidos no login e enviados no `Header` de cada pedido.

- **Modelos de Negócio:**
    - **Custos Loja:** App Store ($99/ano), Google Play ($25 uma vez). Ambos com comissão de 15-30%.
    - **Modelos:** **Paga** (difícil), **Anúncios** (requer volume), **Freemium** (comum: grátis com extras pagos), **Subscrição** (receita recorrente). 