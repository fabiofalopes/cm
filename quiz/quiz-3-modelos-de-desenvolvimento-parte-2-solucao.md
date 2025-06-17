# Quiz #3 - Modelos de Desenvolvimento (Parte 2) - Solução

### Pergunta 1

A abordagem **Nativa Pura** tem como principal desvantagem o **custo duplicado**, uma vez que exige o desenvolvimento de uma aplicação para cada sistema operativo (e.g., **Swift** para iOS e **Kotlin** para Android). No entanto, oferece vantagens como **flexibilidade** máxima e o melhor **desempenho**.

Existem duas grandes técnicas na abordagem **Híbrida-Nativa**. A primeira, usada pelo React Native, recorre a um **JS Engine** para fazer a ponte com os componentes nativos em tempo de **execução**. A segunda, usada por frameworks como Flutter e .NET MAUI, utiliza um **Cross-compiler** que traduz o código para a plataforma final em tempo de **compilação**.

Uma das diferenças fundamentais entre as frameworks Híbrida-Nativa é a forma como desenham a interface. Frameworks como React Native usam widgets **OEM**, que são os componentes gráficos nativos do SO. Já o Flutter usa widgets **Custom**, que são desenhados pela própria framework, garantindo que a aparência é **a mesma** entre plataformas.

A framework Híbrida-Nativa mais popular, tanto em pesquisas Google como em utilização por developers, tem sido o **Flutter**, desenvolvido pela Google e que usa a linguagem **Dart**. A sua principal concorrente é o **React Native**, desenvolvido pelo Facebook.

A capacidade de atualizar uma app sem passar pela store chama-se **Code Push** e é possível em frameworks que usam um JS Engine, como o React Native. 