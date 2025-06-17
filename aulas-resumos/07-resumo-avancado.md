# Resumo: Aula 7 - Funcional, Testes e Injeção de Dependências

## 1. Programação Funcional em Dart

Dart é uma linguagem multi-paradigma que abraça conceitos funcionais, tornando o código mais declarativo e conciso, especialmente para manipulação de coleções.

- **Funções como Cidadãos de Primeira Classe:** Podem ser guardadas em variáveis, passadas como argumentos para outras funções e retornadas como resultado.
    - **Tipagem de Funções:** Para segurança em tempo de compilação, é crucial tipar as variáveis que guardam funções.
      ```dart
      // Esta variável só pode guardar funções que recebem um int e retornam uma String.
      String Function(int) formatador; 
      ```

- **Funções Anónimas (Lambdas):** Funções sem nome, úteis para passar como argumento de forma rápida.
    - **Sintaxe:** `(parametros) => expressao;`
      `var dobro = (int n) => n * 2;`

- **Métodos Funcionais Essenciais (em `Iterable`s como `List`):**
    - **`.map((elemento) => ...)`**: Transforma cada elemento da coleção num novo, criando uma nova coleção. Retorna um `Iterable`, sendo comum terminar com `.toList()`.
        ```dart
        // [1, 2, 3] -> [2, 4, 6]
        var numerosDobrados = [1, 2, 3].map((n) => n * 2).toList();
        ```
    - **`.where((elemento) => ...)`**: Filtra a coleção, retornando um `Iterable` apenas com os elementos que cumprem a condição booleana.
        ```dart
        // [1, 2, 3, 4] -> [2, 4]
        var apenasPares = [1, 2, 3, 4].where((n) => n.isEven).toList();
        ```
    - **`.reduce((valorAcumulado, elemento) => ...)`**: Combina (reduz) todos os elementos de uma coleção num único valor.
        ```dart
        // [1, 2, 3, 4] -> 10
        var soma = [1, 2, 3, 4].reduce((somaParcial, n) => somaParcial + n);
        ```
    - **Encadeamento (Chaining):** A verdadeira força destes métodos está na sua combinação.
        ```dart
        // Obter o quadrado dos números pares de uma lista
        var resultado = numeros.where((n) => n.isEven).map((n) => n * n).toList();
        ```

---

## 2. Injeção de Dependências (DI)

- **O Problema (Acoplamento Forte):** Uma classe que cria as suas próprias dependências internamente fica "amarrada" a uma implementação específica. Isto torna o código rígido e difícil de testar.
    ```dart
    // Mau: A classe UserRepository está fortemente acoplada à classe real ApiService.
    // Como podemos testar UserRepository sem fazer chamadas reais à API?
    class UserRepository {
      final _api = ApiService(); // Cria a sua própria dependência.

      Future<User> getUser(int id) => _api.fetchUser(id);
    }
    ```
- **A Solução (Inversão de Controlo - IoC):** A classe não cria as suas dependências, mas sim **recebe-as** de fora, geralmente através do construtor. A isto chama-se **Injeção via Construtor**.
    ```dart
    // Bom: A classe depende de uma abstração (ApiService) e não de uma implementação concreta.
    class UserRepository {
      final ApiService _api; // Agora depende de uma interface/contrato.
      
      UserRepository({required ApiService api}) : _api = api; // A dependência é injetada.

      Future<User> getUser(int id) => _api.fetchUser(id);
    }
    ```

- **Benefício Principal: Testabilidade:** Nos testes, podemos criar uma implementação "falsa" (`Mock`) da dependência e injetá-la no lugar da real.
    ```dart
    // test/user_repository_test.dart
    test('getUser returns a user if the http call completes successfully', () {
      final mockApiService = MockApiService(); // Uma classe falsa que não faz chamadas de rede.
      final userRepository = UserRepository(api: mockApiService);

      // Configuramos o mock para retornar um User quando fetchUser for chamado.
      when(mockApiService.fetchUser(1)).thenAnswer((_) async => User(id: 1, name: 'Test User'));

      expect(await userRepository.getUser(1), isA<User>());
    });
    ```

- **Service Locators (`get_it`):** Para evitar passar dependências manualmente pela árvore de widgets (`prop drilling`), usam-se pacotes como o `get_it`. É um "mapa" global onde se pode registar e pedir instâncias de classes.
    1.  **Registar (no arranque da app):** `getIt.registerLazySingleton<ApiService>(() => ApiServiceImpl());`
    2.  **Localizar (num widget ou ViewModel):** `final myApi = getIt<ApiService>();`

---

## 3. Testes em Flutter

| Tipo | Objetivo | Diretoria | Dependência | Velocidade | Precisa de Emulador? |
|:---|:---|:---|:---|:---:|:---:|
| **Unitário** | Testa lógica pura de Dart (uma classe, uma função). | `test/` | `test` | ⚡️ Rápido | Não |
| **Widget** | Testa um widget da UI de forma isolada (layout, estado). | `test/` | `flutter_test` | ⚡️ Rápido | Não |
| **Integração**| Testa um fluxo completo da app, simulando um utilizador. | `integration_test/`| `integration_test`| 🐢 Lento | Sim |

### Testes Unitários
- Usam `test('descrição', () => ...);` e `expect(valor_real, matcher_esperado);`.
- Ex: `expect(calculator.add(2, 2), 4);`, `expect(myList, isEmpty);`.

### Testes de Widget
- O setup é `testWidgets('descrição', (WidgetTester tester) async { ... });`.
- O `WidgetTester` é a ferramenta central para interagir com o ambiente de teste.
    - **`await tester.pumpWidget(MeuWidget());`**: Renderiza o widget no ambiente de teste.
    - **`await tester.tap(finder);`**: Simula um toque num widget encontrado.
    - **`await tester.enterText(finder, 'texto');`**: Simula a escrita de texto num campo.
    - **`await tester.pump()`**: Avança um frame na animação, útil após ações.
- **`find`**: Objeto global para encontrar widgets na árvore de widgets.
    - **`find.text('Olá')`**: Encontra um widget `Text`.
    - **`find.byType(ElevatedButton)`**: Encontra pela classe do widget.
    - **`find.byKey(Key('chave-unica'))`**: A forma mais fiável. Encontra um widget pela sua `Key`.
- **Exemplo Prático (Teste de Widget de Contador):**
    ```dart
    testWidgets('Counter increments smoke test', (WidgetTester tester) async {
      // 1. Arrange: Renderiza a nossa app/widget.
      await tester.pumpWidget(const MyApp());

      // 2. Act & Assert (antes da ação)
      // Verifica que o contador começa em 0.
      expect(find.text('0'), findsOneWidget);
      expect(find.text('1'), findsNothing);

      // 3. Act: Simula um toque no botão com o ícone de 'add'.
      await tester.tap(find.byIcon(Icons.add));
      await tester.pump(); // Avança o estado após o setState.

      // 4. Assert (depois da ação)
      // Verifica que o contador foi incrementado.
      expect(find.text('0'), findsNothing);
      expect(find.text('1'), findsOneWidget);
    });
    ``` 