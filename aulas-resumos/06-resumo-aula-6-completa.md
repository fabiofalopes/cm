# Resumo: Aula 6 - Usabilidade, Layout, Formulários e Navegação

A sexta aula foca-se em quatro pilares da construção de interfaces em Flutter, desde os princípios de design até à implementação técnica.

## 1. Usabilidade Móvel: Desenhar para o Mundo Real

A interação em mobile é condicionada por fatores como ecrãs reduzidos, interrupções constantes, uso com uma mão e visibilidade variável. O design deve acomodar estas limitações.

### A) O Problema do "Dedo Gordo" (Fat Finger Problem)
- **Conceito:** A área de toque do dedo humano é grande e imprecisa. Elementos interativos demasiado pequenos ou próximos causam erros de clique frustrantes.
- **Solução Prática:** Garantir que os alvos de toque (`touch targets`) têm um tamanho mínimo adequado.
    - **Recomendação:** A Google recomenda um mínimo de **48x48dp** para qualquer elemento clicável.
    - **Boa Prática:** Aumentar a área de interação para além do ícone/texto visível. Por exemplo, numa lista com um checkbox, tornar a linha inteira clicável para ativar a seleção, maximizando a área de sucesso.

### B) A "Thumb Zone" (Zona de Alcance do Polegar)
- **Conceito:** Ao usar o telemóvel com uma só mão, a maior parte do ecrã é de difícil ou desconfortável alcance para o polegar.
- **Implicação no Design:** As ações primárias e a navegação principal devem ser posicionadas na "zona verde", na parte inferior e central do ecrã.
    - **Widgets Ideais para a Thumb Zone:** `BottomNavigationBar`, `TabBar`, `FloatingActionButton` (FAB).
    - **Anti-Padrão:** Colocar ações importantes ou menus nos cantos superiores do ecrã.

---

## 2. Layout em Flutter: Organizar os Widgets

Flutter abandona o posicionamento absoluto (coordenadas X, Y) em favor de um sistema de **posicionamento relativo e em grelha**, ideal para ecrãs de diferentes tamanhos. A UI é construída aninhando widgets de layout.

- **Pilares do Layout:** `Row` e `Column`.
    - `Row`: Alinha os seus widgets-filhos (`children`) na horizontal.
    - `Column`: Alinha os seus filhos na vertical.
    - **Eixos:** Cada um tem um eixo principal (`mainAxisAlignment`) e um secundário (`crossAxisAlignment`). No `Column`, o eixo principal é o vertical. No `Row`, é o horizontal.
        - `mainAxisAlignment`: Controla o espaçamento ao longo do eixo principal (e.g., `.start`, `.center`, `.spaceBetween`).
        - `crossAxisAlignment`: Controla o alinhamento no eixo secundário (e.g., `.start`, `.center`, `.stretch`).

- **Flexibilidade e Espaçamento:**
    - `Expanded`: Força o seu filho a ocupar **todo o espaço livre disponível** no eixo principal de um `Row` ou `Column`. Se vários widgets forem `Expanded`, o espaço é dividido de acordo com o `flex factor`.
    - `Flexible`: Permite que o filho ocupe o espaço disponível, mas **não o força** a isso. Se o conteúdo do filho for menor que o espaço, ele ocupará apenas o necessário.
    - `Spacer`: Um widget invisível que ocupa o espaço disponível, útil para empurrar outros widgets para os cantos.

- **Widgets de Posição e Decoração:**
    - `Container`: O canivete suíço para layouts. Um widget que combina funcionalidades de posicionamento e decoração. Pode definir `width`, `height`, `padding` (espaçamento interno), `margin` (espaçamento externo), `color` e `decoration` (bordas, sombras, etc.).
    - `Stack`: Permite sobrepor widgets (como z-index na web). O primeiro filho na lista é o de baixo. Usa-se o widget `Positioned` para controlar a localização exata de cada filho dentro do `Stack`.

---

## 3. Formulários em Flutter: Simplificar a Entrada de Dados

- **Princípio Fundamental:** **Fazer o utilizador escrever o mínimo possível.** Em mobile, escrever é um esforço.
    - **Técnicas:** Usar auto-complete, teclados específicos para o tipo de dados (`keyboardType`), valores por omissão, e sempre que possível, substituir a escrita por interação (e.g., usar a câmara para ler um cartão de crédito, GPS para obter a morada, sliders em vez de campos de número).

- **Implementação Técnica com `Form`:**
    - **1. Chave Global (`GlobalKey`):**
        - `final _formKey = GlobalKey<FormState>();`
        - Cria uma chave única para identificar e mais tarde aceder ao estado do nosso formulário.
    - **2. Widget `Form`:**
        - `Form(key: _formKey, child: ...)`
        - Agrupa todos os campos de formulário.
    - **3. Campos de Formulário (`TextFormField`):**
        - Um `TextFormField` é um `TextField` com super-poderes que se integra com o `Form`.
        - **`validator`**: Propriedade que recebe uma função `(value) { ... }`. Esta função valida o input do utilizador. Deve retornar `null` se o valor for válido, ou uma `String` com a mensagem de erro se for inválido.
        - **`onSaved`**: Callback chamado para cada campo quando se invoca `_formKey.currentState!.save()`. É aqui que guardamos o valor final do campo numa variável de estado ou num objeto.
        - **`controller`**: (Opcional) Permite ler ou modificar o texto do campo programaticamente, usando um `TextEditingController`.

- **Fluxo de Validação e Submissão:**
    1.  O utilizador clica no botão "Submeter".
    2.  A função do botão chama `if (_formKey.currentState!.validate()) { ... }`.
    3.  Isto aciona a função `validator` de **todos** os `TextFormField`s dentro do `Form`.
    4.  Se todos os `validator`s devolverem `null`, `validate()` retorna `true`.
    5.  Dentro do `if`, chamamos `_formKey.currentState!.save()`, o que aciona o `onSaved` de todos os campos.
    6.  Se algum `validator` devolver uma `String`, `validate()` retorna `false` e exibe as mensagens de erro nos respetivos campos.

---

## 4. Navegação em Flutter: Gerir Ecrãs

### Padrões de Navegação
- **Persistente:** Os controlos de navegação estão sempre visíveis. É fácil de descobrir, mas ocupa espaço precioso no ecrã.
    - **Exemplos:** `BottomNavigationBar`, `TabBar`, `FloatingActionButton`. Ideal para as 2 a 5 secções principais da app.
- **Transiente:** Os controlos estão ocultos e são revelados por uma ação do utilizador. Poupa espaço, mas é menos visível para o utilizador.
    - **Exemplo:** `Drawer` (o "menu hambúrguer"), que desliza a partir da lateral.

### `Navigator`: A Pilha de Ecrãs
- Flutter gere a navegação como uma **pilha (stack) de ecrãs (chamados `Route`)**. O ecrã visível é o que está no topo da pilha.
- **Ir para um novo ecrã (`push`):**
    - `Navigator.push(context, MaterialPageRoute(builder: (context) => DetailScreen(data: myData)));`
    - Isto "empurra" uma nova `Route` para o topo da pilha. Para passar dados para o novo ecrã, usa-se o construtor do seu widget, como no exemplo (`data: myData`).
- **Voltar ao ecrã anterior (`pop`):**
    - `Navigator.pop(context);`
    - Isto "remove" o ecrã do topo da pilha, revelando o que estava por baixo.
- **Devolver um Resultado:** `pop` pode devolver um valor ao ecrã anterior, que por sua vez pode esperar por ele com `await`.
    ```dart
    // No ecrã da lista (ecrã A)
    Future<void> _navigateToDetail() async {
      // Espera pelo resultado que o ecrã de detalhe possa devolver
      final result = await Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => DetailScreen()),
      );

      // Quando o DetailScreen fizer 'pop', este código executa
      if (result != null) {
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text('Voltou com: $result')));
      }
    }

    // No ecrã de detalhe (ecrã B), no botão de voltar
    ElevatedButton(
      onPressed: () {
        // Devolve o valor 'Operação concluída' ao ecrã anterior
        Navigator.pop(context, 'Operação concluída');
      },
      child: Text('Voltar com Resultado'),
    )
    ``` 