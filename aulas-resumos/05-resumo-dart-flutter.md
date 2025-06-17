# Resumo: Aula 5 - Dart e Fundamentos de Flutter

## 1. A Linguagem Dart: Pilares para Flutter

O Flutter é um framework, mas a lógica é escrita em Dart. Dominar os seguintes conceitos da linguagem é essencial.

- **Compilação Híbrida (A Chave do Flutter):**
    - **JIT (Just-in-Time):** Em desenvolvimento, usa uma Dart VM que compila o código "à medida que é preciso". Isto permite o **Hot Reload**, que injeta o código novo na app a correr, atualizando a UI em <1 segundo sem perder o estado da aplicação. Acelera drasticamente o desenvolvimento.
    - **AOT (Ahead-of-Time):** Em produção (release), o código é compilado diretamente para código máquina nativo (ARM/x64), o que garante **desempenho máximo** e arranque rápido da aplicação.

- **Sintaxe Fundamental:**
    - **Variáveis:** `var` (tipo inferido), `String`, `int`, `double`, `bool`. `final` para variáveis que só são atribuídas uma vez, `const` para valores conhecidos em tempo de compilação.
    - **Null Safety:** Um dos pilares do Dart moderno. Tipos são não-nuláveis por defeito.
        - `String?`: Declara uma variável que *pode* ser nula.
        - `required`: Usado em construtores para indicar que um parâmetro é obrigatório.
        - `??`: O operador "if-null". Ex: `var nome = variavelPodeSerNula ?? 'Valor Padrão';`.
    - **Coleções:**
        - **Listas:** `var nomes = ['Ana', 'Rui'];`
        - **Mapas:** `var capitais = { 'Portugal': 'Lisboa', 'Brasil': 'Brasília' };`
    - **String Interpolation:** `print('Olá, $nome. Bem-vindo a ${capitais['Portugal']}');`
    - **Funções Arrow (Lambdas):** Para funções com uma única expressão.
        - `(n1, n2) => n1 > n2;` é o mesmo que `bool maior(n1, n2) { return n1 > n2; }`

- **Classes e Construtores (Estilo Flutter):**
    - Flutter usa intensivamente **named parameters** nos construtores para clareza.
    ```dart
    class BotaoCustom extends StatelessWidget {
      final String texto;
      final Color cor;
      final double? elevacao; // Parâmetro opcional

      // Construtor com named parameters. `required` força a sua passagem.
      const BotaoCustom({
        super.key,
        required this.texto,
        required this.cor,
        this.elevacao,
      });
      // ... build() method
    }
    ```

---

## 2. Flutter: "Tudo é um Widget"

A UI é uma **árvore de widgets**. Um botão, um texto, o padding, um ecrã inteiro... tudo é um widget, construído por **composição** (widgets dentro de outros widgets).

### `StatelessWidget` vs. `StatefulWidget`

- **`StatelessWidget` (Estático):**
    - Um widget **imutável**. Os seus dados (propriedades) vêm do seu "pai" e não podem ser alterados internamente.
    - Usa-se para partes da UI que não mudam depois de serem desenhadas (um título, um ícone, um texto decorativo).

- **`StatefulWidget` (Dinâmico):**
    - Um widget que **pode manter estado interno e mudar** em resposta a eventos.
    - É composto por duas classes: a `Widget` (imutável) e o seu `State` (mutável).
    - Para atualizar a UI, é **obrigatório** chamar o método `setState(() { ... })` dentro da classe `State`. Este método notifica o Flutter que o estado mudou, fazendo com que o método `build()` seja chamado novamente para reconstruir a UI com os novos valores.

---

## 3. Widgets Essenciais: A Caixa de Ferramentas

Para construir qualquer ecrã, vais precisar de combinar estes widgets fundamentais.

- **Estrutura Base do Ecrã:**
    - `Scaffold`: Implementa a estrutura visual básica do Material Design. Dá-te um `appBar` (barra no topo), um `body` (o conteúdo principal), `floatingActionButton`, `bottomNavigationBar`, etc. Quase todos os ecrãs começam com um `Scaffold`.

- **Layout (Posicionamento):**
    - `Container`: O "canivete suíço". Permite definir cor de fundo, padding, margens, bordas, sombras, etc.
    - `Row` e `Column`: Os mais importantes. Organizam uma lista de widgets-filhos na horizontal (`Row`) ou vertical (`Column`).
    - `Padding`: Adiciona espaço vazio à volta de um widget-filho.
    - `Center`: Centra o seu widget-filho.
    - `ListView`: Cria uma lista de widgets que pode ser scrollada. Essencial para mostrar listas de dados.
    - `Stack`: Permite sobrepor widgets uns aos outros (e.g., colocar texto sobre uma imagem).

- **Conteúdo e Interação:**
    - `Text`: Mostra uma string de texto.
    - `Image`: Mostra uma imagem (`Image.asset` para imagens locais, `Image.network` para imagens da web).
    - `Icon`: Mostra um ícone da biblioteca do Material Design.
    - `ElevatedButton`, `TextButton`, `IconButton`: Diferentes tipos de botões para o utilizador clicar.

---

## 4. Navegação e Comunicação entre Ecrãs

- **Navegação Básica:** Usa a classe `Navigator`.
    - `Navigator.push(context, MaterialPageRoute(builder: (context) => EcradeDetalhe()));`
        - Empurra um novo ecrã para a "pilha" de navegação.
    - `Navigator.pop(context);`
        - Remove o ecrã atual da pilha, voltando ao anterior.
- **Passar Dados para o Novo Ecrã:** A forma mais comum é através do construtor do widget do novo ecrã.
    ```dart
    // No ecrã da lista, ao clicar:
    Navigator.push(context, MaterialPageRoute(
      builder: (context) => EcradeDetalhe(hospitalId: '123', veioDoMapa: false)
    ));

    // No widget EcradeDetalhe:
    class EcradeDetalhe extends StatelessWidget {
      final String hospitalId;
      final bool veioDoMapa;
      const EcradeDetalhe({super.key, required this.hospitalId, required this.veioDoMapa});
      // ...
    }
    ```
- **Devolver Dados ao Ecrã Anterior:** O `pop` pode devolver um valor, que é recebido através do `Future` que o `push` retorna.
    ```dart
    // No ecrã A:
    final resultado = await Navigator.push(context, ...); // Espera pelo resultado
    
    // No ecrã B, ao voltar:
    Navigator.pop(context, 'Dados de volta!'); // Envia o resultado
    ```

---

## 5. Feedback ao Utilizador

- **`SnackBar`:** Uma mensagem temporária que aparece na parte de baixo do ecrã. Ideal para confirmações rápidas ("Item guardado") ou alertas.
    ```dart
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Avaliação submetida!'))
    );
    ```

---

## 6. Gestão de Estado (State Management) - Introdução

Em apps pequenas, `StatefulWidget` é suficiente. Mas quando vários ecrãs precisam de partilhar ou reagir ao mesmo estado, passar dados através de construtores (`prop drilling`) torna-se complexo. Surgem as arquiteturas de gestão de estado:
- **`Provider`:** Uma forma simples de "prover" um estado a todos os widgets descendentes na árvore que precisem dele, sem o passar manualmente.
- **`Bloc`:** Um padrão mais robusto, baseado em eventos e estados, que separa a lógica de negócio da UI.
Para o exame, `StatefulWidget` é provavelmente o esperado, mas conhecer estes termos demonstra uma compreensão mais profunda. 