# O que aprendemos este semestre
---
# O que aprendemos este semestre

## Faceta “conceptual”

*   Computação Móvel / Sistemas Ubíquos
*   Arquitetura e desenvolvimento de aplicações móveis
    *   Web
    *   Híbrida-Web, Híbrida-Nativa
    *   Nativa
*   Usabilidade e Interação
*   Conectividade
*   Geo-localização
*   Autonomia
*   Sensores
*   Integração com serviços externos
*   Modelos de negócio

## Faceta “prática”

*   Arquitetura de aplicações móveis
    *   Separação UI/Lógica de Negócio
    *   Programação de widgets
    *   Gestão de estado
    *   Testes unitários / integração
    *   Injeção de dependências
    *   Programação assíncrona
    *   Padrão repositório
---
# Exame

*   Dia 17 Junho, às 18h30
*   2 salas - a distribuição será publicada no Moodle
*   <u>Quem chegar atrasado não faz o exame</u>
---
# Exame

*   Perguntas de resposta aberta
*   Com consulta
    *   Podem levar uma única folha A4, manuscrita (não pode ser impressa nem fotocópia)
    *   Essa folha não pode conter código Dart nem excertos em JSON, apenas texto e diagramas

Isto também é válido para época de recurso e época especial
---
# Época de recurso / especial

* Obrigatória a inscrição no netpa (secretaria virtual) até 2 dias antes da prova
---
# Estrutura do exame

* Parte 1 - Formato JSON (2 valores)
* Parte 2 - Programação callbacks (2 valores)
* Parte 3 - Conceitos/programação flutter (4 valores)
* Parte 4 - Conceitos computação móvel (12 valores)
---
# Formato JSON

Converter esta mensagem XML para JSON

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
---
# Formato JSON

## Resolução

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
# Processamento callbacks

```dart
class Contadores {
  int _a = 0;
  int _b = 0;
  Function _f1, _f2;

  Contadores(this._f1, this._f2);

  set a(int value) {
    _a = value;
    _f1(_a);
  }

  set b(int value) {
    _b = value;
    _f2(_b);
  }
}

class Callbacks {
  int _x = 0;
  int _y = 0;

  void onX(int v) {
    _x += v;
  }

  void onY(int v) {
    _y = _x + v;
  }
}
```

```dart
void main() {
  Callbacks callbacks = Callbacks();

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

Qual o output deste programa?
---
# Processamento callbacks

```dart
class Contadores {
  int _a = 0;
  int _b = 0;
  Function _f1, _f2;

  Contadores(this._f1, this._f2);

  set a(int value) {
    _a = value;
    _f1(_a);
  }

  set b(int value) {
    _b = value;
    _f2(_b);
  }
}
```

```dart
class Callbacks {
  int _x = 0;
  int _y = 0;

  void onX(int v) {
    _x += v;
  }

  void onY(int v) {
    _y = _x + v;
  }
}
```

```dart
void main() {
  Callbacks callbacks = Callbacks();

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

## Resposta:
```
5
13
7
```
---
# Conceitos flutter
(perguntas exemplo)

- Quais as diferenças entre um StatelessWidget e um StatefulWidget? Em que casos queremos usar cada um deles? (máx. 50 palavras)
- Para que serve a “injeção de dependências”? (máx. 50 palavras)
- Os pedidos a APIs remotas devem ser assíncronos. O que é que isso significa? (máx. 50 palavras)
- Quais as diferenças entre testes de widget e testes de integração?
---
```dart
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
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text(widget.title),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text('Count:'),
          Text(' ??? 4 ??? '),
        ],
      ),
    ),
    floatingActionButton: FloatingActionButton(
      onPressed: ??? 5 ???,
      child: Icon(Icons.add),
    ),
  );
}
}
```

# Programação flutter
(pergunta exemplo)

> Preencha as caixas de forma a que este widget compile e tenha o comportamento correto
---
```dart
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() { _counter++; });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Count:'),
            Text('$_counter'),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

# Programação flutter
(pergunta exemplo)
---
# Conceitos computação móvel
(perguntas exemplo)

- Há quem diga que o carregamento sem fios é o futuro pois permitirá mais facilmente resolver problemas de compatibilidade e miniaturização. Explique esta frase (máx. 50 palavras)

- Segundo a wikipedia, a IoT (Internet of Things) é "um conceito que se refere à interconexão digital de objectos do dia a dia com a Internet. É a conexão dos objectos, mais do que as pessoas, à Internet.". Provavelmente as limitações dos dispositivos móveis que estudámos durante o semestre (smartphones, smartwatches, etc.) também existem, e em maior escala, nestes objectos. Que limitações são essas e de que forma estão ser ultrapassadas? (máx. 50 palavras)

- Observe o seguinte écran da aplicação XYZ. Acha que esta aplicação tira partido da computação móvel para resolver o problema de forma adequada? Justifique (a sua justificação deve incluir as palavras autonomia, geo-localização, usabilidade). (máx. 100 palavras)
---
# Ask Me Anything
---
# Tipos de empregadores
(onde trabalham ex-alunos da Lusófona)

## Serviços para terceiros
- Outsourcing (local, nearshore) - PrimeIT, agap2, Randstad
- Consultoria tecnológica - CGI, Xpand IT, Link, Celfocus, NTT Data, Noesis
- Consultoria de negócio - Accenture, Deloitte, KPMG, CapGemini

## Corporate
- BNP Paribas, Banco de Portugal, Santander, BBVA, Vila Galé Hoteis (departamento de IT)

## Desenvolvimento de produtos
- Miniclip, MAN Digital Hub, Critical Techworks, Innowave, Siemens, Sky, OroraTech, Sensei, Edisoft, Digitalis

## Ex-alunos que criaram a sua própria empresa
---
# Tipos de empregadores
(onde trabalham ex-alunos da Lusófona)

## Serviços para terceiros
- Outsourcing (local, nearshore) - PrimeIT, agap2, Randstad
- Consultoria tecnológica - CGI, Xpand IT, Link, Celfocus, NTT Data, Noesis
- Consultoria de negócio - Accenture, Deloitte, KPMG, CapGemini

## Corporate
BNP Paribas, Banco de Portugal, Santander, BBVA, Vila Galé Hoteis (departamento de IT)

## Desenvolvimento de produtos
Miniclip, MAN Digital Hub, Critical Techworks, Innowave, Siemens, Sky, OroraTech, Sensei, Edisoft, Digitalis, Siscog, Malwarebytes

## Ex-alunos que criaram a sua própria empresa
The Scoring Company, Cobuntu

Nota: Esta lista não é exaustiva, há muitas empresas com ex-alunos Lusófona
---
# Dimensão dos empregadores

| notequal consulting, endlessloop, ... |                         | XPand It, Link, Novabase   |                          |
| ------------------------------------- | ----------------------- | -------------------------- | ------------------------ |
| startups (< 50)                       | PME (50 - 500)          | Grandes empresas nacionais | Grandes multi-nacionais  |
|                                       | Innowave, Miniclip, ... |                            | CGI, Accenture, Deloitte |

---
# Estado do IT em Portugal

Estudo conduzido pela landing.jobs com base em inquérito a profissionais de IT em Portugal

Número de respostas: 1516
(entre Dez 2024 e Março 2025)
---
# Qualificações

| Category                          | Approximate Percentage |
| --------------------------------- | ---------------------- |
| Doctoral degree                   | \~1%                   |
| Masters degree                    | \~44%                  |
| Bachelor degree                   | \~36%                  |
| Technical bootcamp                | \~3%                   |
| Self-taught                       | \~2%                   |
| High school / Professional school | \~12%                  |


Há quase tantos profissionais de IT com licenciatura como com mestrado

© Pedro Alves 2025
---
# Tipo de atividade

| Tipo de atividade                  | Percentagem |
| ---------------------------------- | ----------- |
| Full-Stack Developer               | \~21%       |
| Back-End Developer                 | \~20.5%     |
| Front-End Developer                | \~8%        |
| Data Scientist/Data Engineer       | \~8.5%      |
| UX/UI Designer                     | \~9%        |
| Quality Assurance/Testing          | \~6%        |
| DevOps Engineer                    | \~6.5%      |
| Solutions Architect                | \~4%        |
| SysAdmin Engineer                  | \~3.5%      |
| Mobile Apps Developer              | \~4.5%      |
| Business Applications (BI/CRM/ERP) | \~3%        |
| Computer & Network Security        | \~2.5%      |
| Maintenance & Support              | \~2%        |
| Blockchain/Web3 Developer          | \~0.5%      |

---
# Local de trabalho

## Remote vs Office

| **50%**<br/>full remote | **44%**<br/>hybrid | **6%**<br/>full office |
| ----------------------- | ------------------ | ---------------------- |


Full-remote a ganhar força, desde o COVID
---
# Motivação

|                                    | Percentage |
| ---------------------------------- | ---------- |
| Salary & benefits                  | 22%        |
| Work-life balance                  | 19%        |
| Career progression                 | 11%        |
| Technological challenge            | 10%        |
| Cultural fit with company and team | 9%         |
| Professional stability             | 8%         |
| Schedule flexibility               | 7%         |
| Learning & training                | 6%         |
| Impact of my work in society       | 5%         |
| Recognition and status             | 3%         |

---
# Quanto tempo na mesma empresa?

| Category            | Less than 6 months (approx. %) | Between 6 months and 1 year (approx. %) | 1 to 2 years (approx. %) | 2 to 4 years (approx. %) | 5 to 10 years (approx. %) | More than 10 years (approx. %) | Average time in current company |
| ------------------- | ------------------------------ | --------------------------------------- | ------------------------ | ------------------------ | ------------------------- | ------------------------------ | ------------------------------- |
| Between 1 - 3 years | \~8%                           | \~17%                                   | \~25%                    | \~40%                    | \~7%                      | \~3%                           | Avg. 2.2 years                  |
| Between 3 - 6 years | \~7%                           | \~15%                                   | \~23%                    | \~30%                    | \~20%                     | \~5%                           | Avg. 2.6 years                  |
| Between 6 - 9 years | \~6%                           | \~12%                                   | \~17%                    | \~25%                    | \~30%                     | \~10%                          | Avg. 3.6 years                  |
| More than 9 years   | \~5%                           | \~10%                                   | \~15%                    | \~20%                    | \~25%                     | \~25%                          | Avg. 4.4 years                  |

---
# Evolução salarial

|                        | Less than 3 years | 3 to 6 years | More than 6 years | Total average |
| ---------------------- | ----------------- | ------------ | ----------------- | ------------- |
| Tech development roles | \~28,000€         | \~42,000€    | \~54,000€         | \~49,000€     |
| Tech management roles  | \~27,000€         | \~41,000€    | \~66,000€         | \~62,000€     |


<div style="display: flex; align-items: center; margin-top: 10px;">
  <div style="width: 15px; height: 15px; background-color: #28B2A8; margin-right: 5px; border-radius: 50%;"></div>
  <span style="margin-right: 20px;">Tech development roles</span>
  <div style="width: 15px; height: 15px; background-color: #2077F2; margin-right: 5px; border-radius: 50%;"></div>
  <span>Tech management roles</span>
</div>

salários médios brutos
---
Relatório completo

https://campaign.landing.jobs/hubfs/Tech%20Talent%20Trends%20Report%202025.pdf