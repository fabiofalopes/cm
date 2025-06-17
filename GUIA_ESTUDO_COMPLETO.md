# Estrutura e Regras do Exame

- **Formato:** Perguntas de resposta aberta.
- **Consulta:** É permitida uma **única folha A4, manuscrita** (frente e verso).
- **Restrições da Folha (Oficiais):** A folha de consulta **não pode conter código Dart nem excertos JSON**. Use este guia para preparar essa folha.

### Pontuação
- **Parte 1:** Formato JSON (2 valores)
- **Parte 2:** Programação com Callbacks (2 valores)
- **Parte 3:** Conceitos e Programação Flutter (4 valores)
- **Parte 4:** Conceitos de Computação Móvel (12 valores)

---

## Parte 1: Transformação de XML para JSON

O objetivo é converter uma estrutura XML para JSON.

**Exemplo XML:**
```xml
<response>
    <code>Success</code>
    <body>
        <count>2</count>
        <movies>
            <movie name="Gladiador" year="2000" rating="8.5">
                <actor name="Russell Crowe" />
                <actor name="Joaquin Phoenix" />
            </movie>
            <movie name="The Matrix" year="1999" rating="8.7">
                <actor name="Keanu Reeves" />
                <actor name="Carrie-Anne Moss" />
            </movie>
        </movies>
    </body>
</response>
```

**Lógica e Resultado JSON:**

- **Regra 1: Tags Aninhadas → Objetos Aninhados.** `<response>` e `<body>` tornam-se objetos.
- **Regra 2: Tags com Texto → Pares Chave-Valor.** `<code>Success</code>` vira `"code": "Success"`.
- **Regra 3: Atributos de Tag → Pares Chave-Valor.** `name="..."` vira `"name": "..."`.
- **Regra 4: Múltiplas Tags Iguais → Lista de Objetos.** Vários `<movie>` e `<actor>` viram listas `[]`.
- **Regra 5: Tipagem de Dados.** `year="2000"` vira `"year": 2000` (número).

**JSON Equivalente:**
```json
{
  "response": {
    "code": "Success",
    "body": {
      "count": 2,
      "movies": [
        {
          "name": "Gladiador",
          "year": 2000,
          "rating": 8.5,
          "actors": [
            { "name": "Russell Crowe" },
            { "name": "Joaquin Phoenix" }
          ]
        },
        {
          "name": "The Matrix",
          "year": 1999,
          "rating": 8.7,
          "actors": [
            { "name": "Keanu Reeves" },
            { "name": "Carrie-Anne Moss" }
          ]
        }
      ]
    }
  }
}
```

---

## Parte 2: Lógica de Callbacks e Análise de Código

O objetivo é analisar código Dart que usa callbacks para perceber o fluxo de execução e prever o output.

**Código de Exemplo:**
```dart
// Objeto que dispara os callbacks através de setters
class Contadores {
  int _a = 0, _b = 0;
  Function _f1, _f2;
  Contadores(this._f1, this._f2);
  set a(int value) { _a = value; _f1(_a); }
  set b(int value) { _b = value; _f2(_b); }
}

// Objeto que contém o estado e os métodos (callbacks) que o alteram
class Callbacks {
  int _x = 0, _y = 0;
  void onX(int v) { _x += v; }
  void onY(int v) { _y = _x + v; }
}

// Execução Principal
void main() {
  Callbacks callbacks = Callbacks(); // Estado inicial: _x = 0, _y = 0
  Contadores contadores1 = Contadores(callbacks.onX, callbacks.onY);
  Contadores contadores2 = Contadores(callbacks.onX, (x) => print(x));

  contadores1.a = 3;
  contadores1.b = 4;
  contadores2.a = 10;
  contadores2.b = 5;

  print(callbacks._x);
  print(callbacks._y);
}
```

**Análise Passo-a-Passo:**

1.  **`Callbacks callbacks = Callbacks();`** → Cria o objeto que guarda o estado. `_x` é `0`, `_y` é `0`.
2.  **`Contadores contadores1 = ...`** → `contadores1` fica com referências para `callbacks.onX` e `callbacks.onY`.
3.  **`Contadores contadores2 = ...`** → `contadores2` fica com uma referência para `callbacks.onX` e uma função anónima (lambda) que imprime o seu argumento.
4.  **`contadores1.a = 3;`** → Invoca o `setter a` de `contadores1`. Este chama `_f1(3)`, que é `callbacks.onX(3)`. O estado muda: `_x` passa a `0 + 3 = 3`.
5.  **`contadores1.b = 4;`** → Invoca o `setter b` de `contadores1`. Este chama `_f2(4)`, que é `callbacks.onY(4)`. O estado muda: `_y` passa a `_x (que é 3) + 4 = 7`.
6.  **`contadores2.a = 10;`** → Invoca o `setter a` de `contadores2`. Este chama `_f1(10)`, que é `callbacks.onX(10)`. O estado muda: `_x` passa a `3 + 10 = 13`.
7.  **`contadores2.b = 5;`** → Invoca o `setter b` de `contadores2`. Este chama `_f2(5)`, que é a lambda `(x) => print(x)`. **Output no ecrã: `5`**. O estado do objeto `callbacks` não é afetado.
8.  **`print(callbacks._x);`** → Imprime o valor final de `_x`. **Output no ecrã: `13`**.
9.  **`print(callbacks._y);`** → Imprime o valor final de `_y`. **Output no ecrã: `7`**.

**Output Final Esperado:**
```
5
13
7
```

---

## Parte 3: Conceitos Fundamentais de Flutter

### A) Respostas Curtas (com exemplos)

- **StatelessWidget vs. StatefulWidget:**
  - **Stateless:** UI imutável. Recriado do zero quando o pai muda.
    - **Uso:** `Icon(Icons.add)`, `Text('Olá')`.
  - **Stateful:** UI dinâmica. O `State` persiste e é reutilizado. A UI é reconstruída via `setState()`.
    - **Uso:** Formulários, contadores, qualquer ecrã que reaja a interações.

- **Injeção de Dependências (DI):**
  - Fornecer dependências a uma classe pelo exterior (construtor) em vez de as criar internamente. Crucial para testes.
  - **Exemplo:** Em vez de `final _api = ApiService();` dentro da classe, faz-se `final ApiService _api; UserRepository(this._api);`. Isto permite passar um `MockApiService` nos testes.

- **Pedidos Assíncronos (`async`/`await`):**
  - Permite que operações longas (rede) não bloqueiem a UI. `await` pausa a função `async` atual, libertando o *thread* principal.
    ```dart
    Future<void> fetchData() async {
      // UI não fica bloqueada aqui
      final response = await http.get(Uri.parse(...)); 
      // Esta linha só executa após o get() terminar
      final data = jsonDecode(response.body);
    }
    ```

- **Testes de Widget vs. Integração:**
  - **Widget:** Testa um widget isolado (`await tester.pumpWidget(MeuWidget())`). Rápido, sem emulador.
  - **Integração:** Testa a app inteira (`await tester.pumpAndSettle()`). Lento, com emulador, simula fluxos completos.

### B) Lógica de Programação (Widget de Contador Completo)

O desafio é preencher os espaços para criar um contador funcional.

**Código Completo (Solução):**
```dart
// 1. Tem de ser StatefulWidget para gerir o estado (_counter)
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  // 2. Declaração da variável final precisa de ponto e vírgula
  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    // 3. setState notifica o Flutter para reconstruir o widget
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text(widget.title)),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('You have pushed the button this many times:'),
            // 4. Interpolação de string para mostrar o valor
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        // 5. Passar a referência da função para o callback onPressed
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

## Parte 4: Mega-Resumo de Computação Móvel (com exemplos)

### Arquiteturas de Desenvolvimento

- **Nativa Pura:** Máximo desempenho. (Ex: App `Mail` do iOS, `Telefone` do Android).
- **Híbrida-Nativa (Flutter):** Melhor compromisso. Código único (Dart), UI consistente, alta performance.
- **Híbrida-Nativa (React Native):** Código único (JS), mas depende de uma "ponte" para a UI nativa, o que pode ser um gargalo.
- **Híbrida-Web:** Site numa `WebView`. (Ex: Muitas apps de bancos antigas).
- **PWA:** Site "instalável" com capacidades offline via `Service Worker`.

### Modelos de Navegação e Estado

- **Passagem de Dados (Navegação):**
  ```dart
  // Passar um argumento para o próximo ecrã
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => DetailScreen(itemId: '123', origin: 'lista')),
  );
  ```
- **Estado Persistente (Local):** `shared_preferences`
  ```dart
  Future<void> saveUserPreference(String key, bool value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool(key, value);
  }

  Future<bool> readUserPreference(String key) async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getBool(key) ?? false; // Retorna false se não existir
  }
  ```
- **Layouts Complexos:**
  - `Row` para horizontal, `Column` para vertical.
  - `Expanded` para um filho preencher o espaço restante.
  - `Padding` para espaçamento interno, `SizedBox(width: 10)` para espaçamento externo fixo.
  - `Stack` para sobrepor widgets.

### Usabilidade e Interação

- **Thumb Zone:** Botões principais em baixo.
- **Dedo Gordo:** Alvos de toque com `48dp` no mínimo.
- **Feedback ao Utilizador:** `SnackBar`
  ```dart
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text('Avaliação guardada!')),
  );
  ```

### Conectividade e Dados

- **Padrão Repositório (Exemplo):**
  ```dart
  // Contrato
  abstract class ThingRepository {
    Future<Thing> getThing();
  }

  // Implementação real (usa a rede)
  class ApiThingRepository implements ThingRepository {
    Future<Thing> getThing() async { /* ... lógica http ... */ }
  }
  
  // Implementação para testes (não usa a rede)
  class MockThingRepository implements ThingRepository {
    Future<Thing> getThing() async => Thing(name: 'Mock Thing');
  }
  ```
- **Offline-First (Verificar Conectividade):**
  ```dart
  import 'package:connectivity_plus/connectivity_plus.dart';
  
  final connectivityResult = await (Connectivity().checkConnectivity());
  if (connectivityResult == ConnectivityResult.none) {
    // Estou offline, carregar da cache
  } else {
    // Estou online, ir à API
  }
  ```
- **Ponto de Atenção (Lógica de Negócio):** O repositório é o local ideal para centralizar a lógica de negócio, como **fundir dados de múltiplas fontes** e **filtrar** a lista final antes de a entregar à UI.

### Autonomia (Gestão de Bateria)

- **Otimizar Rede:** Agrupar (`batching`) pedidos.
- **Otimizar GPS:** Usar `LocationAccuracy.low` sempre que possível.
- **Processamento em Background (agendado):** `workmanager`
  ```dart
  Workmanager().registerPeriodicTask(
    "1", "tarefaPeriodica",
    frequency: Duration(hours: 1),
    constraints: Constraints(networkType: NetworkType.unmetered),
  );
  ```

### Sensores e Contexto

- **Geolocalização (Pedir Permissão):**
  ```dart
  import 'package:geolocator/geolocator.dart';

  Future<void> _handlePermission() async {
    LocationPermission permission = await Geolocator.checkPermission();
    if (permission == LocationPermission.denied) {
      permission = await Geolocator.requestPermission();
    }
    if (permission == LocationPermission.deniedForever) {
      // O utilizador negou para sempre. Mostrar diálogo para ir às definições.
      await Geolocator.openAppSettings();
    }
  }
  ```
- **Consumir Sensores:** Usar `StreamBuilder` para que a UI se atualize com os novos dados do sensor.

### Serviços Externos e APIs

- **REST:** `GET` para ler, `POST` para escrever, usando `JSON`.
- **Tokens:** **API Token** (autentica a app), **Access Token** (autentica o utilizador). Enviado no `Header`.
  `headers: {'Authorization': 'Bearer $accessToken'}`

### Modelos de Negócio

- **Custos:** App Store ($99/ano), Google Play ($25/uma vez). Comissão de 15-30%.
- **Modelos:** Anúncios (requer escala), Paga (requer reputação), Freemium (mais comum), Subscrição (requer valor contínuo).

---

## Anexo: Cábula Rápida Kotlin -> Dart

| Conceito | Kotlin | Dart | Notas |
|:---|:---|:---|:---|
| **Variáveis Imutáveis** | `val x = 10` | `final int x = 10;` | `const` em Dart é para tempo de compilação. |
| **Nulabilidade** | `String? nome` | `String? nome;` | Similar. |
| **Safe Call** | `nome?.length` | `nome?.length;` | Idêntico. |
| **Elvis Operator** | `nome ?: "Default"` | `nome ?? "Default"` | `?:` vira `??`. |
| **Função (Lambda)** | `(Int, Int) -> a + b` | `(int a, int b) => a + b;` | Usa `=>`. |
| **Callbacks em Setters** | `set(v) { field=v; f(v) }` | `set a(v) { _a=v; f(v); }` | Sintaxe diferente. |
| **Listas** | `listOf(1, 2)` | `[1, 2]` | Sintaxe literal. |
| **Mapas** | `mapOf("a" to 1)` | `{"a": 1}` | Sintaxe JSON-like. | 