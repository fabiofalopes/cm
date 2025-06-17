# Quiz #4 - Arquitetura de aplicações móveis - Solução

### Pergunta 1

**Arquitetura de aplicações Android**

A estrutura de uma aplicação Android é fortemente orientada a objetos. Todos os ecrãs são **instâncias** de classes que herdam de **Activity** que, por sua vez, herda de **Context**. Além de relações de herança, as activities criadas pelo programador têm relações de **composição** com classes relativas aos componentes gráficos. Todas essas classes herdam da classe **View**.

**Arquitetura de aplicações móveis**

Uma das arquiteturas mais usadas no desenvolvimento de aplicações móveis é o MVC, em que o M vem de **Model**, o V de **View** e o C de **Controller**. A vantagem desta arquitetura é que permite separar responsabilidades dentro da aplicação, facilitando a sua **manutenção**. O "C" é responsável pelo tratamento de **eventos** e por garantir a comunicação entre o "M" e o "V" pois o "M" e o "V" **não** falam diretamente um com o outro. Uma outra vantagem do MVC é que é mais fácil **testar** o "M" programaticamente.

**Modelos de programação**

Ao contrário da programação **imperativa**, na programação por **eventos**, o programa está numa espécie de ciclo **infinito**, à espera de eventos, resultantes da interação com os componentes gráficos do programa. É possível ter os dois modelos em simultâneo através de **threads** (uma palavra, no plural, em inglês), que são fios de execução independentes. O fio lançado pela função main() chama-se **Main Thread** (2 palavras, capitalizadas) enquanto a parte gráfica é executada na **UI Thread** (2 palavras, capitalizadas).

Os **eventos** resultantes da interação com a aplicação são tratados por funções. Em Kotlin, é possível passar funções por parâmetro para outras funções.

---

Por exemplo, neste pedaço de código, a função calcula recebe uma função f. A função f, recebe 2 parâmetros do tipo inteiro e retorna um inteiro.

```kotlin
fun calcula(f: ???) {
    ...
}
```

O que colocarias no lugar dos ???: **(Int, Int) -> Int**

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

O que colocarias no lugar dos ???: **::soma**

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

Que lambda colocarias no lugar do ??lambda?? : **n1,n2->n1+n2**
Nota: não é preciso colocar as chavetas; usa as variáveis n1 e n2; não coloques espaços 