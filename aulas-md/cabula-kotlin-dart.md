# Cábula Kotlin-Dart

As diferenças entre o Kotlin e o Dart são principalmente de teor sintático, sendo a conversão de uma para outra relativamente linear. Abaixo apresenta-se uma tabela que permite, de forma sumarizada, perceber quais as primitivas da linguagem Dart que suportam os mecanismos que foram lecionados para a linguagem Kotlin.

## Estrutura do programa

| Kotlin                     | Dart                          | Observações                                                                                     |
|---------------------------|-------------------------------|-------------------------------------------------------------------------------------------------|
| (ficheiro .kts)           | (ficheiro .dart)              | Em Dart é obrigatório declarar uma função main. Em Kotlin, apenas é obrigatório declarar a função main se o ficheiro for .kt. |
| Estrutura livre           | `void main() {`               | Em Dart, os nomes dos ficheiros .dart não têm restrições, no entanto, costuma usar-se snake_case em vez de CamelCase como no Kotlin. |
| (ficheiro .kt)           | `}` ...                       |                                                                                                 |
| `fun main(){`            |                               |                                                                                                 |
| `...`                     |                               |                                                                                                 |
| `numero = 3`             | `numero = 3;`                 | Em Dart, as linhas têm que terminar com `;` (ponto e vírgula).                                |

## Declaração de variáveis

| Kotlin                                   | Dart                                   | Observações                                                                                     | | | |
|------------------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------|---|---|---|
| `var numero : Int = 10`                  | `int numero = 10;` (tipo explícito)  | Em Dart podemos declarar variáveis com tipo implícito ou explícito.                           | | | |
|                                          | `var numero = 10;` (tipo implícito)   | Nem todos os tipos estão disponíveis:                                                          | | | |
|                                          |                                        |                                                                                                 | | | |
|                                          |                                        | | Kotlin | Dart |                                                                                 |
|                                          |                                        | |--------|------|                                                                                 |
|                                          |                                        | | Byte   | Não existe |                                                                              |
|                                          |                                        | | Short  | Não existe |                                                                              |
|                                          |                                        | | Int    | int      |                                                                              |
|                                          |                                        | | Long   | não existe |                                                                              |
|                                          |                                        | | Float  | não existe |                                                                              |
|                                          |                                        | | Double | double   |                                                                              |
|                                          |                                        | | Char   | não existe |                                                                              |
|                                          |                                        | | String | String   |                                                                              |
|                                          |                                        | | Boolean | bool    |                                                                              |
| `não existe; o kotlin é fortemente tipificado` | `dynamic coisa = 10;` // neste momento é inteiro | Em Dart é possível mudar o tipo das variáveis. Deve ser usado com cuidado.                   | | | |
|                                          | `coisa = 'ola';` // agora passou a ser string |                                                                                                 | | | |
| `var numero : Int (erro!!)`              | `int numero; (erro !!)`               | Tal como no Kotlin é obrigatório inicializar todas as variáveis em Dart.                      | | | |
| `var numero : Int = 10` // mutável       | `int numero = 10;` // mutável         | Em Dart, usa-se o `const` e o `final` para indicar que uma variável é imutável.              | | | |
| `val numero2 : Int = 11` // imutável     | `const int numero2 = 11;` // imutável | A diferença é que no `const`, o valor tem que ser conhecido em tempo de compilação, enquanto no `final` pode ser conhecido apenas em tempo de execução. | | | |

---
# Cheatsheet: Kotlin vs Dart

## Nullability

| Kotlin                                   | Dart                                   | Observações                                                                                     |
|------------------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------|
| `var numero : Int? = null`               | `int? numero = null;`                 | Tal como em Kotlin, todos os tipos podem ser nullable acrescentando um `?` à frente do tipo.   |
| `var numero2 : Double? = null`           | `double? numero2 = null;`             | As variáveis nullable são inicializadas por omissão com o valor `null`.                        |
| `var texto : String? = null`             | `String? texto = null;`               |                                                                                                 |
| `var resultado = numero!! + 3`           | `var resultado = numero! + 3;`        | Para se usarem variáveis que podem ser null, e se tivermos a certeza que não têm o valor null, podemos colocar o `!!` (Kotlin) ou `!` (Dart). |
| `var resultado = numero?.round()`        | `var resultado = numero?.round();`    | O safe operador `?` é igual em Kotlin e Dart.                                                 |
| `var resultado = numero ?: 0`            | `var resultado = numero ?? 0`         | O elvis operator em Dart é representado por `??`.                                             |

## Conversão de tipos

| Kotlin                                   | Dart                                   | Observações                                                                                     |
|------------------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------|
| `var numero : Int = 3.4.toInt()`         | `var numero = 3.4.toInt();`           | Igual nas duas linguagens.                                                                      |
| `var caracter : Char = 74.toChar()`     | `// não existe char`                   |                                                                                                 |
| `var numero : Int = "34".toInt()`       | `int numero = int.parse("34");`       | Em Dart, não existem primitivas `toInt()` e `toDouble()`. Para converter Strings para outros tipos existem primitivas `int.parse()` e `double.parse()`. |
| `var numero2 : Double = "34.5".toDouble()` | `double numero2 = double.parse("34.5");` |                                                                                                 |

## Operações com Strings

| Kotlin                                   | Dart                                   | Observações                                                                                     |
|------------------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------|
| `var texto = "Olá mundo"`                | `var texto = "Olá mundo";`            | Neste aspeto, o Kotlin e o Dart são praticamente iguais, exceptuando poder-se representar Strings com aspas simples em Dart. |
|                                          | `var texto = 'Olá mundo';`            |                                                                                                 |
| `var c = texto[4] // letra 'm'`         | `var c = texto[4] // letra 'm'`      |                                                                                                 |
| `var tamanho = texto.length`             | `var tamanho = texto.length();`       |                                                                                                 |

## Arrays, Listas e Maps

| Kotlin                                   | Dart                                   | Observações                                                                                     |
|------------------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------|
| `var numeros : Array<Int> = arrayOf(3, 6, 7)` | `não existe`                          | Em Dart, não existem arrays no sentido "clássico" - estruturas que têm que ser pré-alocadas com um certo tamanho e que não podem crescer posteriormente. Em vez disso, usam-se listas. |
| `var numeros : List<Int> = listOf(3, 6, 7)` | `List<int> numeros = [3, 6, 7];`     | A sintaxe para inicializar listas é mais compacta em Dart, basta colocar os elementos entre colchetes. |
| `var numeros = listOf(3, 6, 7)`         | `var numeros = [3, 6, 7];`           | A sintaxe para aceder aos elementos de uma lista é idêntica.                                   |
| `println(numeros[1])  // escreve 6`     | `print(numeros[1]); // escreve 6`    |                                                                                                 |
| `println(numeros.size) // escreve 3`    | `print(numeros.length) // escreve 3` |                                                                                                 |
| `var idadesPorNome: Map<String,Int> = mapOf("Pedro" to 40, "Sara" to 16)` | `Map<String,int> idadesPorNome = {"Pedro": 40, "Sara": 16};` | Os mapas/dicionários são representados pelo tipo `Map` em ambas as linguagens. No entanto, a forma de inicializar é mais compacta em Dart, com uma sintaxe similar ao Javascript (JSON). |
| `println(idadesPorNome["Pedro"])`       | `print(idadesPorNome["Pedro"]);`     | A forma de obter um valor a partir de uma chave é igual nas duas linguagens.                   |

---
# Kotlin vs Dart Cheatsheet

## Basic Output

| Kotlin                             | Dart                               | Observações                                                                                     |
|------------------------------------|------------------------------------|-------------------------------------------------------------------------------------------------|
| `println("olá")`                   | `print("olá");`                    | Em Dart, as Strings podem estar dentro de plicas ou de aspas.                                   |
|                                    | `print('olá');`                    | O print do Dart termina com uma quebra de linha. Para um print sem quebra de linha, use `stdout.write(...)`. |
| `println("numero = $numero")`      | `print("numero = $numero")`        | Para incluir variáveis dentro das Strings, o sistema é o mesmo.                                |
| `println("numero = ${numero}")`    | `print("numero = ${numero}")`      |                                                                                                 |

## Estruturas de Controle - Seleção

| Kotlin                                                    | Dart                                                    | Observações                                                                                     | | | | |
|-----------------------------------------------------------|---------------------------------------------------------|-------------------------------------------------------------------------------------------------|---|---|---|---|
| `if (numero >= 10) {`                                    | `if (numero >= 10) {`                                   | Sintaxe igual, tirando os ponto e vírgula.                                                     | | | | |
| `    soma += numero`                                     | `    soma += numero;`                                   |                                                                                                 | | | | |
| `} else {`                                               | `} else {`                                             |                                                                                                 | | | | |
| `    soma = 10`                                         | `    soma = 10;`                                       |                                                                                                 | | | | |
| `}`                                                     | `}`                                                   |                                                                                                 | | | | |
| `if (numero in 1..10) {`                                 | `if (numero >= 1 && numero <= 10) {`                  | Em Dart, não existe o operador `in`.                                                            | | | | |
| `    println("numero entre 1 e 10")`                     | `    print("numero entre 1 e 10");`                    |                                                                                                 | | | | |
| `}`                                                     | `}`                                                   |                                                                                                 | | | | |
| `var positivo : Boolean = if (numero < 0) false else true` | `boolean positivo = numero < 0 ? false : true;`      | Em Dart, existe o operador ternário, que usa `?` e `:` para construir uma espécie de if numa única linha. | | | | |
|                                                         |                                                         | `<variável> = <condição> ? <valor-caso-condicao-true> : <valor-caso-condicao-false>`         | | | | |
| `var texto1 : String = ...`                              | `String texto1 = ...;`                                 | Em Dart também se pode usar o operador `==` para comparar Strings.                             | | | | |
| `if (texto1 == "ola") {`                                 | `if (texto1 == "ola") {`                               |                                                                                                 | | | | |
| `    ...`                                               | `    ...`                                             |                                                                                                 | | | | |
| `}`                                                     | `}`                                                   |                                                                                                 | | | | |
| `var cor : String = ...`                                 | `String cor = ...;`                                    | Em Dart, o equivalente ao `when` é o `switch`.                                               | | | | |
| `when (cor) {`                                          | `switch (cor) {`                                       | Note-se que, ao contrário do C e do Java, não é necessário colocar um `break` no final de cada case. | | | | |
| `    "amarelo" -> println("amarelo")`                    | `    case "amarelo": print("amarelo");`                |                                                                                                 | | | | |
| `    "azul" -> println("azul")`                          | `    case "azul": print("azul");`                      |                                                                                                 | | | | |
| `}`                                                     | `} default: print("cor desconhecida");`               | Em vez do `default`, pode-se usar o `_`.                                                       | | | | |
| `var monocromatico = when (cor) {`                      | `bool? monocromatico = switch(cor) {`                 | Em Dart também é possível usar o `switch` como expressão.                                     | | | | |
| `    "amarelo", "azul", "vermelho" -> false`             | `    "amarelo" || "azul" || "vermelho" => false,`     |                                                                                                 |
| `    "preto", "branco" -> true`                           | `    "branco" || "preto" => true,`                    |                                                                                                 | | |
| `    else -> null`                                       | `    _ => null`                                        |                                                                                                 | | | | |
| `}`                                                     | `};`                                                  |                                                                                                 | | | | |

## Estruturas de Controle - Repetição

| Kotlin                          | Dart                              | Observações                                                                                     |
|---------------------------------|-----------------------------------|-------------------------------------------------------------------------------------------------|
| `var i = 0`                     | `int i = 0;`                      | Sintaxe igual, tirando os ponto e vírgula.                                                     |
| `while (i < 10) {`              | `while (i < 10) {`                |                                                                                                 |
| `    println(i)`                | `    print(i);`                   |                                                                                                 |
| `    i++`                       | `    i++;`                        |                                                                                                 |
| `}`                             | `}`                               |                                                                                                 |
| `var i = 0`                     | `int i = 0;`                      | Sintaxe igual, tirando os ponto e vírgula.                                                     |
| `do {`                          | `do {`                            |                                                                                                 |
| `    println(i)`                | `    print(i);`                   |                                                                                                 |
| `    i++`                       | `    i++;`                        |                                                                                                 |
| `} while (i < 10)`              | `} while (i < 10);`              |                                                                                                 |

---
# Kotlin vs Dart Cheatsheet

## Loops

| Kotlin Code                             | Dart Code                                   | Observations                                                                                     |
|-----------------------------------------|--------------------------------------------|--------------------------------------------------------------------------------------------------|
| ```kotlin                               | ```dart                                   | In Dart, there is no `in` operator or ranges. Therefore, the classic `for` loop must be used, |
| for (i in 1..10) {                      | for (var i = 1; i <= 10; i++) {          | similar to C, which has three parts separated by semicolons:                                   |
|     println(i)                          |     print(i);                             | `for (initialization; condition; increment)`                                                   |
| }                                       | }                                          | This type of loop does not exist in Kotlin.                                                     |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   |                                                                                                  |
| var numeros = arrayOf(2, 6, 7)          | var numeros = [2, 6, 7];                  | Very similar syntax. Note that Dart does not have arrays.                                       |
| for (numero in numeros) {               | for (var numero in numeros) {             | Alternatively, the classic `for` can be used (as explained above):                             |
|     println(numero)                     |     print(numero);                        | ```dart                                                                                          |
| }                                       | }                                          | for (var i = 0; i < numeros.length; i++) {                                                    |
|                                         |                                            |     print(numeros[i]);                                                                          |
|                                         |                                            | }                                                                                                |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | In Dart, it is not possible to iterate over a String directly; we must use the classic `for`   |
| var texto = "olá"                       | String texto = "olá";                     | loop to access characters one by one.                                                           |
| for (letra in texto) {                  | for (int i = 0; i < texto.length; i++) { |                                                                                                  |
|     println(letra)                      |     print(texto[i]);                      |                                                                                                  |
| }                                       | }                                          |                                                                                                  |

## Functions

| Kotlin Code                             | Dart Code                                   | Observations                                                                                     |
|-----------------------------------------|--------------------------------------------|--------------------------------------------------------------------------------------------------|
| ```kotlin                               | ```dart                                   | The difference in syntax reflects how variables are declared. Otherwise, they are similar.      |
| fun soma(num1: Int, num2: Int) : Int { | int soma(int num1, int num2) {           |                                                                                                  |
|     return num1 + num2                  |     return num1 + num2;                   |                                                                                                  |
| }                                       | }                                          |                                                                                                  |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | In Dart, functions that do not return anything must use the `void` type.                        |
| fun escreve(palavra: String) {         | void escreve(String palavra) {            |                                                                                                  |
|     println(palavra)                   |     print(palavra);                       |                                                                                                  |
| }                                       | }                                          |                                                                                                  |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | In Dart, square brackets `[]` are used to define default values for positional parameters.      |
| fun soma(num1: Int = 1, num2: Int = 2) : Int { | int soma([int numero1 = 1, int numero2 = 2]) { | For named parameters, it is slightly different, see below.                                     |
|     return num1 + num2                  |     return numero1 + numero2;             |                                                                                                  |
| }                                       | }                                          |                                                                                                  |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | The syntax for "one-liner" functions is similar. In Dart, they are called arrow functions.      |
| fun soma(num1: Int, num2: Int) = num1 + num2 | int soma(num1: Int, num2: Int) => num1 + num2; |                                                                                                  |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | In Dart, it is possible to define named parameters, which are referenced by name instead of position. |
| fun enableFlags(Boolean? bold, Boolean? hidden) {...} | void enableFlags({bool? bold, bool? hidden}) {...} | This allows changing the order of parameters using curly braces.                                |
| enableFlags(hidden = false, bold = true) | enableFlags(hidden: false, bold: true);   | In Kotlin, parameters are automatically named.                                                  |
|                                         |                                            |                                                                                                  |
| ```kotlin                               | ```dart                                   | With named parameters, it is possible to define default values.                                 |
| fun soma(num1: Int = 1, num2: Int = 2) : Int { | int soma({int numero1 = 3, int numero2 = 4}) { |                                                                                                  |
|     return num1 + num2                  |     return numero1 + numero2;             |                                                                                                  |
| }                                       | }                                          |                                                                                                  |
