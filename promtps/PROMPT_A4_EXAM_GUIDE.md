# Super-Prompt: Geração de Guia de Estudo A4 para Exame de Computação Móvel

## 1. Objetivo Principal

O objetivo é gerar o conteúdo para um **guia de estudo de uma única folha A4**, otimizado para ser **transcrito à mão**. Este guia deve ser o recurso de consulta perfeito para o exame de Computação Móvel, cobrindo todos os tópicos essenciais de forma densa, estruturada e visualmente clara.

## 2. Restrições Críticas (Extraídas de @aula-13.md)

Aderir estritamente às seguintes regras. A violação destas regras torna o guia inútil.

- **NÃO incluir código Dart.** A explicação de conceitos de programação deve ser feita através de pseudocódigo, descrições de fluxo ou diagramas conceituais.
- **NÃO incluir excertos de JSON.** A explicação do formato e da sua manipulação deve ser conceitual.
- **APENAS texto e diagramas.** O conteúdo deve ser composto por texto conciso e descrições de diagramas que possam ser facilmente desenhados à mão.

## 3. Fontes de Informação

A geração do conteúdo deve basear-se na síntese e cruzamento das seguintes fontes de informação, garantindo uma cobertura completa e precisa da matéria:

- **Aulas Completas:** `@/aulas-md/` (Fonte primária para a teoria)
- **Resumos das Aulas:** `@/aulas-resumos/` (Para identificar os pontos-chave de cada aula)
- **Quizzes:** `@/quiz/` (Para validar os conceitos mais importantes e formatos de pergunta)
- **Transcrições Práticas:** `@/youtube_transcripts/md/` (Para extrair a essência dos conceitos práticos de Flutter)
- **Guia do Exame:** `@/aulas-md/aula-13.md` (A fonte de verdade para a estrutura do exame e as regras)

## 4. Estratégia de Geração Iterativa e Foco

O guia deve ser construído em **iterações sequenciais**, uma para cada secção do exame. Esta abordagem garante que cada tópico é abordado com a profundidade necessária, sem que o contexto geral se perca. Para as partes práticas (JSON e Callbacks), o foco não é apenas na solução, mas em construir um **framework mental** que permita resolver problemas semelhantes.

---

## 5. Geração do Guia de Estudo (Execução Iterativa)

### **Iteração 1: Parte 1 - Formato JSON (Preparação e Conceitos)**

**Tarefa:** Criar um "Guia Mental de Conversão XML->JSON" que sirva como um checklist de raciocínio para o exame.

- **Instruções:**
    1.  **Não use o exemplo XML->JSON da `aula-13.md`**.
    2.  Formule as regras de mapeamento como um **processo passo-a-passo**:
        -   **Passo 1: Elemento Raiz.** Identifique a tag principal do XML; ela será a chave de topo no objeto JSON.
        -   **Passo 2: Mapeamento de Tags para Chaves.** Cada tag filha do XML torna-se uma chave no objeto JSON correspondente. O conteúdo da tag torna-se o valor da chave.
        -   **Passo 3: Mapeamento de Atributos.** Atributos de uma tag XML são geralmente mapeados como chaves-valor dentro do objeto JSON dessa tag.
        -   **Passo 4: Mapeamento de Listas/Arrays.** Uma sequência de tags XML com o mesmo nome (e.g., `<ator>...</ator><ator>...</ator>`) deve ser mapeada para um array de objetos em JSON.
    3.  Ilustre a ideia com um micro-exemplo conceitual para reforçar o padrão (e.g., `Livro(titulo, autor)` -> `{ "livro": { "titulo": "...", "autor": "..." } }`).

---

### **Iteração 2: Parte 2 - Processamento Callbacks (Análise de Padrões e Fluxo)**

**Tarefa:** Desconstruir a lógica do exercício de callbacks, focando primeiro no padrão de design e depois no fluxo de execução.

- **Instruções:**
    1.  **Análise do Padrão (O "Porquê"):**
        -   Primeiro, descreva o padrão de design em jogo. Explique que o código usa a **injeção de dependências via construtor** para passar funções (`callbacks`) a uma classe (`Contadores`).
        -   Clarifique o propósito: `Contadores` é um "sujeito" que notifica "observadores" externos (os métodos em `Callbacks`) sobre mudanças no seu estado interno, sem precisar de os conhecer diretamente. Isto promove o desacoplamento.
    2.  **Rastreamento de Estado (O "Como"):**
        -   A seguir, crie uma "tabela de execução" ou um log de rastreamento da função `main`.
        -   Para cada instrução (`contadores1.a = 3;`, `contadores1.b = 4;`, etc.), descreva o efeito em cadeia:
            - **Ação:** e.g., `contadores1.a = 3`
            - **Efeito:** "O `setter set a` é chamado. A função `_f1` (que aponta para `callbacks.onX`) é invocada com o valor 3. O estado `callbacks._x` passa a ser `0 + 3 = 3`."
        -   Continue para todas as linhas, atualizando o estado de `_x` e `_y` a cada passo.
        -   No final, apresente os valores finais e o output, justificando com base no rastreamento.

---

### **Iteração 3: Parte 3 - Conceitos e Programação Flutter (Definições para Exame)**

**Tarefa:** Produza definições ultra-concisas e uma "dica de exame" para cada conceito fundamental de Flutter.

- **Instruções:**
    - Sintetize as informações das fontes com foco no "porquê" e "quando".
    - Para cada conceito, adicione uma **Dica de Exame** para ajudar a identificar o conceito em perguntas.
    - **`StatelessWidget` vs. `StatefulWidget`:** Diferença (estado imutável vs. mutável). **Dica:** Se a pergunta descreve uma UI que muda com base em interações do utilizador ou dados internos, a resposta envolve `StatefulWidget` e `setState`.
    - **Injeção de Dependências (DI):** Propósito (desacoplar, facilitar testes). **Dica:** Se um problema menciona a necessidade de trocar implementações (e.g., usar uma API falsa para testes), a DI é a solução.
    - **Programação Assíncrona (`async/await`):** Importância (não bloquear a UI em operações de I/O). **Dica:** Qualquer menção a pedidos de rede, acesso a bases de dados ou ficheiros implica o uso de programação assíncrona.
    - **Testes de Widget vs. Integração:** Diferença de escopo (um widget vs. um fluxo de ecrãs). **Dica:** "Testar um formulário" é um teste de widget. "Testar o login e a navegação para a home" é um teste de integração.
    - **Padrão Repositório:** Função (mediador entre lógica de negócio e fontes de dados). **Dica:** Quando a aplicação precisa de obter dados (de uma API ou cache local) de forma transparente, o padrão repositório é a resposta.
    - **Gestão de Estado:** Problema (sincronizar dados e UI). **Dica:** Se a pergunta envolve partilhar dados entre diferentes ecrãs, a resposta envolve uma solução de gestão de estado como `Provider`.

---

### **Iteração 4: Parte 4 - Conceitos Computação Móvel (Síntese Densa)**

**Tarefa:** Crie a secção mais densa do guia, usando listas, palavras-chave e descrições de diagramas.

- **Instruções:**
    - Para cada tópico, sintetize a essência das `aulas-md` e `aulas-resumos`. Use abreviações (e.g., "P/C" para prós/contras).
    - **Arquiteturas de App:**
        - **Nativa, Híbrida-Web, Híbrida-Nativa:** Tabela comparativa (P/C) focada em: Performance, Custo, Acesso a APIs, Portabilidade.
        - **[Diagrama] Arquitetura Híbrida-Nativa:** Descrever um diagrama que mostra [UI Nativa] <-> [Bridge] <-> [Lógica Dart/JS], contrastando com a Nativa que não tem a "ponte".
    - **Usabilidade e Interação:** Listar 3-4 princípios chave (e.g., Leis de Fitts/Hick, consistência, feedback).
    - **Conectividade:** Tipos (Wi-Fi, Celular), Desafios (Latência, Perda de rede), Estratégia "Offline-first".
    - **Geo-localização:** Tecnologias (GPS vs. Rede), Trade-off (Precisão vs. Bateria), Implicações (Privacidade, Permissões).
    - **Autonomia:** Otimizações chave (Reduzir I/O de rede/disco, usar modo escuro em OLED, agrupar tarefas).
    - **Sensores:** Listar comuns (Acelerómetro, Giroscópio, etc.), Conceito de "Sensor Fusion" (combinar sensores para dados melhores).
    - **Integração com Serviços Externos:** Padrão (App -> HTTP -> API REST/JSON -> Servidor).
    - **Modelos de Negócio:** Descrever em uma linha: Premium, Freemium, Subscrição, Publicidade.

---

## 6. Revisão Final

Após gerar todo o conteúdo, faça uma revisão final para garantir que:
1.  O conteúdo cabe, realisticamente, numa folha A4 quando escrito à mão.
2.  NENHUMA regra da secção 2 foi violada.
3.  A linguagem é clara, direta e otimizada para consulta rápida durante o exame. 