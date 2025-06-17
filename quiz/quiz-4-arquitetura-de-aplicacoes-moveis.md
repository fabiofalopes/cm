# Quiz #4 - Arquitetura de aplicações móveis

### Pergunta 1

**Arquitetura de aplicações Android**

A estrutura de uma aplicação Android é fortemente orientada a objetos. Todos os ecrãs são [ ... ] de classes que herdam de [ ... ] que, por sua vez, herda de [ ... ]. Além de relações de herança, as activities criadas pelo programador têm relações de [ ... ] com classes relativas aos componentes gráficos. Todas essas classes herdam da classe [ ... ].

**Arquitetura de aplicações móveis**

Uma das arquiteturas mais usadas no desenvolvimento de aplicações móveis é o MVC, em que o M vem de [ ... ], o V de [ ... ] e o C de [ ... ]. A vantagem desta arquitetura é que permite separar responsabilidades dentro da aplicação, facilitando a sua [ ... ]. O "C" é responsável pelo tratamento de [ ... ] e por garantir a comunicação entre o "M" e o "V" pois o "M" e o "V" [ ... ] falam diretamente um com o outro. Uma outra vantagem do MVC é que é mais fácil [ ... ] o "M" programaticamente.

**Modelos de programação**

Ao contrário da programação [ ... ], na programação por [ ... ], o programa está numa espécie de ciclo [ ... ], à espera de eventos, resultantes da interação com os componentes gráficos do programa. É possível ter os dois modelos em simultâneo através de [ ... ] (uma palavra, no plural, em inglês), que são fios de execução independentes. O fio lançado pela função main() chama-se [ ... ] (2 palavras, capitalizadas) enquanto a parte gráfica é executada na [ ... ] (2 palavras, capitalizadas).

Os [ ... ] resultantes da interação com a aplicação são tratados por funções. Em Kotlin, é possível passar funções por parâmetro para outras funções.

---

Por exemplo, neste pedaço de código, a função calcula recebe uma função f. A função f, recebe 2 parâmetros do tipo inteiro e retorna um inteiro.

```kotlin
fun calcula(f: ???) {
    ...
}
```

O que colocarias no lugar dos ???: [ ... ]

---

Imaginando agora que tinhas uma função soma e querias chamar, no main, a função calcula passando-lhe como parâmetro a função soma:

```kotlin
fun calcula(...) {
    ...
}

fun soma(num1: Int, num2: Int) = num1 + num2

fun main() {
    calcula(??????)
}
```

O que colocarias no lugar dos ???: [ ... ]

---

E se agora não quisesses estar a criar uma função soma, e lhe passasses apenas um lambda:

```kotlin
fun calcula(...) {
    ...
}

fun main() {
    calcula { ??lambda?? }
}
```

Que lambda colocarias no lugar do ??lambda?? : [ ... ]
Nota: não é preciso colocar as chavetas; usa as variáveis n1 e n2; não coloques espaços 