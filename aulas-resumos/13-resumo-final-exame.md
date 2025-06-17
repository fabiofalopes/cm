# Guia de Estudo Final: Exame de Computação Móvel

Este guia consolida toda a matéria, seguindo a estrutura e os exemplos da aula de revisão.

## Informações Cruciais sobre o Exame

- **Formato:** Perguntas de resposta aberta.
- **Consulta:** É permitida uma **única folha A4, manuscrita** (frente e verso). Não são permitidas impressões ou fotocópias.
- **Restrição da Folha de Consulta:** A folha **não pode conter código Dart nem excertos JSON**. Apenas texto e diagramas.

### Estrutura e Pontuação
- **Parte 1:** Formato JSON (2 valores)
- **Parte 2:** Programação com Callbacks (2 valores)
- **Parte 3:** Conceitos e Programação Flutter (4 valores)
- **Parte 4:** Conceitos de Computação Móvel (12 valores)

---

## Parte 1: Formato JSON (2 valores)

**Objetivo:** Converter uma estrutura de dados de XML para JSON.

**Exemplo da Aula:**
*   **XML Original:**
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

*   **JSON Equivalente (Solução):**
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
**Lógica de Mapeamento:**
- Tags aninhadas (`<response>`, `<body>`) tornam-se objetos JSON (`{}`).
- Tags com o mesmo nome dentro de outra (vários `<movie>` ou `<actor>`) tornam-se uma lista (`[]`) de objetos.
- Atributos de uma tag (`name`, `year`, `rating`) tornam-se pares `chave: valor` dentro do objeto.
- Conteúdo de uma tag (`<code>Success</code>`) torna-se um par `chave: valor`.

---

## Parte 2: Programação com Callbacks (2 valores)

**Objetivo:** Analisar código Dart que usa callbacks e determinar o seu output. A chave é seguir o fluxo de execução e manter o registo do estado das variáveis.

**Exemplo da Aula:**
```dart
// Classes (Definições)
class Contadores {
  int _a = 0, _b = 0;
  Function _f1, _f2;
  Contadores(this._f1, this._f2);
  set a(int value) { _a = value; _f1(_a); }
  set b(int value) { _b = value; _f2(_b); }
}

class Callbacks {
  int _x = 0, _y = 0;
  void onX(int v) { _x += v; }
  void onY(int v) { _y = _x + v; }
}

// Execução
void main() {
  Callbacks callbacks = Callbacks(); // Estado inicial: _x = 0, _y = 0
  Contadores contadores1 = Contadores(callbacks.onX, callbacks.onY);
  Contadores contadores2 = Contadores(callbacks.onX, (x) => print(x));

  contadores1.a = 3;   // 1. Chama callbacks.onX(3).  => _x passa a 0 + 3 = 3.
  contadores1.b = 4;   // 2. Chama callbacks.onY(4).  => _y passa a _x(3) + 4 = 7.
  contadores2.a = 10;  // 3. Chama callbacks.onX(10). => _x passa a 3 + 10 = 13.
  contadores2.b = 5;   // 4. Chama print(5).          => Output: 5

  print(callbacks._x); // Output: 13
  print(callbacks._y); // Output: 7
}
```
**Output Final Esperado:**
```
5
13
7
```

---

## Parte 3: Conceitos e Programação Flutter (4 valores)

### A) Conceitos (Respostas Curtas)

- **StatelessWidget vs. StatefulWidget:**
  `StatelessWidget` é para UI estática, imutável, que não muda com a interação (ex: ícones, texto fixo). `StatefulWidget` é para UI dinâmica; o seu estado pode mudar. A chamada a `setState()` notifica o framework para reconstruir o widget com os novos valores de estado (ex: contador, formulário).

- **Injeção de Dependências (DI):**
  É uma técnica para fornecer as dependências (objetos necessários) a uma classe pelo exterior (ex: via construtor), em vez de ela as criar internamente. Isto desacopla o código, tornando-o flexível e, crucialmente, testável, pois permite substituir dependências reais por `mocks` durante os testes.

- **Pedidos Assíncronos (`async`/`await`):**
  Significa que a app não bloqueia a UI à espera de uma operação demorada (ex: pedido de rede). O `await` pausa a execução da função *assíncrona* até o `Future` completar, mas liberta o "thread" principal para que a app continue a responder ao utilizador.

- **Testes de Widget vs. Testes de Integração:**
  **Widget:** Testa um único widget isoladamente. É rápido, não requer emulador e verifica a UI e a interação de um componente específico.
  **Integração:** Testa um fluxo completo da app (end-to-end). É lento, precisa de um emulador/dispositivo real e valida a integração entre vários widgets, serviços e a performance geral.

### B) Programação (Preencher os Espaços)

**Exemplo da Aula:**
```dart
// Widget por completar
class MyHomePage extends ??? 1 ??? {
  const MyHomePage({super.key, required this.title});
  final String ??? 2 ???
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;
  void _incrementCounter() {
    ??? 3 ??? (() { _counter++; });
  }
  @override
  Widget build(BuildContext context) { /* ... */ 
    /* ... */ Text(' ??? 4 ??? '), /* ... */
    /* ... */ onPressed: ??? 5 ???, /* ... */
  }
}
```
**Solução:**
1.  **`StatefulWidget`**: O widget tem estado (`_counter`) que muda.
2.  **`title;`**: A declaração da variável `title` precisa de um ponto e vírgula.
3.  **`setState`**: É a função que se chama para notificar o Flutter que o estado mudou e a UI precisa de ser reconstruída.
4.  **`'$_counter'`**: Interpolação de strings para mostrar o valor da variável `_counter`.
5.  **`_incrementCounter`**: Passa a referência da função a ser executada no `onPressed`.

---

## Parte 4: Mega-Resumo de Computação Móvel (12 valores)

Esta secção agrega os conceitos mais importantes de todas as aulas, focados em perguntas de desenvolvimento e justificação.

### Arquiteturas de Desenvolvimento
- **Nativa Pura:** Máximo desempenho e acesso a APIs. Custo elevado (código separado para iOS/Android).
- **Híbrida-Nativa (Flutter):** Base de código única (Dart). Excelente desempenho (compilado para nativo) e UI consistente. Acesso a APIs via plugins. **O melhor compromisso para a maioria das apps.**
- **Híbrida-Web (Ionic/Cordova):** Essencialmente um site dentro de uma `WebView`. Desempenho mais fraco, acesso limitado a APIs. Mais barato, mas a experiência do utilizador é inferior.
- **PWA (Progressive Web App):** Um site que "se comporta" como uma app (manifest, service worker para offline, pode ser "instalado" no ecrã principal). Não passa pelas stores.

### Usabilidade e Interação
- **Thumb Zone (Zona do Polegar):** As ações principais e a navegação devem estar na parte inferior do ecrã, facilmente alcançáveis com uma mão.
- **Problema do "Dedo Gordo":** Os alvos de toque (botões, ícones) devem ter no mínimo **48dp** (cerca de 9mm) para serem fáceis de usar, mesmo que o ícone visível seja menor.
- **Layouts Responsivos:** Usar `Column`, `Row`, `Expanded` e `MediaQuery` para garantir que a UI se adapta bem a diferentes tamanhos de ecrã e orientações.

### Conectividade e Dados
- **Padrão Repositório:** Essencial. Cria uma camada de abstração entre a UI e as fontes de dados (`DataSource`). A UI pede dados ao repositório, que decide se os vai buscar a uma **API remota** ou a uma **cache local** (BD/SharedPreferences). Desacopla o código e facilita os testes e a implementação de lógica offline.
- **Offline-First:** A app deve ser funcional mesmo sem internet. A UI deve carregar dados da cache local primeiro e só depois (ou em background) tentar sincronizar com a rede.

### Autonomia (Gestão de Bateria)
- **Otimizar a Rede:** O rádio de rede é um grande consumidor. **Agrupar (`batching`)** vários pedidos pequenos num único pedido maior é a melhor estratégia para permitir que o rádio "durma" por mais tempo.
- **Otimizar GPS:** A geolocalização consome muita bateria. Pedir sempre a **menor precisão (`LocationAccuracy`)** aceitável para a tarefa e **desligar o sensor (`stream.cancel()`)** assim que a localização for obtida.
- **Processamento em Background:** É **fortemente restringido pelo SO**. Para tarefas periódicas não urgentes (ex: sincronização), usar o plugin `workmanager` para **agendar** a tarefa. O SO decidirá o melhor momento para a executar, otimizando pela bateria do sistema (e.g., **Modo Doze**).

### Sensores e Contexto
- **Geolocalização:** Requer **permissão explícita** do utilizador, que deve ser gerida no código (pedir, verificar estado).
- **Tipos de Sensores:** Físicos (acelerómetro, giroscópio), Lógicos/Virtuais (detetor de passo, que combina dados de vários sensores físicos) e Biométricos (ritmo cardíaco).

### Serviços Externos e APIs
- **REST:** Um estilo de arquitetura para desenhar APIs. Usa os verbos HTTP (`GET`, `POST`, `PUT`, `DELETE`) para operações em recursos, que são identificados por **Endpoints** (URLs).
- **Tokens:** `Access Tokens` (tipicamente JWT) são usados para autenticar pedidos a endpoints protegidos. São obtidos após o login e enviados no cabeçalho (`Header`) de cada pedido.

### Modelos de Negócio
- **Custos:** Publicar na **App Store custa $99/ano**; na **Google Play custa $25 (pagamento único)**. Ambas ficam com uma comissão de **15-30%** sobre as vendas.
- **Modelos:**
    - **Anúncios:** Requer muitos utilizadores/tempo de uso.
    - **Paga:** Difícil de vender sem reputação prévia.
    - **Freemium:** Grátis para usar, pagar por extras (o mais comum).
    - **Subscrição:** Exige valor contínuo; gera receita recorrente.

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
| **Listas** | `listOf(1, 2)` | `[1, 2]` | Sintaxe mais simples em Dart. |
| **Mapas** | `mapOf("a" to 1)` | `{"a": 1}` | Sintaxe JSON-like em Dart. | 