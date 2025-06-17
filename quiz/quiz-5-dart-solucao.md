# Quiz #5 - Dart - Solução

### Pergunta 1

O Dart é uma linguagem multi-plataforma que combina rapidez de **desenvolvimento** graças ao JIT Compiler com rapidez de **execução** graças ao AOT Compiler. O primeiro permite que as alterações ao código sejam imediatamente refletidas na aplicação, uma técnica chamada (2 palavras): **Hot Reload**.

Que linha de código escreverias em Dart para escrever no ecrã a concatenação das variáveis nome e apelido, com um espaço no meio:
**print("$nome $apelido");**

Que linha de código escreverias em Dart para declarar e inicializar uma variável nomes (lista) com as Strings "Computação" e "Móvel"
**var nomes = ["Computação", "Móvel"];**

Nesta classe, completa o ???? com o construtor usando "named" arguments:

```dart
class Aluno {
    String nome;
    int idade;
    String? morada;
    ???
}
```
**Aluno({required this.nome, required this.idade, this.morada});**

Transforma a seguinte função num lambda, sem usar tipos explícitos:

```dart
bool maior(int n1, int n2) {
    return n1 < n2;
}
```
**(n1, n2) => n1 < n2;**

Qual o output do seguinte programa?

```dart
var valores = { '1': 'Portugal', '2': 'Brasil', '3': 'Angola' };
print(valores['2']);
print(valores['Portugal']);
print(valores['3'] ?? 'Indefinido');
print(valores['4'] ?? 'Indefinido');
```

Linha 1: **Brasil**
Linha 2: **null**
Linha 3: **Angola**
Linha 4: **Indefinido** 